---
title: エラー ソース検出への参加
description: エラー ソース検出への参加
ms.assetid: 349c8f06-be79-4a40-8b9f-cbefc563f6de
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラー ソースの検出
- WHEA WDK、エラー ソースの検出
- ハードウェア エラー WDK WHEA、エラー ソースの検出
- エラー WDK WHEA、エラー ソースの検出
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラー ソースの検出
- PSHED プラグイン WDK WHEA、エラー ソースの検出
- WDK WHEA エラー ソースの検出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee5bad768e29f04c4822d51506d324a68bfbb26f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387159"
---
# <a name="participating-in-error-source-discovery"></a>エラー ソース検出への参加


エラー ソースの検出に参加するにプラグインの PSHED を実装する必要があります、 [ *GetAllErrorSources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_get_all_error_sources)コールバック関数。 エラー ソースの検出に参加している PSHED プラグインは、省略可能な実装も[ *GetErrorSourceInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_get_error_source_info)コールバック関数。

次のコード例では、これらのコールバック関数を実装する方法を示します。

```cpp
//
// The PSHED plug-in's GetAllErrorSources callback function
//
NTSTATUS
  GetAllErrorSources(
    IN OUT PVOID PluginContext,
    IN OUT PULONG Count,
    IN OUT PWHEA_ERROR_SOURCE_DESCRIPTOR *ErrorSources,
    IN OUT PULONG Length
    )
{
  // Check if there is enough space remaining in the buffer
  // that contains the array of error source descriptors to 
  // include any additional error sources to be reported by
  // the PSHED plug-in.
  if (...)
  {
    // Update the list of error sources by modifying the
    // existing error sources in the list and adding any
    // additional error sources to the list.
    ...

    // If the number of error sources in the list has changed
    // update the count that is returned back to the kernel.
    *Count = ...;

    // If successful, return success status
    if (...)
    {
      return STATUS_SUCCESS;
    }

    // Failed to update the list of error sources
    else
    {
      return STATUS_UNSUCCESSFUL;
    }
  }

  // Insufficient space in the buffer.
  else
  {
    // Set the length the necessary buffer size
    *Length = ...;

    return STATUS_BUFFER_TOO_SMALL;
  }
}

//
// The PSHED plug-in's GetErrorSourceInfo callback function
//
NTSTATUS
  GetErrorSourceInfo(
    IN OUT PVOID PluginContext,
    IN OUT PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource
    )
{
  // Modify the information contained in the
  // error source descriptor as appropriate.
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to update the error source information
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}
```

エラー ソースの検出に参加している PSHED プラグインを指定する必要があります、 **PshedFADiscovery**フラグを付けるときに、[登録](registering-a-pshed-plug-in.md)自体と、オペレーティング システムを使用します。

 

 




