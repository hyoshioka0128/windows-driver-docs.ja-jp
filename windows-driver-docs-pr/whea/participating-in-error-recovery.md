---
title: エラーからの回復への参加
description: エラーからの回復への参加
ms.assetid: 79f534b2-a5eb-4249-bfff-2f40c25805a6
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラーからの回復
- WHEA WDK、エラーからの回復
- ハードウェア エラー WDK WHEA、エラーからの回復
- エラー WDK WHEA、エラーからの回復
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラーからの回復
- PSHED プラグイン WDK WHEA、エラーからの回復
- WDK WHEA エラーの回復
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: def79e808f5256e4e2d2a10dd91dd5b44ef94c25
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386453"
---
# <a name="participating-in-error-recovery"></a>エラーからの回復への参加


エラーからの回復に参加するにプラグインの PSHED を実装する必要があります、 [ *AttemptRecovery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_attempt_error_recovery)コールバック関数。

次のコード例では、このコールバック関数を実装する方法を示します。

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

エラーからの回復に参加している PSHED プラグインを指定する必要があります、 **PshedFAErrorRecovery**フラグを付けるときに、[登録](registering-a-pshed-plug-in.md)オペレーティング システム自体。

 

 




