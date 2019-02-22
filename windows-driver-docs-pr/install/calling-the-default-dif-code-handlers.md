---
title: 既定の差分コード ハンドラーを呼び出す
description: 既定の差分コード ハンドラーを呼び出す
ms.assetid: bc168c30-2269-4760-bc0a-e3e6ee3ce720
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c67142d1b5f71d813c1df651d42f56fb8702986
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559022"
---
# <a name="calling-the-default-dif-code-handlers"></a>既定の差分コード ハンドラーを呼び出す


差分の既定のコード ハンドラーが差分コードのシステム定義の既定の操作を実行し、*共同インストーラー*差分の要求の前に処理が最初に**SetupDiCallClassInstaller**リコール、登録要求の処理後の共同インストーラー。

**注**  の操作**SetupDiCallClassInstaller** DIF 要求の処理後にクラスのインストーラーを思い出してくださいするように構成することはできません。

 

そのような場合で、*クラス インストーラー*操作を実行する必要があります DIF 要求の既定のハンドラーが呼び出されると、クラスのインストーラーする必要がありますを直接呼び出す既定のハンドラー次のように、差分要求を処理するとき。

1.  既定のハンドラーを呼び出す前に行う必要がある操作を実行します。

2.  既定の操作を実行する既定のハンドラーを呼び出します。

    **注**  クラスのインストーラーは、既定のハンドラーの操作を優先するしないでください。

     

3.  既定のハンドラーが返された後に行う必要がある操作を実行します。

4.  処理が失敗した場合は、Win32 エラーを返すまたは NO_ERROR が返さクラスのインストーラーが正常に差分要求の処理を完了します。

**重要な**  [共同インストーラー](writing-a-co-installer.md)と[デバイス インストール アプリケーション](writing-a-device-installation-application.md)既定 DIF コード ハンドラーを呼び出していない必要があります。

 

このメソッドを使用する必要があります、状況の例は、既定のハンドラーを呼び出す方法の詳細情報を参照してください[ **SetupDiInstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552039)上、 [ **DIF_INSTALLDEVICE。** ](https://msdn.microsoft.com/library/windows/hardware/ff543692)リファレンスのページを要求します。

次の表では、既定のハンドラーを持つ差分コードを示します。

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

 

 

 





