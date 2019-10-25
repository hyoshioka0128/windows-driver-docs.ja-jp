---
title: エラーの挿入への参加
description: エラーの挿入への参加
ms.assetid: 0bd9efbd-e98d-457a-a28f-e09dcb5ae24d
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、エラー挿入
- WHEA WDK、エラー挿入
- ハードウェアエラー WDK WHEA、エラー挿入
- エラー WDK WHEA、エラー挿入
- プラットフォーム固有のハードウェアエラードライバープラグイン WDK WHEA、エラー挿入
- PSHED プラグイン WDK WHEA、エラー挿入
- エラー挿入 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35dd295977e61e374606baa3d82e1f4fb51d527c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826187"
---
# <a name="participating-in-error-injection"></a>エラーの挿入への参加


エラー情報の取得に参加するには、次のコールバック関数を実装する必要があります。

[*GetInjectionCapabilities*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_get_injection_capabilities)

[*InjectError*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_inject_error)

これらのコールバック関数を実装する方法を次のコード例に示します。

```cpp
//
// The PSHED plug-in's GetInjectionCapabilities callback function
//
NTSTATUS
  GetInjectionCapabilities(
    IN OUT PVOID PluginContext,
    OUT PWHEA_ERROR_INJECTION_CAPABILITIES Capabilities
    )
{
  // Set the members in the structure pointed to by the
  // Capabilities parameter to indicate the error injection
  // capabilities supported by the PSHED plug-in.
  ...

  // Return success status
  return STATUS_SUCCESS;
}

//
// The PSHED plug-in's InjectError callback function
//
NTSTATUS
  InjectError(
    IN OUT PVOID PluginContext,
    IN ULONG ErrorType,
 IN ULONGLONG Parameter1,
    IN ULONGLONG Parameter2,
    IN ULONGLONG Parameter3,
    IN ULONGLONG Parameter4
    )
{
  // Inject the hardware error specified in the ErrorType
  // parameter into the hardware platform.
  // Parameter1 through Parameter4 contain any additional
  // data that is required to inject the error.
  ...

  // Note: For injected errors that are fatal or otherwise
  // unrecoverable, this callback function might not continue
  // execution past this point before the Windows kernel
  // generates a bug check in response to the error condition.

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to update the error record
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}
```

エラー挿入に参加する**PshedFAErrorInjection**は、オペレーティングシステムに[登録](registering-a-pshed-plug-in.md)するときに、フラグを指定する必要があります。

 

 




