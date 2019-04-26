---
title: エラーの挿入への参加
description: エラーの挿入への参加
ms.assetid: 0bd9efbd-e98d-457a-a28f-e09dcb5ae24d
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラーの挿入
- WHEA WDK、エラーの挿入
- ハードウェア エラー WDK WHEA、エラーの挿入
- エラー WDK WHEA、エラーの挿入
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラーの挿入
- PSHED プラグイン WDK WHEA、エラーの挿入
- WDK WHEA エラーの挿入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba750aebcad32ffa450042a5189109aee3172c4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341910"
---
# <a name="participating-in-error-injection"></a>エラーの挿入への参加


エラー情報の取得に参加するには、プラグイン PSHED は次のコールバック関数を実装する必要があります。

[*GetInjectionCapabilities*](https://msdn.microsoft.com/library/windows/hardware/ff559372)

[*InjectError*](https://msdn.microsoft.com/library/windows/hardware/ff559397)

次のコード例では、これらのコールバック関数を実装する方法を示します。

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

エラーの挿入に参加している PSHED プラグインを指定する必要があります、 **PshedFAErrorInjection**フラグを付けるときに、[登録](registering-a-pshed-plug-in.md)オペレーティング システム自体。

 

 




