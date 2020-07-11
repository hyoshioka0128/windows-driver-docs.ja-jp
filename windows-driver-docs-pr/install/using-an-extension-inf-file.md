---
title: 拡張 INF ファイルの使用
description: Windows 10 以降では、拡張機能 INF と呼ばれる追加の INF ファイルを提供して、ドライバーパッケージの INF ファイルの機能を拡張できます。
ms.assetid: 124C4E58-7F06-46F5-B530-29A03FA75C0A
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: d354ee7facb4b3d09addfc1812a8f54afc4b087e
ms.sourcegitcommit: 5148f4ff682a2d9cdf5eafdb76e13400331f5660
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2020
ms.locfileid: "86272975"
---
# <a name="using-an-extension-inf-file"></a>拡張 INF ファイルの使用

Windows 10 より前の Windows では、特定のデバイスにインストールするドライバーパッケージが1つだけ選択されていました。  この結果、すべてのシナリオと構成のコードを含む大規模で複雑なドライバーパッケージが生成され、各マイナー更新でドライバーパッケージ全体を更新する必要がありました。  Windows 10 以降では、INF 機能を複数のコンポーネントに分割することができ、それぞれを個別に処理することができます。

ドライバーパッケージの INF ファイルの機能を拡張するには、別のドライバーパッケージに拡張機能の INF を提供します。  拡張機能の INF:

* は、別の会社によって提供され、ベース INF から独立して更新できます。
* は基本 INF と同じように見えますが、カスタマイズまたは特殊化のためにベース INF を拡張できます。
* はデバイスの値を拡張しますが、基本ドライバーが動作するためには必要ありません。
* は、[ユニバーサル INF ファイル](../install/using-a-universal-inf-file.md)である必要があります。

すべてのデバイスは1つのベース INF を持つ必要があり、必要に応じて1つまたは複数の拡張機能の Inf を関連付けることができます。

拡張機能の INF を使用する一般的なシナリオは次のとおりです。

* デバイスのフレンドリ名をカスタマイズしたり、ハードウェア構成設定を変更したりするなど、基本 INF に用意されている設定を変更する。
* [Inf AddComponent ディレクティブ](inf-addcomponent-directive.md)を指定し、[コンポーネントの inf ファイル](using-a-component-inf-file.md)を指定して、1つまたは複数のソフトウェアコンポーネントを作成します。

これらのシナリオのサンプルコードについては、以下の例を参照してください。  [Dch の汎用ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)で拡張機能の inf を使用する方法については、「 [Dch 準拠のドライバーパッケージの例](../develop/dch-example.md)」も参照してください。

次の図では、2つの異なる企業が同じデバイス用に個別のドライバーパッケージを作成しています。これらは点線で示されています。  最初のは拡張機能の INF のみを含み、2つ目の要素にはコンポーネント INF とレガシソフトウェアモジュールが含まれています。  また、この図は、拡張機能の INF がコンポーネント INF を参照する方法も示しています。これは、ソフトウェアモジュールを参照してインストールすることができます。

![拡張機能とコンポーネントの INF 階層](images/extension-component-inf-hierarchy.png)

## <a name="how-extension-inf-and-base-inf-work-together"></a>拡張機能 INF とベース INF の連携のしくみ

拡張機能 INF の設定は、基本 INF の設定後に適用されます。 その結果、拡張機能の INF とベース INF で同じ設定が指定されている場合、拡張機能 INF のバージョンが適用されます。 同様に、ベース INF が変更された場合、拡張機能の INF はそのままで、新しい基本 INF に適用されます。

上書きできるエントリと、適用可能なパラメーター値の範囲および制約を記述するコメントをベース INF に含めると便利です。

## <a name="specifying-extensionid"></a>ExtensionId の指定

拡張機能の INF を記述するときに、 **Extensionid**と呼ばれる特殊な GUID を生成します。これは、inf の** \[ Version \] **セクションのエントリです。

システムは、デバイスのハードウェア ID と互換性のある Id を、そのシステムに適用される[**モデル**](inf-models-section.md)セクションの拡張機能の INF に指定されているものと照合することで、特定のデバイスで使用可能な拡張機能の inf を識別します。

同じ**Extensionid**値を指定するすべての拡張機能の inf の中で、システムは1つだけを選択して、基本 INF の設定をインストールし、その設定を適用します。  INF に指定されているドライバーの日付とドライバーのバージョンをこの順序で使用して、同じ**Extensionid**を持つ複数の拡張機能の inf 間で単一の inf を選択します。

例として、次のようなシナリオでは、3つの拡張機能の Inf がある仮定のデバイスが含まれています。

![基本 INF と拡張機能の Inf を選択する方法を示す図](images/extension-base-inf-example.png)

**Extensionid**値 `{A}` 、 `{B}` 、および `{C}` は中かっこで示され、各ドライバーの[ランク](how-setup-ranks-drivers--windows-vista-and-later-.md)はバナーリボンに表示されます。

最初に、システムは最新のバージョンとランクが最も高いドライバーを選択します。

次に、使用可能な拡張機能の Inf がシステムによって処理されます。  2つは**Extensionid**値を持ち、 `{B}` 1 つは**extensionid**値を持ち `{A}` ます。  最初の2つは、ドライバーの日付が同じであるとします。  次の tiebreaker はドライバーのバージョンであるため、システムは v2.0 を使用して拡張機能の INF を選択します。

[固有の**Extensionid**値を持つ拡張機能 INF も選択されます。  システムによってデバイスのベース INF が適用され、そのデバイスの2つの拡張 Inf が適用されます。

拡張機能の INF ファイルは常にベース INF の後に適用されますが、拡張機能の inf が適用される順序は決まっていないことに注意してください。

## <a name="creating-an-extension-inf"></a>拡張機能の INF を作成する

INF を拡張機能の INF として定義するために必要なエントリを次に示します。

1.  [[**バージョン**](inf-version-section.md)] セクションで**クラス**および**classguid**にこれらの値を指定します。 セットアップクラスの詳細については、「[ベンダーが使用できるシステム定義のデバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/system-defined-device-setup-classes-available-to-vendors)」を参照してください。

    ```cpp
    [Version]
    ...
    Class       = Extension
    ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
    ```

2.  [ [** \[ バージョン \] **](inf-version-section.md) ] セクションに**extensionid**エントリを入力します。 拡張機能の初期バージョンの新しい GUID を生成するか、最初の拡張機能の INF の後続の更新に対して最後の GUID を再利用します。

    ```cpp
    ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
    ```

組織が所有する**Extensionid**のみを使用できることに注意してください。  拡張機能 ID の登録については、「 [Windows Hardware デベロッパーセンターダッシュボードでのハードウェアの送信の管理](../dashboard/manage-your-hardware-submissions.md)」を参照してください。     

3.  拡張機能の INF を更新する場合は、 **Extensionid**を同じにし、 [**DriverVer**](inf-driverver-directive.md)ディレクティブで指定されたバージョンまたは日付 (またはその両方) をインクリメントします。 指定された**Extensionid**値に対して、PnP は**DriverVer**が最も高い INF を選択します。

>[!NOTE]
> 拡張機能の INF が Windows 10 S を対象としている場合は、そのバージョンの Windows でのドライバーのインストールに関する情報について、「 [windows 10 In S モードドライバーの要件](https://docs.microsoft.com/windows-hardware/drivers/install/windows10sdriverrequirements)」を参照してください。

4.  [ [**INF モデル] セクション**](inf-models-section.md)で、ターゲットデバイスのハードウェア id と互換性のある id を1つ以上指定します。  これらのハードウェアおよび互換性のある Id は、ベース INF のものと一致する必要がないことに注意してください。  通常、拡張機能の INF には、特定のドライバー構成をさらに特殊化することを目的とした、基本 INF よりも具体的なハードウェア ID が一覧表示されます。  たとえば、ベース INF は2つの部分で構成される PCI ハードウェア ID を使用しますが、拡張機能の INF は次のように4つの部分で構成される PCI ハードウェア ID を指定します。
    
    ```cpp
    [DeviceExtensions.NTamd64]
    %Device.ExtensionDesc% = DeviceExtension_Install, PCI\VEN_XXXX&DEV_XXXX&SUBSYS_XXXXXXXX&REV_XXXX
    ```

    または、拡張機能の INF によって、ベース INF と同じハードウェア ID が一覧表示される場合があります。たとえば、デバイスの対象が既に狭い場合や、ベース INF に特定のハードウェア ID が既に含まれている場合などです。
    
    場合によっては、拡張機能の INF では、より多くのデバイスで設定をカスタマイズするために、互換性のある ID のような特定のデバイス ID が提供されることがあります。

    [Chid ターゲット](https://docs.microsoft.com/windows-hardware/drivers/bringup/target-a-system-using-chid)は、4つの部分で構成されるハードウェア ID が使用できない場合、または制限が不十分な場合に使用できます。

5.  でサービスを定義しないで `SPSVCINST_ASSOCSERVICE` ください。  ただし、拡張機能の INF では、デバイスのフィルタードライバーなど、他のサービスを定義できます。  サービスの指定の詳細については、「 [**INF AddService ディレクティブ**](inf-addservice-directive.md)」を参照してください。

ほとんどの場合、基本ドライバーパッケージとは別に、拡張機能の INF パッケージをハードウェアデベロッパーセンターに送信します。  拡張機能の Inf のパッケージ化方法の例と、サンプルコードへのリンクについては、「 [Dch 準拠のドライバーパッケージの例](../develop/dch-example.md)」を参照してください。

ドライバーの検証と送信のプロセスは、通常の Inf と同様に拡張機能の Inf と同じです。 詳細については、「 [WINDOWS HLK はじめに](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)」を参照してください。

## <a name="uninstalling-an-extension-driver"></a>拡張機能ドライバーのアンインストール

拡張機能ドライバーをアンインストールする前に、まず基本デバイスをアンインストールする必要があります。  次に、拡張機能の INF で [PnPUtil] を実行します。

ドライバーパッケージを削除するには、を使用 `pnputil /delete-driver oem0.inf` します。
ドライバーパッケージを強制的に削除するには、を使用し `pnputil /delete-driver oem1.inf /force` ます。

## <a name="example-1-using-an-extension-inf-to-set-the-device-friendly-name"></a>例 1: 拡張機能の INF を使用してデバイスのフレンドリ名を設定する

1つの一般的なシナリオでは、デバイスの製造元 (IHV) によって基本ドライバーとベース INF が提供されます。その後、システムビルダー (OEM) は、を補完する拡張機能の INF を提供し、場合によってはベース INF の構成と設定を上書きします。  次のスニペットは、デバイスのフレンドリ名を設定する方法を示す完全な拡張機能の INF です。

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

## <a name="example-2-using-an-extension-inf-to-install-additional-software"></a>例 2: 拡張機能 INF を使用して追加のソフトウェアをインストールする

次のスニペットは、[汎用ドライバーのドライバーパッケージインストールツールキット](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)に含まれている完全な拡張機能の INF です。  この例では、 [INF AddComponent ディレクティブ](inf-addcomponent-directive.md)を使用して、サービスと実行可能ファイルをインストールするコンポーネントを作成します。  コンポーネント INF で実行できる操作の詳細については、「[コンポーネント Inf ファイルの使用](using-a-component-inf-file.md)」を参照してください。

オンラインでこのファイルにアクセスするには、「」を参照してください [`osrfx2_DCHU_extension.inx`](https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx) 。

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
拡張機能 INF を使用してフィルタードライバーをインストールする方法の詳細については、「[デバイスフィルタードライバーの順序](https://docs.microsoft.com/windows-hardware/drivers/develop/device-filter-driver-ordering)」を参照してください。

拡張機能を向上させるには、IHV が拡張機能の[INF テンプレート](using-an-extension-inf-file-template.md)にオプション機能を配置することをお勧めします。

## <a name="backward-compatibility"></a>下位互換性

ベース INF に対する変更は、既存の拡張機能の Inf の旧バージョンとの互換性が損なわれないように十分にテストする必要があります。

基本 INF を管理する場合は、次のベストプラクティスに従ってください。

* コードコメントとデザインドキュメントの両方で、ドキュメントパラメーター値の範囲と制約の両方を指定します。 今後の変更は、指定された範囲に従っている必要があります。
* 新しい範囲をサポートするには、省略可能なパラメーターを追加します (既定値はありません)。

IHV がすべての機能をベース INF に配置する場合、既存の拡張機能の Inf が引き続き動作するようにする方法の1つを次に示します。

1. IHV には、既定でオプション機能を無効にするためのレジストリフラグを設定するコンパニオンアプリが用意されています。
2. 基本ドライバーは、オプションの機能を使用する前に、フラグが有効になっているかどうかを確認します。
3. OEM が提供する拡張機能の INF では、フラグを [有効] に設定することによってオプトインできます。

##  <a name="submitting-an-extension-inf-for-certification"></a>認定のために拡張機能の INF を送信する

ハードウェアデベロッパーセンターで拡張機能の Inf を操作する方法の詳細については、 [Windows Hardware デベロッパーセンターのダッシュボードの「拡張機能](../dashboard/submit-dashboard-extension-inf-files.md)の使用」を参照してください。

## <a name="related-topics"></a>関連トピック

* [パートナー センターでの拡張 INF の使用](../dashboard/submit-dashboard-extension-inf-files.md)
* [DCH 準拠のドライバー パッケージの例](../develop/dch-example.md)
* [ユニバーサル INF ファイルの使用](using-a-universal-inf-file.md)
* [Windows ドライバーの概要](../develop/getting-started-with-windows-drivers.md)
* [ユニバーサルドライバー用ドライバーパッケージインストールツールキット](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)
