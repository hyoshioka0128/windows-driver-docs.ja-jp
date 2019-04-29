---
title: コード クラスのインストーラーの 完了-インストール アクションの例
description: コード クラスのインストーラーの 完了-インストール アクションの例
ms.assetid: 394f321c-2ce4-4773-b5df-e30ce23b7207
keywords:
- 完了-インストール アクション WDK デバイスのインストール
- クラスのインストーラー WDK デバイス インストールの完了インストール アクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00db8c010124f6a96f9a1b5d28f7c5458c483a0c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361196"
---
# <a name="code-example-finish-install-actions-in-a-class-installer"></a>コードの例:クラス インストーラーでのインストールの完了アクション


この例では、クラスのインストーラーは、完了-インストール操作をサポートするために、次の操作を実行します。

-   クラスのインストーラーを受信すると、 [ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)要求、インストーラーが指定した関数を呼び出して*FinishInstallActionsNeeded*に実行するアクションが完了-インストールがあるかどうかを決定します。 (コードを*FinishInstallActionsNeeded*関数は、この例では表示されません)。

    場合*FinishInstallActionsNeeded*返します**TRUE**、クラスのインストーラー呼び出し[ **SetupDiGetDeviceInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff551104)を取得する、デバイスのデバイスのパラメーターをインストールします。 呼び出して[ **SetupDiSetDeviceInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff552141)を設定する、 **FlagsEx**のメンバー、 [ **SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346) DI_FLAGSEX_FINISHINSTALL_ACTION フラグを使用してデバイスの構造体。 このフラグを設定すると、送信する Windows、 [ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684)すべてのクラスのインストーラー、co-installer クラスとのこのインストールに関係しているデバイスの共同インストーラーへの要求デバイスです。 この要求は、完了-インストール操作が完了した点を除いて、すべてのインストール操作の後に送信されます。

-   もう一度呼び出すクラスのインストーラーは DIF_FINISHINSTALL_ACTION 要求を受け取る、 *FinishInstallActionsNeeded*とを確認するかどうか、完了-インストール アクションを実行するが、そうである場合は、完了-インストール操作を実行します。 します。 クラスのインストーラーは、完了インストール操作が進行状況と完了インストール アクション DIF_FINISHINSTALL_ACTION 要求の処理から戻る前に完了するまで待機をユーザーに通知します。

-   完了-インストール操作が成功した場合、クラスのインストーラーは完了-インストール操作が成功したユーザーを通知します。

-   完了-インストール操作には、完了-インストール アクションを実行するシステムの再起動が必要な場合、クラスのインストーラーは、デバイスのデバイスのインストール パラメーターを取得する SetupDiGetDeviceInstallParams から呼び出されを呼び出して設定する SetupDiSetDeviceInstallParams、**フラグ**DI_NEEDREBOOT フラグを使用したデバイスの SP_DEVINSTALL_PARAMS 構造体のメンバー。 インストーラーには、システムの再起動が必要であるユーザーも通知します。

-   完了-インストール操作が失敗した場合、デバイスが列挙されたときにもう一度完了-インストール操作をしようとする必要がありますは、クラスのインストーラーがこのような状況のユーザーに通知します。

    **注**  1 回のみ実行完了-インストール アクションを Windows 8 で開始します。 Windows は自動的に再実行されませんが、次回特にないデバイスが列挙完了インストール アクションは実行されませんであるためです。

     

-   完了-インストール アクションことはできませんが成功しますが、クラスのインストーラーがこのような状況のユーザーに通知の完了インストール操作の失敗とクラスのインストーラーを決定するかどうか。

-   既定では、クラスのインストーラーを返します ERROR_DI_DO_DEFAULT DIF_FINISHINSTALL_ACTION 要求への応答で完了-インストール操作が成功した場合や完了-インストール操作が失敗しました、インストーラーは、完了-インストール操作が必要があるを決定します。行われません。 インストーラーでは、完了-インストール操作が失敗した場合にのみ、Win32 エラー コードと 完了-インストール操作が管理者のコンテキストに、デバイスが列挙されたときにもう一度を試行する必要があるを返します。

    **注**  1 回のみ実行完了-インストール アクションを Windows 8 で開始します。 Windows は自動的に再実行されませんが、次回特にないデバイスが列挙完了インストール アクションは実行されませんであるためです。

     

次のクラス インストーラーのコード例では、完了-インストール アクションを実装するクラスのインストーラーのコードの基本構造を示します。

```cpp
DWORD CALLBACK
SampleClassInstaller(
  IN DI_FUNCTION  InstallFunction,
  IN HDEVINFO  DeviceInfoSet,
  IN PSP_DEVINFO_DATA  DeviceInfoData,
  )
{
  SP_DEVINSTALL_PARAMS DeviceInstallParams;
  DWORD ReturnValue = ERROR_DI_DO_DEFAULT; // The default return value

  switch(InstallFunction)
  {
    case DIF_NEWDEVICEWIZARD_FINISHINSTALL:
      //
      // Processing for finish-install wizard pages
      // If the class installer has wizard pages,
      // set ReturnValue to NO_ERROR
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
      // Processing for finish-install actions
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
        // should not be attempted again: clean up and
        // notify the user of the failure
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

 

 





