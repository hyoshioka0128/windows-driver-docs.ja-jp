---
title: コードで共同インストーラー - インストールが完了アクションの例
description: コードで共同インストーラー - インストールが完了アクションの例
ms.assetid: 57d41fec-cedb-436e-858e-c010a8bd6506
keywords:
- 完了-インストール アクション WDK デバイスのインストール
- 共同インストーラー WDK デバイスのインストールが完了-インストール アクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc087da0bed51e9c47ac2d2dc3d168f8f5bf7292
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361190"
---
# <a name="code-example-finish-install-actions-in-a-co-installer"></a>コードの例:共同インストーラーでのインストールの完了アクション


この例では、共同インストーラーは、完了-インストール操作をサポートするために、次の操作を実行します。

-   共同インストーラーを受信すると、 [ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)要求、インストーラーが指定した関数を呼び出して*FinishInstallActionsNeeded*に実行するアクションが完了-インストールがあるかどうかを決定します。 (コードを*FinishInstallActionsNeeded*関数は、この例では表示されません)。

    場合*FinishInstallActionsNeeded*返します**TRUE**、共同インストーラー呼び出し[ **SetupDiGetDeviceInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff551104)を取得する、デバイスと、呼び出しのデバイスのインストール パラメーター [ **SetupDiSetDeviceInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff552141)を設定する、 **FlagsEx** のメンバー[ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346) DI_FLAGSEX_FINISHINSTALL_ACTION フラグを使用してデバイスの構造体。 このフラグを設定すると、送信する Windows、 [ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684)すべてのクラスのインストーラー、co-installer クラスとのこのインストールに関係しているデバイスの共同インストーラーへの要求デバイスです。 完了した後、完了-インストール アクションを除く、すべてのインストール操作にこの要求が送信されます。

-   共同インストーラーをもう一度呼び出す共同インストーラーは DIF_FINISHINSTALL_ACTION 要求を受け取る、 *FinishInstallActionsNeeded*と判断するかどうか、完了インストール アクションを実行するが、そうである場合は、実行、完了-インストール アクション。 共同インストーラーは、進行状況と完了インストール アクション DIF_FINISHINSTALL_ACTION 要求の処理から戻る前に完了するまで待機に 完了-インストール アクションのあるユーザーに通知します。

-   完了-インストール操作が成功した場合、共同インストーラーが完了-インストールが成功したアクションをユーザーに通知します。

-   完了-インストール操作には、完了-インストール アクションを実行するシステムの再起動が必要な場合共同インストーラーは、デバイスのデバイスのインストール パラメーターを取得する SetupDiGetDeviceInstallParams から呼び出されを呼び出して設定する SetupDiSetDeviceInstallParams、**フラグ**DI_NEEDREBOOT フラグを使用してデバイスの SP_DEVINSTALL_PARAMS 構造体のメンバー。 インストーラーには、システムの再起動が必要であるユーザーも通知します。

-   完了インストール操作の失敗、完了-インストール アクションに次に、デバイスを列挙すると、共同インストーラーがこのような状況のユーザーに通知するときにもう一度を試みたかどうか。

    **注**  1 回のみ実行完了-インストール アクションを Windows 8 で開始します。 Windows は自動的に再実行されませんが、次回特にないデバイスが列挙完了インストール アクションは実行されませんであるためです。

     

-   完了-インストール操作が成功することはできません、共同インストーラーがこのような状況のユーザーに通知されるのと共同インストーラーの 完了-インストール操作の失敗を決定するかどうか。

-   既定では、共同インストーラーを返します NO_ERROR DIF_FINISHINSTALL_ACTION 要求への応答で完了-インストール操作が成功した場合、または 完了-インストール操作に失敗し、共同インストーラーが完了-インストール操作がされないことを決定場合もう一度実行します。 共同インストーラーは、完了-インストール操作が失敗した場合にのみ、Win32 エラー コードと 完了-インストール操作が管理者のコンテキストに、デバイスが列挙されたときにもう一度を試行する必要があるを返します。

    **注**  1 回のみ実行完了-インストール アクションを Windows 8 で開始します。 Windows は自動的に再実行されませんが、次回特にないデバイスが列挙完了インストール アクションは実行されませんであるためです。

     

次の共同インストーラーのコード例では、完了-インストール アクションを実装するコードを共同インストーラーの基本構造を示します。

```cpp
DWORD CALLBACK
SampleCoInstaller(
  IN DI_FUNCTION  InstallFunction,
  IN HDEVINFO  DeviceInfoSet,
  IN PSP_DEVINFO_DATA  DeviceInfoData,
  IN OUT PCOINSTALLER_CONTEXT_DATA  Context
  )
{
  SP_DEVINSTALL_PARAMS DeviceInstallParams;
  DWORD ReturnValue = NO_ERROR; // The default return value

  switch(InstallFunction)
  {
    case DIF_NEWDEVICEWIZARD_FINISHINSTALL:
      //
      // Processing for finish-install wizard pages
      //
      // Processing for finish-install actions
      if (FinishInstallActionsNeeded())
      {
        // Obtain the device install parameters for the device
        // and set the DI_FLAGSEX_FINISHINSTALL_ACTION flag
        DeviceInstallParams.cbSize = sizeof(DeviceInstallParams);
        if (SetupDiGetDeviceInstallParams(DeviceInfoSet, DeviceInfoData, &DeviceInstallParams))
        {
          DeviceInstallParams.FlagsEx |= DI_FLAGSEX_FINISHINSTALL_ACTION;
          SetupDiSetDeviceInstallParams(DeviceInfoSet, DeviceInfoData, &DeviceInstallParams);
        }
      }
      break;

    case DIF_FINISHINSTALL_ACTION:
      if (FinishInstallActionsNeeded())
      {
        //
        // Perform the finish-install actions,
        // notify the user that finish install actions
        // are in progress and wait for
        // the finish-install actions to complete
        //
        // If the finish-install actions succeed, notify the user
        //
        // If the finish install actions require a system restart: 
        // notify the user, call SetupDiGetDeviceInstallParams 
        // to obtain the device install parameters for the device in 
        // DeviceInstallParams, and call SetupDiSetInstallParams to set 
        // the DI_NEEDREBOOT flag in DeviceInstallParams.Flags
        // 
        // If the finish install actions failed, but
        // should be attempted again: clean up,
        // notify the user of the failure, and
        // set ReturnValue to an appropriate Win32 error code
        //
        // If the finish install actions failed and 
        // should not be attempted again: clean up
        // and notify the user of the failure
        //
        // Starting with Windows 8, a finish-install action
        // is only run once. Windows will not automatically
        // run it again, especially not the next time
        // the device is enumerated because that is not when
        // finish-install actions are run.
        //
      }
      break;
  }

  return ReturnValue;
}
```

 

 





