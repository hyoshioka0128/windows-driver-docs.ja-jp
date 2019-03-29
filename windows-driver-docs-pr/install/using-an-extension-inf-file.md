---
title: 拡張 INF ファイルの使用
description: Windows 10 以降できます機能を拡張するドライバー パッケージ INF ファイルの拡張子 INF と呼ばれる追加の INF ファイルを提供することで。
ms.assetid: 124C4E58-7F06-46F5-B530-29A03FA75C0A
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: aecaba727d928106b0a1dfc642b01f61e59485ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580722"
---
# <a name="using-an-extension-inf-file"></a>拡張 INF ファイルの使用

Windows 10 では、以前は、Windows は、特定のデバイスをインストールする 1 つのドライバー パッケージを選択します。  結果として、大規模で複雑なドライバー パッケージのすべてのシナリオと構成をコードに含まれてし、必要なドライバー パッケージ全体の更新プログラムを各マイナー更新します。  Windows 10 以降、それぞれが処理されていない独立して、複数のコンポーネントに INF 機能を分割できます。  ドライバー パッケージの INF ファイルの機能を拡張するには、個別のドライバー パッケージに拡張子 INF を提供します。  INF 拡張子:

* 別の会社によって提供され、基本の INF から独立して更新できます。
* 基本 INF と同じに見えますが、カスタマイズまたは特殊化の基本 INF を拡張することができます。
* デバイスの価値を向上しますが、ベースのドライバーが動作する必要はありません。
* 必要があります、[ユニバーサル INF ファイル](../install/using-a-universal-inf-file.md)します。

すべてのデバイスでは、1 つの基本 INF があり、必要に応じて、1 つまたは複数の拡張子 Inf を関連付けられています。

拡張子 INF を使う場合の一般的なシナリオは次のとおりです。

* デバイスのフレンドリ名をカスタマイズまたはハードウェア構成の設定を変更するなどの基本 INF で提供された設定を変更します。
* 指定することで 1 つまたは複数のソフトウェア コンポーネントの作成、 [INF AddComponent ディレクティブ](inf-addcomponent-directive.md)を提供して、[コンポーネント INF ファイル](using-a-component-inf-file.md)します。

このページでは、以下の例では、これらシナリオのサンプル コードが表示されます。  参照してください[ユニバーサル ドライバー シナリオ](../develop/universal-driver-scenarios.md)、について説明する方法、 [DCHU ユニバーサル ドライバー サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)拡張子 Inf を使用して。

次の図では、2 つの会社は点線で示されている、同じデバイスの個別のドライバー パッケージを作成しました。  最初には、INF、拡張機能だけが含まれています。 と 2 番目にはコンポーネントの INF と従来のソフトウェア モジュールが含まれています。  図には、拡張子 INF が有効にする参照ソフトウェア モジュールをインストールするにはコンポーネント INF を参照する方法も示します。

![拡張機能とコンポーネント INF の階層構造](images/extension-component-inf-hierarchy.png)

## <a name="how-extension-inf-and-base-inf-work-together"></a>拡張子 INF ベース INF 連携させる方法

基本 INF で設定した後、拡張子 INF の設定が適用されます。 結果として、拡張子 INF と基本 INF は、同じ設定を指定して、拡張子 INF のバージョンに適用されます。 同様に、基本の INF を変更する場合、拡張子 INF ままになり、新しい基本 INF に適用します。

## <a name="specifying-extensionid"></a>ExtensionId を指定します。

呼ばれる特殊な GUID を生成する拡張子 INF を記述するときに、 **ExtensionId**、INF の内のエントリは**\[バージョン\]** セクション。

システム ハードウェア ID およびに拡張子 INF で指定されているデバイスの互換性 Id を照合して、特定のデバイスの可能な拡張子 Inf を識別する、 [**モデル**](inf-models-section.md)セクションに適用されます。そのシステム。

すべての可能な拡張機能、同じを指定する Inf の間で**ExtensionId**値、システムをインストールする 1 つだけを選択し、基本の INF の経由でその設定を適用します。  ドライバーの日付と、INF で指定されたドライバーのバージョンを使用して、順番に同じ複数の拡張子 Inf の間で 1 つの INF を選択**ExtensionId**します。

を示すためには、次の 3 つの拡張子 Inf しているすべての仮想デバイスを含む次のシナリオを検討してください。

![ダイアグラムの表示方法の基本 INF と拡張子 Inf を選択します。](images/extension-base-inf-example.png)

**ExtensionId**に中かっこ、および各ドライバーの値が表示[ランク](how-setup-ranks-drivers--windows-vista-and-later-.md)バナーのリボンに表示されます。

最初に、システムは、最新バージョンおよび最高ランクのドライバーを選択します。

次に、システムは、使用可能な拡張子 Inf を処理します。  2 つが**ExtensionId**値`{B}`、いずれかが**ExtensionId**値`{A}`します。  最初の 2 つからとドライバーの日付が同じであります。  次の条件はドライバーのバージョンは、システムが v2.0 に拡張子 INF を選択します。

一意に拡張子 INF **ExtensionId**値が選択されていることもできます。  システムは、デバイスの基本 INF を適用し、そのデバイスの 2 つの拡張子 Inf を適用します。

基本の INF の後に拡張子 INF ファイルが常に適用されているが、拡張子 Inf を適用する特定の順序がないことに注意してください。

## <a name="creating-an-extension-inf"></a>拡張子 INF を作成します。

INF の拡張機能として、INF を定義する必要があるエントリを次に示します。

1.  これらの値を指定**クラス**と**ClassGuid**で、 [**バージョン**](inf-version-section.md)セクション。 セットアップ クラスの詳細については、次を参照してください。[ベンダー デバイス セットアップ クラスできるベンダー](https://msdn.microsoft.com/library/windows/hardware/ff553426)します。

    ```cpp
    [Version]
    ...
    Class       = Extension
    ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
    ```

2.  提供、 **ExtensionId**内のエントリ、 [ **\[バージョン\]** ](inf-version-section.md)セクション。 初期拡張子 INF の後続の更新プログラムの最後の GUID を再利用または INF、拡張機能の初期バージョンの新しい GUID を生成します。

    ```cpp
    ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
    ```

組織でのみ使用できますが、 **ExtensionID**所有します。  拡張機能 ID を登録する方法の詳細については、次を参照してください。 [Windows ハードウェア デベロッパー センター ダッシュ ボードでのハードウェアの提出を管理する](../dashboard/manage-your-hardware-submissions.md)します。     

3.  拡張子 INF を更新する場合は、保持、 **ExtensionId**同じで、バージョン、または日付 (またはその両方) を指定のインクリメント、 [ **DriverVer** ](inf-driverver-directive.md)ディレクティブ。 指定された**ExtensionId**値には、PnP 選択最高 INF **DriverVer**。

4.  [ **INF モデル セクション**](inf-models-section.md)、1 つまたは複数のハードウェアとターゲット デバイスのものと一致する互換性 Id を指定します。  これらのハードウェアと互換性のある Id が行う基本 INF のものと一致する必要がないことに注意してください。  通常、INF の拡張機能では、特定のドライバーの構成をさらに専門の目的で、基本の INF よりもより特定のハードウェア ID が一覧表示します。  たとえば、基本 INF は 2 つの部分の PCI ハードウェア ID を使用可能性がありますに拡張子 INF を次のように、4 部構成の PCI ハードウェア ID を指定します。
    
    ```cpp
    [DeviceExtensions.NTamd64]
    %Device.ExtensionDesc% = DeviceExtension_Install, PCI\VEN_XXXX&DEV_XXXX&SUBSYS_XXXXXXXX&REV_XXXX
    ```

    または、拡張子 INF が基本の INF と同じハードウェア ID をインスタンスのリスト、デバイスが既に非常に限定対象となるか、基本 INF が既に特定のハードウェア ID を一覧表示
    
    場合によっては、拡張子 INF 可能性がありますより広範な一連のデバイス間での設定をカスタマイズするにはより一般的なデバイス ID、互換性 ID などを提供します。

5.  使用済みのサービスを定義しない`SPSVCINST_ASSOCSERVICE`します。  ただし、INF の拡張機能では、デバイスのフィルター ドライバーなどの他のサービスを定義できます。  サービスを指定する方法の詳細については、次を参照してください。 [ **INF AddService ディレクティブ**](inf-addservice-directive.md)します。

ほとんどの場合に提出する INF 拡張機能パッケージ ハードウェア デベロッパー センターとは別にドライバー パッケージから。  パッケージの拡張機能、Inf とサンプル コードへのリンクの例についてを参照してください。[ユニバーサル ドライバー シナリオ](../develop/universal-driver-scenarios.md)します。

ドライバーの検証と送信のプロセスは、拡張機能と正規表現の Inf Inf のと同じです。 詳細については、次を参照してください。 [Windows HLK Getting Started](https://msdn.microsoft.com/library/windows/hardware/dn915002)します。

## <a name="uninstalling-an-extension-driver"></a>拡張機能、ドライバーのアンインストール

拡張機能ドライバーをアンインストールする前に、ベースのデバイスをアンインストールする必要があります。  次に、拡張子 INF を pnputil ツールを実行します。

ドライバー パッケージを削除する使用`pnputil /delete-driver oem0.inf`します。
強制的にドライバー パッケージを削除を使用して、`pnputil /delete-driver oem1.inf /force`します。

## <a name="example-1-using-an-extension-inf-to-set-the-device-friendly-name"></a>例 1:拡張子 INF を使用して、デバイスのフレンドリ名を設定するには

1 つの一般的なシナリオで基本のドライバーと基本 INF では、デバイスの製造元 (IHV) が提供と、システム ビルダー (OEM) 拡張子 INF を補足するものし、場合によっては、構成と基本 INF の設定の上書きを示します。  次のスニペットは、完全な拡張子 INF をデバイスのフレンドリ名を設定する方法を示します。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = Extension
ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider    = %CONTOSO%
ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
DriverVer   = 05/28/2013,1.0.0.0
CatalogFile = delta.cat

[Manufacturer]
%CONTOSO% = DeviceExtensions,NTamd64

[DeviceExtensions.NTamd64]
%Device.ExtensionDesc% = DeviceExtension_Install, PCI\VEN_XXXX&DEV_XXXX&SUBSYS_XXXXXXXX&REV_XXXX

[DeviceExtension_Install]
; No changes

[DeviceExtension_Install.HW]
AddReg = FriendlyName_AddReg

[FriendlyName_AddReg]
HKR,,FriendlyName,, "New Device Friendly Name"

[Strings]
CONTOSO              = "Contoso"
Device.ExtensionDesc = "Sample Device Extension"
```

## <a name="example-2-using-an-extension-inf-to-install-additional-software"></a>例 2:拡張子 INF を使用して、追加のソフトウェアをインストールするには

次のスニペットは、完全な拡張子 INF に含まれている、[ユニバーサル ドライバーのドライバー パッケージのインストール ツールキット](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)します。  この例では[INF AddComponent ディレクティブ](inf-addcomponent-directive.md)サービスおよび実行可能ファイルをインストールするコンポーネントを作成します。  コンポーネントの INF で実行できる操作についての詳細については、次を参照してください。[コンポーネントの INF ファイルを使用して](using-a-component-inf-file.md)します。

このファイルをオンラインにアクセスするを参照してください。 [ `osrfx2_DCHU_extension.inx`](https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx)します。

```cpp
;/*++
;
;Copyright (c) Microsoft Corporation.  All rights reserved.
;
;   THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY
;   KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE
;   IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR
;   PURPOSE.
;
;Module Name:
;
;    osrfx2_DCHU_extension.INF
;
;Abstract:
;
;    Extension inf for the OSR FX2 Learning Kit
;
;--*/

[Version]
Signature = "$WINDOWS NT$"
Class = Extension
ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider = %ManufacturerName%
ExtensionId = {3846ad8c-dd27-433d-ab89-453654cd542a}
CatalogFile = osrfx2_DCHU_extension.cat
DriverVer = 05/16/2017,15.14.36.721

[Manufacturer]
%ManufacturerName% = OsrFx2Extension, NT$ARCH$

[OsrFx2Extension.NT$ARCH$]
%OsrFx2.ExtensionDesc% = OsrFx2Extension_Install, USB\Vid_045e&Pid_94aa&mi_00
%OsrFx2.ExtensionDesc% = OsrFx2Extension_Install, USB\Vid_0547&PID_1002

[OsrFx2Extension_Install.NT]
CopyInf=osrfx2_DCHU_usersvc.inf

[OsrFx2Extension_Install.NT.HW]
AddReg = OsrFx2Extension_AddReg
AddReg = OsrFx2Extension_COMAddReg

[OsrFx2Extension_AddReg]
HKR, OSR, "OperatingParams",, "-Extended"
HKR, OSR, "OperatingExceptions",, "x86"

; Add all registry keys to successfully register the
; In-Process ATL COM Server MSFT Sample.
[OsrFx2Extension_COMAddReg]
HKCR,AppID\ATLDllCOMServer.DLL,AppID,,"{9DD18FED-55F6-4741-AF25-798B90C4AED5}"
HKCR,AppID\{9DD18FED-55F6-4741-AF25-798B90C4AED5},,,"ATLDllCOMServer"
HKCR,ATLDllCOMServer.SimpleObject,,,"SimpleObject Class"
HKCR,ATLDllCOMServer.SimpleObject\CLSID,,,"{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}"
HKCR,ATLDllCOMServer.SimpleObject\CurVer,,,"ATLDllCOMServer.SimpleObject.1"
HKCR,ATLDllCOMServer.SimpleObject.1,,,"SimpleObject Class"
HKCR,ATLDllCOMServer.SimpleObject.1\CLSID,,,"{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084},,,"SimpleObject Class"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,,%REG_EXPAND_SZ%,"%%SystemRoot%%\System32\ATLDllCOMServer.dll"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,ThreadingModel,,"Apartment"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\ProgID,,,"ATLDllCOMServer.SimpleObject.1"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\Programmable,,%FLG_ADDREG_KEYONLY%
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\TypeLib,,,"{9B23EFED-A0C1-46B6-A903-218206447F3E}"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\VersionIndependentProgID,,,"ATLDllCOMServer.SimpleObject"

[OsrFx2Extension_Install.NT.Components]
AddComponent = osrfx2_DCHU_component,,OsrFx2Extension_ComponentInstall
AddComponent = osrfx2_DCHU_usersvc,,OsrFx2Extension_ComponentInstall_UserSvc

[OsrFx2Extension_ComponentInstall]
ComponentIds=VID_045e&PID_94ab

[OsrFx2Extension_ComponentInstall_UserSvc]
ComponentIds=VID_045e&PID_94ac

[Strings]
ManufacturerName = "Contoso"
OsrFx2.ExtensionDesc = "OsrFx2 DCHU Device Extension"
REG_EXPAND_SZ = 0x00020000
FLG_ADDREG_KEYONLY = 0x00000010
```

## <a name="example-3-using-an-extension-inf-to-install-a-filter-driver"></a>例 3: 拡張子 INF を使用して、フィルター ドライバーをインストールするには

システム提供のデバイス ドライバーを使用するデバイスのフィルター ドライバーをインストールするのに拡張子 INF を使用することもできます。 INF 拡張子は、デバイスのハードウェア ID を指定し、サービスとフィルター ドライバーの設定を提供します。

次のコード スニペットでは、拡張子 INF を使用して、フィルター ドライバーをインストールする方法を示します。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = Extension
ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider    = %CONTOSO%
ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
DriverVer   = 05/28/2013,1.0.0.0
CatalogFile = delta.cat

[Manufacturer]
%CONTOSO% = DeviceExtensions,NTx86

[DeviceExtensions.NTx86]
%Device.ExtensionDesc% = DeviceExtension_Install,PCI\VEN_XXXX&DEV_XXXX&SUBSYS_XXXXXXXX&REV_XXXX

[DeviceExtension_Install]
CopyFiles = Filter_CopyFiles

[DeviceExtension_Install.HW]
AddReg = DeviceExtensionFilter_AddReg

[DeviceExtensionFilter_AddReg]
HKR,,"UpperFilters",0x00010008,"fltsample" 

[DeviceExtension_Install.Services]
AddService = fltsample,,FilterService_Install

[FilterService_Install]
DisplayName   = %FilterSample.ServiceDesc%
ServiceType   = 1   ; SERVICE_KERNEL_DRIVER
StartType     = 3   ; SERVICE_DEMAND_START
ErrorControl  = 1   ; SERVICE_ERROR_NORMAL
ServiceBinary = %12%\fltsample.sys

[Filter_CopyFiles]
fltsample.sys

[SourceDisksFiles]
fltsample.sys = 1

[SourceDisksNames]
1 = Disk

[DestinationDirs]
Filter_CopyFiles = 12

[Strings]
CONTOSO                  = "Contoso"
Device.ExtensionDesc     = "Sample Extension Device"
FilterSample.ServiceDesc = "Sample Upper Filter"
```

##  <a name="submitting-an-extension-inf-for-certification"></a>証明書の拡張子 INF を送信します。

ハードウェア デベロッパー センターに拡張子 Inf を使用する方法の詳細についてを参照してください[Windows ハードウェア デベロッパー センター ダッシュ ボードに拡張子 Inf を扱う](../dashboard/submit-dashboard-extension-inf-files.md)します。

## <a name="related-topics"></a>関連トピック

* [ユニバーサル ドライバーのシナリオ](../develop/universal-driver-scenarios.md)
* [ユニバーサル INF ファイルの使用](using-a-universal-inf-file.md)
* [ユニバーサル ドライバーの概要](../develop/getting-started-with-universal-drivers.md)
* [ユニバーサル ドライバーのドライバー パッケージのインストール ツールキット](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)
