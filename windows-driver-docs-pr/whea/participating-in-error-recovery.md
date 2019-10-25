---
title: エラーからの回復への参加
description: エラーからの回復への参加
ms.assetid: 79f534b2-a5eb-4249-bfff-2f40c25805a6
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、エラー回復
- WHEA WDK、エラー回復
- ハードウェアエラー WDK WHEA、エラー回復
- エラー WDK WHEA、エラー回復
- プラットフォーム固有のハードウェアエラードライバープラグイン WDK WHEA、エラー回復
- PSHED プラグイン WDK WHEA、エラー回復
- エラー回復 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9037cf42b8190ff4436fc1627a088b481a24933f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826183"
---
# <a name="participating-in-error-recovery"></a>エラーからの回復への参加


エラー復旧に参加するには、 [*AttemptRecovery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_attempt_error_recovery)コールバック関数を実装する必要があります。

このコールバック関数を実装する方法を次のコード例に示します。

```cpp
//
// The PSHED plug-in's AttemptRecovery callback function
//
NTSTATUS
  AttemptRecovery(
    IN OUT PVOID PluginContext,
    IN ULONG BufferLength,
    IN PWHEA_ERROR_RECORD ErrorRecord
    )
{
  // Check if the error condition was not corrected by the
  // operating system or by the PSHED.
  if (ErrorRecord->Header.Severity != WheaErrSevCorrected)
  {
    // Attempt to correct the error condition.
    ...

    // If not successful, return failure status
    if (...)
    {
      return STATUS_UNSUCCESSFUL;
    }
  }

  // Perform any additional operations that are required
  // to fully recover from the error condition.
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to fully recover from the error condition
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}
```

エラー回復に参加するプラグインでは、オペレーティングシステムに[登録](registering-a-pshed-plug-in.md)するときに**PshedFAErrorRecovery**フラグを指定する必要があります。

 

 




