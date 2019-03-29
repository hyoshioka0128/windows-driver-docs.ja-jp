---
title: SetupAPI 関数の呼び出し
description: SetupAPI 関数の呼び出し
ms.assetid: 757AAF33-B57B-4ab8-A034-23B8AC0C5CB3
keywords:
- SetupAPI 関数 WDK、呼び出し元
- WDK SetupAPI 関数を呼び出す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ad0cbe865e850a35185ff994e996b5163736ab8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580535"
---
# <a name="calling-setupapi-functions"></a>SetupAPI 関数の呼び出し


このセクションでは、呼び出すときに従う必要のあるガイドラインを提供します。、 [SetupAPI](setupapi.md)から関数を[共同インストーラー](writing-a-co-installer.md)または[デバイス インストール アプリケーション](writing-a-device-installation-application.md)します。

-   [SetupAPI 関数を呼び出す場合の規則](#calling-setupapi-functions)
-   [既定値の差分コード ハンドラー関数を呼び出す場合の規則](#calling-the-default-dif-code-handler-functions)

### <a href="" id="calling-setupapi-functions"></a>SetupAPI 関数を呼び出す場合の規則

クラスのインストーラー共同インストーラーでは、次を呼び出す必要がありますいない[SetupAPI](setupapi.md)関数。

-   **SetupQueueCopy**

-   **SetupQueueCopyIndirect**

-   **SetupQueueCopySection**

-   **SetupQueueDefaultCopy**

-   **SetupQueueDelete**

-   **SetupQueueDeleteSection**

-   **SetupQueueRename**

-   **SetupQueueRenameSection**

-   **SetupScanFileQueue**

    **注**  クラスのインストーラーと共同インストーラーが呼び出し元から禁止されている**SetupScanFileQueue** SPQ_SCAN_PRUNE_COPY_QUEUE フラグが設定いる場合にのみ、*フラグ*パラメーター。

     

### <a href="" id="calling-the-default-dif-code-handler-functions"></a>既定値の差分コード ハンドラー関数を呼び出す場合の規則

既定のデバイス インストール機能 (差分) コードが、差分要求をする前に処理最初**SetupDiCallClassInstaller**要求の処理後の登録されている共同インストーラーを呼び出します。

[共同インストーラー](writing-a-co-installer.md)と[デバイス インストール アプリケーション](writing-a-device-installation-application.md)既定 DIF コード ハンドラー関数を呼び出していない必要があります。 これらのハンドラー関数を直接呼び出すは登録されているすべての共同インストーラーをバイパスし、これらのインストーラーを格納する任意のデバイスの内部状態を無効できます。

次の表では、既定 DIF コード ハンドラー関数を含む差分コードを示します。

| コードの差分                                                             | 既定の差分コード ハンドラー関数                                                  |
|----------------------------------------------------------------------|------------------------------------------------------------------------------------|
| [**DIF_PROPERTYCHANGE**](https://msdn.microsoft.com/library/windows/hardware/ff543712)                | [**SetupDiChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff550930)                               |
| [**DIF_FINISHINSTALL_ACTION**](https://msdn.microsoft.com/library/windows/hardware/ff543684)   | [**SetupDiFinishInstallAction**](https://msdn.microsoft.com/library/windows/hardware/ff551022)               |
| [**DIF_INSTALLDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff543692)                  | [**SetupDiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552039)                           |
| [**DIF_INSTALLINTERFACES**](https://msdn.microsoft.com/library/windows/hardware/ff543695)          | [**SetupDiInstallDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff552043)       |
| [**DIF_INSTALLDEVICEFILES**](https://msdn.microsoft.com/library/windows/hardware/ff543694)        | [**SetupDiInstallDriverFiles**](https://msdn.microsoft.com/library/windows/hardware/ff552048)                 |
| [**DIF_REGISTER_COINSTALLERS**](https://msdn.microsoft.com/library/windows/hardware/ff543715) | [**SetupDiRegisterCoDeviceInstallers**](https://msdn.microsoft.com/library/windows/hardware/ff552085) |
| [**DIF_REGISTERDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff543713)                | [**SetupDiRegisterDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff552091)                 |
| [**DIF_REMOVE**](https://msdn.microsoft.com/library/windows/hardware/ff543717)                                | [**SetupDiRemoveDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552097)                             |
| [**DIF_SELECTBESTCOMPATDRV**](https://msdn.microsoft.com/library/windows/hardware/ff543719)      | [**SetupDiSelectBestCompatDrv**](https://msdn.microsoft.com/library/windows/hardware/ff552112)               |
| [**DIF_SELECTDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff543723)                    | [**SetupDiSelectDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552115)                             |
| [**DIF_UNREMOVE**](https://msdn.microsoft.com/library/windows/hardware/ff543728)                            | [**SetupDiUnremoveDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552193)                         |

 

 

 





