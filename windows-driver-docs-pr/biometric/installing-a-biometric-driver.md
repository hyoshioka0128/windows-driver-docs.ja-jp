---
title: 生体認証ドライバーのインストール
description: 生体認証ドライバーのインストール
ms.assetid: f1ae7346-c55b-484e-a94a-b4e22f5fafed
keywords:
- 生体認証ドライバー WDK をインストールします。
- 生体認証ドライバー WDK 生体認証をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3baaf63f05b9fa93aff0c72317408bf7d32a7289
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573093"
---
# <a name="installing-a-biometric-driver"></a>生体認証ドライバーのインストール


ベンダーは、WBDI ドライバーをインストールするための INF ファイルを提供できます。

次に生体認証デバイスのインストールに関するガイドラインの一覧を示します。 このトピックのコード例は、の WudfBioUsbSample.inx ファイルから取得、 [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver):

-   WBDI ドライバーは、「生体認証します」のクラスを指定する必要があります。 GUID ClassGuid に対応する値と等しく設定\_DEVCLASS\_Devguid.h で生体認証。

    ```cpp
    [Version]
    Signature="$Windows NT$"
    Class=Biometric
    ClassGuid={53D29EF7-377C-4D14-864B-EB3A85769359}
    ```

-   します。ハードウェア セクションで、AddReg ディレクティブを指定する 3 つのセクションでは、レジストリに追加するエントリを含めることを指定します。

    ```cpp
    [Biometric_Install.NT.hw]
    AddReg=Biometric_Device_AddReg
    AddReg=DriverPlugInAddReg, DatabaseAddReg
    ```

-   名前付きのセクションで参照を提供します。ハードウェア セクション。 \[生体認証の\_デバイス\_AddReg\]セクションは、生体認証デバイス、デバイスを含め、排他的なフラグとシステム スリープ解除/アイドル状態の値を設定します。 Windows 生体認証フレームワークで認識される、UMDF に基づく WBDI ドライバーは「排他」の値を 1 に設定する必要があります。 最初の 2 行、\[生体認証の\_デバイス\_AddReg\]セクションは、デバイスは、管理者またはローカル システム アカウントによってのみ開くことができるようにアクセス制御リスト (ACL) の権限を指定します。 これらの acl アクセス許可を指定するとサード パーティ製のアプリケーションはデバイスを開くし、WinBio サービスが実行されていないときに指紋データをキャプチャすることはできません。 例:

    ```cpp
    [Biometric_Device_AddReg]
    HKR,,"DeviceCharacteristics",0x10001,0x0100     ; Use same security checks on relative opens
    HKR,,"Security",,"D:P(A;;GA;;;BA)(A;;GA;;;SY)"  ; Allow generic-all access to Built-in administrators and Local system
    HKR,,"LowerFilters",0x00010008,"WinUsb" ; FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
    HKR,,"Exclusive",0x10001,1
    HKR,,"SystemWakeEnabled",0x00010001,1
    HKR,,"DeviceIdleEnabled",0x00010001,1
    HKR,,"UserSetDeviceIdleEnabled",0x00010001,1
    HKR,,"DefaultIdleState",0x00010001,1
    HKR,,"DefaultIdleTimeout",0x00010001,5000
    ```

    レガシ (WBDI 以外) の生体認証スタックへの機能を公開する WBDI ドライバーは、排他的な値を 0 に設定する必要があります。 この値が 0 に設定されている場合は、Windows 生体認証フレームワークは、デバイスを制御しようとはせず、WBF デバイスは公開されません。

    ベンダーは、従来のスタックや、WBF で動作する 1 つのドライバー バイナリを持つことができますが、2 つが同時に動作することはできません。 WBF は、排他アクセスでデバイスを起動できる場合にのみ動作します。

-   2 番目の名前付きセクションには、プラグインのアダプターのレジストリ値が含まれています。 サンプルでは、Microsoft 提供のセンサーのアダプターと記憶域アダプターを使用します。 このセクションでは、SystemSensor 値を設定して Windows ログインのサポートもできます。

    ```cpp
    [DriverPlugInAddReg]
    HKR,WinBio\Configurations,DefaultConfiguration,,"0"
    HKR,WinBio\Configurations\0,SensorMode,0x10001,1                                ; Basic - 1, Advanced - 2
    HKR,WinBio\Configurations\0,SystemSensor,0x10001,1                              ; UAC/Winlogon - 1
    HKR,WinBio\Configurations\0,SensorAdapterBinary,,"WinBioSensorAdapter.DLL"      ; Windows built-in WBDI sensor adapter.
    HKR,WinBio\Configurations\0,EngineAdapterBinary,,"EngineAdapter.DLL"            ; Vendor engine
    HKR,WinBio\Configurations\0,StorageAdapterBinary,,"WinBioStorageAdapter.DLL"    ; Windows built-in storage adapter
    HKR,WinBio\Configurations\0,DatabaseId,,"6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50"  ; Unique database GUID
    ```

-   最後に、3 番目のセクションでは、データベースのサービスの次のレジストリ値を設定します。 特定の GUID は、特定の形式の場合は、各仕入先データベースで一意である必要があります。 たとえば、サンプルからのこのコード例では、INF ファイルで、独自の一意の GUID を 6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50 を変更します。

    ```cpp
    [DatabaseAddReg]
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},BiometricType,0x00010001,0x00000008
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},Attributes,0x00010001,0x00000001
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},Format,,"00000000-0000-0000-0000-000000000000"
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},InitialSize,0x00010001,0x00000020
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},AutoCreate,0x00010001,0x00000001
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},AutoName,0x00010001,0x00000001
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},FilePath,,""
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},ConnectionString,,""
    ```

-   WBDI と従来のドライバーを区別する、ベンダーする必要があります特徴スコア ドライバーのファイルで設定、INX。 特徴のスコアに設定されていない、 [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)サンプル。 特徴のスコアを設定する方法についての詳細については、次を参照してください。[生体認証ドライバーを Windows Update で順位付け](ranking-a-biometric-driver-on-windows-update.md)します。

INX ファイルと INF ファイルからの違いについては、次を参照してください。 [INX INF ファイルを作成するファイルを使用する](https://msdn.microsoft.com/library/windows/hardware/ff545473)します。

従来、ドライバーを使用した WBDI ドライバーを置き換えるためには、次の手順を使用します。

1.  現在アクティブなすべての WBF アプリケーションを閉じます。

2.  WBDI ドライバーをアンインストールします。

3.  WBF サービスを停止、再起動、および、再度停止します。

4.  従来、ドライバーをインストールします。

 

 





