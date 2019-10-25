---
title: エラー ソース検出への参加
description: エラー ソース検出への参加
ms.assetid: 349c8f06-be79-4a40-8b9f-cbefc563f6de
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、エラーソース検出
- WHEA WDK、エラーソースの検出
- ハードウェアエラー WDK WHEA、エラーソース検出
- エラー WDK WHEA、エラーソース検出
- プラットフォーム固有のハードウェアエラードライバープラグイン WDK WHEA、エラーソース検出
- PSHED プラグイン WDK WHEA、エラーソース検出
- エラーソース検出 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0bea3f2ed669be34924d20197658dee6b610cd4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837997"
---
# <a name="participating-in-error-source-discovery"></a>エラー ソース検出への参加


エラーソースの検出に参加するには、 [*GetAllErrorSources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_get_all_error_sources)コールバック関数を実装する必要があります。 エラーソースの検出に参加しているプラグインは、オプションの[*GetErrorSourceInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_get_error_source_info)コールバック関数を実装することもできます。

これらのコールバック関数を実装する方法を次のコード例に示します。

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

エラーソースの検出に参加しているプラグインでは、オペレーティングシステムに[登録](registering-a-pshed-plug-in.md)するときに**PshedFADiscovery**フラグを指定する必要があります。

 

 




