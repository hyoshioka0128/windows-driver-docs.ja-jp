---
title: 既定の DIF コード ハンドラーの呼び出し
description: 既定の DIF コード ハンドラーの呼び出し
ms.assetid: bc168c30-2269-4760-bc0a-e3e6ee3ce720
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb1987eb32b093cde2520b7c33714bc6fd3c3b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385283"
---
# <a name="calling-the-default-dif-code-handlers"></a>既定の DIF コード ハンドラーの呼び出し


差分の既定のコード ハンドラーが差分コードのシステム定義の既定の操作を実行し、*共同インストーラー*差分の要求の前に処理が最初に**SetupDiCallClassInstaller**リコール、登録要求の処理後の共同インストーラー。

**注**  の操作**SetupDiCallClassInstaller** DIF 要求の処理後にクラスのインストーラーを思い出してくださいするように構成することはできません。

 

そのような場合で、*クラス インストーラー*操作を実行する必要があります DIF 要求の既定のハンドラーが呼び出されると、クラスのインストーラーする必要がありますを直接呼び出す既定のハンドラー次のように、差分要求を処理するとき。

1.  既定のハンドラーを呼び出す前に行う必要がある操作を実行します。

2.  既定の操作を実行する既定のハンドラーを呼び出します。

    **注**  クラスのインストーラーは、既定のハンドラーの操作を優先するしないでください。

     

3.  既定のハンドラーが返された後に行う必要がある操作を実行します。

4.  処理が失敗した場合は、Win32 エラーを返すまたは NO_ERROR が返さクラスのインストーラーが正常に差分要求の処理を完了します。

**重要な**  [共同インストーラー](writing-a-co-installer.md)と[デバイス インストール アプリケーション](writing-a-device-installation-application.md)既定 DIF コード ハンドラーを呼び出していない必要があります。

 

このメソッドを使用する必要があります、状況の例は、既定のハンドラーを呼び出す方法の詳細情報を参照してください[ **SetupDiInstallDevice** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)上、 [ **DIF_INSTALLDEVICE。** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice)リファレンスのページを要求します。

次の表では、既定のハンドラーを持つ差分コードを示します。

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

 

 

 





