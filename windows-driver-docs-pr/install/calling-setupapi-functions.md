---
title: SetupAPI 関数の呼び出し
description: SetupAPI 関数の呼び出し
ms.assetid: 757AAF33-B57B-4ab8-A034-23B8AC0C5CB3
keywords:
- SetupAPI 関数 WDK、呼び出し元
- WDK SetupAPI 関数を呼び出す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b26c11d0c8b9fd35c83a50bdb7d3527267ff1775
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385285"
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
| [**DIF_PROPERTYCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-propertychange)                | [**SetupDiChangeState**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)                               |
| [**DIF_FINISHINSTALL_ACTION**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)   | [**SetupDiFinishInstallAction**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85))               |
| [**DIF_INSTALLDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice)                  | [**SetupDiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)                           |
| [**DIF_INSTALLINTERFACES**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installinterfaces)          | [**SetupDiInstallDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)       |
| [**DIF_INSTALLDEVICEFILES**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevicefiles)        | [**SetupDiInstallDriverFiles**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)                 |
| [**DIF_REGISTER_COINSTALLERS**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-register-coinstallers) | [**SetupDiRegisterCoDeviceInstallers**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers) |
| [**DIF_REGISTERDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-registerdevice)                | [**SetupDiRegisterDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)                 |
| [**DIF_REMOVE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-remove)                                | [**SetupDiRemoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)                             |
| [**DIF_SELECTBESTCOMPATDRV**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-selectbestcompatdrv)      | [**SetupDiSelectBestCompatDrv**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)               |
| [**DIF_SELECTDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-selectdevice)                    | [**SetupDiSelectDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice)                             |
| [**DIF_UNREMOVE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-unremove)                            | [**SetupDiUnremoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiunremovedevice)                         |

 

 

 





