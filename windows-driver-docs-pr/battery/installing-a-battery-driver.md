---
title: バッテリ ドライバーのインストール
description: バッテリ ドライバーのインストール
ms.assetid: 09db4d88-0cac-4171-8d05-d15a2cf4dab4
keywords:
- バッテリ miniclass ドライバー WDK をインストールします。
- バッテリ クラス ドライバー WDK をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfcd250b0a5ec2475cf5594673b7e52242d0f1d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574357"
---
# <a name="installing-a-battery-driver"></a>バッテリ ドライバーのインストール


## <span id="ddk_installing_a_battery_driver_dg"></span><span id="DDK_INSTALLING_A_BATTERY_DRIVER_DG"></span>


バッテリ ドライバーの INF ファイルでは、ドライバーとデバイスの制御に関する情報を指定します。 バッテリ クラスのメンバーであるすべてのデバイスのバッテリおよびバッテリ クラスのインストーラーには、ドライバーがインストールされます。

このセクションでは、INF ファイルでバッテリに固有のエントリについて説明します。 作成と INF ファイルを配布するドライバーのインストールの詳細については、次を参照してください。 [INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff549520)と[INF ファイルのセクションとディレクティブ](https://msdn.microsoft.com/library/windows/hardware/ff547433)します。

バッテリ ドライバーの INF ファイルには、以下に示すセクションが含まれます。

### <a name="span-idversionspanspan-idversionspanspan-idversionspanversion"></a><span id="Version"></span><span id="version"></span><span id="VERSION"></span>バージョン

バッテリ ドライバーの INF ファイルは、バッテリ クラスと、その GUID を指定します。 を使用して、 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)次の例のように。

``` syntax
[Version]
Signature="$WINDOWS NT$"
Class=Battery
ClassGuid={72631e54-78a4-11d0-bcf7-00aa00b7b32a}
Provider=%MyCo%
```

その %myco% を定義する必要がありますに注意してください、 [ **INF 文字列セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547485) (示されていません)。

### <a name="span-iddestinationdirsspanspan-iddestinationdirsspanspan-iddestinationdirsspandestinationdirs"></a><span id="DestinationDirs"></span><span id="destinationdirs"></span><span id="DESTINATIONDIRS"></span>DestinationDirs

[ **INF DestinationDirs セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547383)、バッテリ ドライバーの INF ファイルをすべての既定値としてドライバー ディレクトリ (12) を指定します。

``` syntax
[DestinationDirs]
DefaultDestDir = 12
```

### <a name="span-idmanufacturerspanspan-idmanufacturerspanspan-idmanufacturerspanmanufacturer"></a><span id="Manufacturer"></span><span id="manufacturer"></span><span id="MANUFACTURER"></span>製造元

[ **INF 製造元セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547454)デバイスの製造元を定義します。

``` syntax
[Manufacturer]
%MyCo%=MyCompany
```

### <a name="span-idmodelsspanspan-idmodelsspanspan-idmodelsspanmodels"></a><span id="Models"></span><span id="models"></span><span id="MODELS"></span>*モデル*

[ **INF*モデル*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456) 、バッテリのプラグ アンド プレイ ハードウェア ID を指定します (として示す*pnpid*の例)。 このセクションが EISA スタイル ID を指定する必要がありますも ACPI を通じて、デバイスが列挙されている場合 (として示す*acpidevnum*)。 これらの Id を作成する方法の詳細については、次を参照してください。、 *Advanced Configuration and Power Interface Specification*、を通じて、 [ACPI/電源管理](https://go.microsoft.com/fwlink/p/?linkid=8760)web サイト。

``` syntax
[MyCompany]
%pnpid.DeviceDesc% = NewBatt_Inst,pnpid
%ACPI\acpidevnum.DeviceDesc% = NewBatt_Inst,ACPI\acpidevnum
```

### <a name="span-idddinstallspanspan-idddinstallspanspan-idddinstallspanddinstall"></a><span id="DDInstall"></span><span id="ddinstall"></span><span id="DDINSTALL"></span>*DDInstall*

[ **INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344) (という名前の NewBatt\_命令の例では)、 [ **INF CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)バッテリ クラス ドライバーがコピー (*ため、Battc.sys*) と新しい miniclass ドライバー (*NewBatt.sys*) で指定される宛先に、 **DestinationDirs**ディレクティブ。

``` syntax
[NewBatt_Inst]
CopyFiles = @NewBatt.sys
CopyFiles = @battc.sys
```

### <a name="span-idddinstallservicesspanspan-idddinstallservicesspanspan-idddinstallservicesspanddinstallservices"></a><span id="DDInstall.Services"></span><span id="ddinstall.services"></span><span id="DDINSTALL.SERVICES"></span>*DDInstall*します。サービス

[ **INF *DDInstall*します。サービス セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547349)が含まれています、 [ **INF AddService ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546326)バッテリ ドライバーに関する追加情報を指定します。 バッテリ ドライバーの INF ファイルは、ドライバーは、通常のエラー処理を使用して、オペレーティング システムの初期化中に開始するカーネル ドライバーであることを示す必要があります。 バッテリのドライバーでは、ロード順序グループ ベースの拡張を指定します。

``` syntax
[NewBatt_Inst.Services]
AddService = NewBatt,2,NewBatt_Service_Inst    ; function driver for the device
 
[NewBatt_Service_Inst]
DisplayName    = %NewBatt.SvcDesc%
ServiceType    = 1 ;    SERVICE_KERNEL_DRIVER
StartType      = 3 ;    SERVICE_DEMAND_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL%
ServiceBinary  = %12%\NewBatt.sys
```

 

 




