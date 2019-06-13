---
title: ユニバーサル ドライバーのシナリオ
description: 'DCHU ユニバーサル ドライバーのサンプルに、DCHU 設計原則 (Declarative: 宣言型、Componentized: コンポーネント化済み、Hardware Support Apps [HSA]: ハードウェア サポート アプリ、Universal API Compliance: ユニバーサル API 準拠) がどのように適用されているかについて説明します。'
ms.date: 04/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 55ab2413f70f424fff93a4e4967c6b1063087f4c
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63344068"
---
# <a name="universal-driver-scenarios"></a>ユニバーサル ドライバーのシナリオ

このトピックでは、[DCHU ユニバーサル ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)に DCHU [design principles](getting-started-with-universal-drivers.md) (Declarative: 宣言型、Componentized: コンポーネント化済み、Hardware Support Apps [HSA]: ハードウェア サポート アプリ、Universal API compliance) がどのように適用されているかについて説明します。  実際のユニバーサル ドライバー パッケージのモデルとして使うことができます。

サンプル リポジトリのローカル コピーが必要な場合は、[Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) から複製できます。

このサンプルは、Windows 10 バージョン 1703 以降で使うことを前提として作られています。

## <a name="prerequisites"></a>前提条件

このセクションを読む前に、「[ユニバーサル Windows ドライバーの概要](getting-started-with-universal-drivers.md)」で説明されているユニバーサル ドライバー パッケージの要件とベスト プラクティスを確認してください。

## <a name="overview"></a>概要

DCHU サンプルで提供されているシナリオ例では、2 つのハードウェア パートナー Contoso (システム ビルダーまたは OEM) と Fabrikam (デバイスの製造元または IHV) が共同で、Contoso の次期システムのデバイス用のユニバーサル Windows ドライバーを作成しています。  対象のデバイスは [OSR USB FX2 学習キット](https://store.osr.com/product/osr-usb-fx2-learning-kit-v2/)です。  これまで、Fabrikam は、特定の Contoso 製品ライン用にカスタマイズされた非ユニバーサル ドライバー パッケージを作成し、サービスを処理するために OEM に渡していました。  その結果、大きなメンテナンス オーバーヘッドが発生していたため、Fabrikam は、コードをリファクタリングして、代わりにユニバーサル ドライバー パッケージを作成することを決定しました。

## <a name="use-only-declarative-sections-and-directives"></a>宣言型セクションとディレクティブのみを使用する

最初に、Fabrikam はユニバーサル ドライバー パッケージ無効な [INF のセクションとディレクティブの一覧](../install/using-a-universal-inf-file.md#which-inf-sections-are-invalid-in-a-universal-inf-file)を確認します。  その間に、Fabrikam は無効なセクションとディレクティブの多くをドライバー パッケージで使っていることに気付きます。  

Fabrikam の非ユニバーサル ドライバーの INF は、プラットフォームに依存する設定とファイルを適用する共同インストーラーを登録します。  そのため、ドライバー パッケージが本来のサイズより大きいだけでなく、ドライバーを搭載している OEM システムの一部のみがバグの影響を受ける場合のドライバーの保守作業が困難です。  また、OEM 固有の変更のほとんどはブランドに関連するため、OEM が追加されたり、軽微な問題が OEM システムのサブセットに影響を与えたりするたびに、Fabrikam はドライバー パッケージを更新する必要があります。

Fabrikam は、非ユニバーサルのセクションとディレクティブを削除し、[InfVerif](../devtest/infverif.md) ツールを使って新しいドライバー パッケージの INF ファイルがユニバーサルであることを確認します。

## <a name="use-extension-infs-to-componentize-a-driver-package"></a>拡張 INF を使ってドライバー パッケージをコンポーネント化する

次に、Fabrikam は、OEM パートナー (Contoso など) に固有のカスタマイズを基本ドライバー パッケージから分離して、[拡張 INF](../install/using-an-extension-inf-file.md) にまとめます。

[`osrfx2_DCHU_extension.inx`  ] から更新された次のスニペットでは、`Extension` クラスが指定されており、拡張ドライバー パッケージを所有する Contoso がプロバイダーとしてを識別されます。

```cpp
[Version]
Class       = Extension
ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider    = Contoso
ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
```

[`osrfx2_DCHU_base.inx`  ] では、次のエントリが指定されています。

```cpp
[OsrUsbFx2_AddReg]
HKR, OSR, "OperatingMode",, "Default" ; FLG_ADDREG_TYPE_SZ
HKR, OSR, "OperatingParams",, "None" ; FLG_ADDREG_TYPE_SZ
```

[`osrfx2_DCHU_extension.inx`  ] で、Contoso は基本パッケージによって設定された **OperatingParams** レジストリ値をオーバーライドして、**OperatingExceptions** を追加します。

```cpp
[OsrUsbFx2Extension_AddReg]
HKR, OSR, "OperatingParams",, "-Extended"
HKR, OSR, "OperatingExceptions",, "x86" 
```

拡張機能は常に基本 INF の後に順不同で処理されることに注意してください。 基本 INF が新しいバージョンに更新された場合、拡張 INF は新しい基本 INF がインストールされた後で再適用されます。

## <a name="install-a-service-from-an-inf-file"></a>INF ファイルからサービスをインストールする

Fabrikam では、OSR ボード上の LED 制御に Win32 サービスを使用しています。 同社にとってこのコンポーネントはデバイスのコア機能の一部であるため、基本 INF ([`osrfx2_DCHU_base.inx`]) の一部として組み込みます。  このユーザーモード サービス (usersvc) は、INF ファイルに [**AddService**](../install/inf-addservice-directive.md) ディレクティブを指定して宣言することで、追加および開始できます。

```cpp
[OsrFx2_Install.NT]
CopyFiles = OsrFx2_UserSvcCopyFiles

[OsrFx2_Install.NT.Services]
AddService = osrfx2_DCHU_usersvc, 0x00000800, UserSvc_ServiceInstall
    
[UserSvc_ServiceInstall]
DisplayName = %UserSvcDisplayName%
ServiceType = 0x00000010
StartType = 3
ErrorControl = 1
ServiceBinary = %13%\osrfx2_DCHU_usersvc.exe

[OsrFx2_UserSvcCopyFiles]
osrfx2_DCHU_usersvc.exe
```
このようなサービスは、状況に応じて、コンポーネント INF または拡張 INF にもインストールできることに注意してください。

## <a name="use-a-component-to-install-legacy-software-from-a-driver-package"></a>コンポーネントを使ってドライバー パッケージからレガシ ソフトウェアをインストールする

Fabrikam は、これまで共同インストーラーを使ってインストールしていた実行可能ファイル `osrfx2_DCHU_componentsoftware.exe` を持っています。  このレガシ ソフトウェアはボードによって設定されるレジストリ キーを表示し、OEM が必要とします。  これは、デスクトップ エディションの Windows でのみ実行される GUI ベースの実行可能ファイルです。  これをインストールするため、Fabrikam は別のコンポーネント ドライバー パッケージを作成し、それを拡張 INF に追加します。

[`osrfx2_DCHU_extension.inx`  ] の次のスニペットは、[**AddComponent**](../install/inf-addcomponent-directive.md) ディレクティブを使って仮想子デバイスを作成します。

```cpp
[OsrFx2Extension_Install.NT.Components]
AddComponent = osrfx2_DCHU_component,,OsrFx2Extension_ComponentInstall


[OsrFx2Extension_ComponentInstall]
ComponentIds=VID_045e&PID_94ab
```

その後、コンポーネントの INF [`osrfx2_DCHU_component.inx`] で指定されている [**AddSoftware**](../install/inf-addsoftware-directive.md) ディレクティブによって、オプションの実行可能ファイルがインストールされます。

```cpp
[OsrFx2Component_Install.NT.Software]
AddSoftware = osrfx2_DCHU_componentsoftware,, OsrFx2Component_SoftwareInstall
    
[OsrFx2Component_SoftwareInstall]
SoftwareType = 1
SoftwareBinary = osrfx2_DCHU_componentsoftware.exe
SoftwareArguments = <<DeviceInstanceId>>
SoftwareVersion = 1.0.0.0 

[OsrFx2Component_CopyFiles]
osrfx2_DCHU_componentsoftware.exe
```

[Win32 アプリのソース コード](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_componentsoftware)は、DCHU サンプルに含まれます。

[Windows ハードウェア デベロッパー センター ダッシュボード](https://developer.microsoft.com/dashboard/Registration/Hardware)でターゲット指定が設定されているため、このコンポーネント ドライバー パッケージは デスクトップ SKU のみに配布されることに注意してください。  詳しくは、「[Windows Update にドライバーを公開する](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)」をご覧ください。

## <a name="allow-communication-with-a-hardware-support-app"></a>ハードウェア サポート アプリとの通信を許可する

Fabrikam は、ユニバーサル ドライバー パッケージの一部として GUI ベースのコンパニオン アプリを提供したいと考えています。  Win32 ベースのコンパニオン アプリケーションをユニバーサル ドライバー パッケージの一部にすることはできないため、Win32 アプリをユニバーサル Windows プラットフォーム (UWP) に移植し、[アプリをデバイスとペアリング](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-access-for-universal-windows-platform-apps)します。

[`osrfx2_DCHU_base/device.c`  ](https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_base/device.c) の次のスニペットでは、ベース ドライバー パッケージがデバイス インターフェイスのインスタンスにカスタム機能を追加する方法が示されています。

```cpp
    WDF_DEVICE_INTERFACE_PROPERTY_DATA PropertyData = { 0 };
    static const wchar_t customCapabilities[] = L"CompanyName.yourCustomCapabilityNameTBD_YourStorePubId\0";

    WDF_DEVICE_INTERFACE_PROPERTY_DATA_INIT(&PropertyData,
                                            &GUID_DEVINTERFACE_OSRUSBFX2,
                                            &DEVPKEY_DeviceInterface_UnrestrictedAppCapabilities);

    Status = WdfDeviceAssignInterfaceProperty(Device,
                                              &PropertyData,
                                              DEVPROP_TYPE_STRING_LIST,
                                              sizeof(customCapabilities),
                                              (PVOID)customCapabilities);
```

(DCHU サンプルに含まれない) 新しいアプリは、セキュリティで保護され、Microsoft Store で簡単に更新することができます。   UWP アプリケーション対応になったことで、Contoso は [DISM (展開イメージのサービスと管理)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows) を使ってアプリケーションを Windows デスクトップ エディションのイメージに事前に読み込みます。

## <a name="registering-a-com-component-in-an-inf-file"></a>INF ファイルに COM コンポーネントを登録する

Fabrikam は、共同インストーラーを使用せずに COM コンポーネントを登録する必要があります。  そこでユニバーサル INF ファイルでこれを実現するために、WDK で配布された [Reg2inf ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/reg2inf) を使用します。  同社は COM サーバー プロジェクト ([In-process ATL COM server のサンプル](https://code.msdn.microsoft.com/ATLDllCOMServer-b52a7d5d) から取得) をビルドした後、COM .dll を Reg2inf ツールへの入力として指定します。  このツールによって次の INF ディレクティブが生成され、Fabrikam はこれを基本 INF ([`osrfx2_DCHU_base.inx`]) に追加します。

```cpp
; Add all registry keys to successfully register the
; In-Process ATL COM Server MSFT Sample.
[OsrFx2_AddReg_COM]
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
```

## <a name="tightly-coupling-multiple-inf-files"></a>複数の INF ファイルを密結合する

基本パッケージ、拡張パッケージ、コンポーネント パッケージの間には、優れたバージョン管理コントラクトが存在するのが理想です。  これら 3 つのパッケージが個別にサービスを受けることには ("疎結合" のシナリオ) サービス上のメリットがありますが、シナリオによっては、バージョン管理コントラクトが不十分なために、単一のドライバー パッケージへのバンドル ("密結合") が必要な場合があります。  次のサンプルでは、両方のシナリオの例が示されています。

* [DCHU_Sample\osrfx2_DCHU_extension_loose](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_extension_loose)
* [DCHU_Sample\osrfx2_DCHU_extension_tight](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_extension_tight)
 
  拡張機能とコンポーネントが、同じドライバー パッケージにある場合 (「密結合」)、拡張 INF は [CopyINF ディレクティブ](../install/inf-copyinf-directive.md)を指定して、コンポーネント INF をターゲット システムにコピーします。  この例については、[DCHU_Sample\osrfx2_DCHU_extension_tight\osrfx2_DCHU_extension\osrfx2_DCHU_extension.inx ](https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_tight/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx) をご覧ください。

```cpp
[OsrFx2Extension_Install.NT]
CopyInf=osrfx2_DCHU_component.inf
```

このディレクティブは、多機能デバイス内での INF ファイルのインストールを調整することもできます。  詳しくは、「[Copying INF files](https://docs.microsoft.com/windows-hardware/drivers/install/copying-inf-files)」 (INF ファイルのコピー) をご覧ください。 

> [!NOTE]
> ベース ドライバーのペイロードに拡張機能を格納する (そして、配送先住所ラベルでベース ドライバーをターゲットにする) ことはできますが、別のドライバーとバンドルされている拡張機能を、拡張機能のハードウェア ID に公開することはできません。

## <a name="run-from-the-driver-store"></a>ドライバー ストアから実行する

ドライバーを容易に更新できるように、Fabrikam は、可能であれば [**dirid** 13](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids) を使って、[ドライバー ストア](../install/driver-store.md) をドライバー ファイルのコピー先として指定します。  コピー先ディレクトリの値として 13 を使うと、ドライバー更新プロセスの間の安定性が向上します。  [`osrfx2_DCHU_base.inx`  ] の例を次に示します。

```cpp
[DestinationDirs]
OsrFx2_UserSvcCopyFiles = 13 ; copy to Driver Store
```
ドライバー ストアから実行されているカーネル モード ドライバーは、[**IoQueryFullDriverPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioqueryfulldriverpath) を呼び出してそのパスを使用し、パスを基準として構成ファイルを見つけます。  カーネル モード ドライバーが KMDF ドライバーの場合、[**WdfDriverWdmGetDriverObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverwdmgetdriverobject) を使用して、IoQueryFullDriverPath に渡す WDM ドライバー オブジェクトを取得できます。 UMDF ドライバーは、[**GetModuleHandleExW**](https://docs.microsoft.com/windows/desktop/api/libloaderapi/nf-libloaderapi-getmodulehandleexw) および [**GetModuleFileNameW**](https://docs.microsoft.com/windows/desktop/api/libloaderapi/nf-libloaderapi-getmodulefilenamew) を使用してドライバーがどこから読み込まれたかを特定できます。  次に、例を示します。 

```cpp
bRet = GetModuleHandleExW(GET_MODULE_HANDLE_EX_FLAG_FROM_ADDRESS,
                         (PCWSTR)&DriverEntry,
                         &handleModule);
if (bRet) {
   winErr = GetModuleFileNameW(handleModule, 
                               path, 
                               pathLength);
     …
```

### <a name="dynamically-finding-and-loading-files-from-the-driver-store"></a>ドライバー ストアから動的にファイルを見つけて読み込む

ドライバー パッケージには、別のドライバー パッケージのバイナリまたはユーザー モード コンポーネントによって読み込まれるファイルが含まれている場合があります。

次にいくつかの例を示します。

* ユーザー モード DLL は、ドライバー パッケージ内のドライバーと通信するためのインターフェイスを提供します。
* 拡張ドライバー パッケージには、ベース ドライバー パッケージ内のドライバーによって読み込まれる構成ファイルが含まれています。

このような場合、ドライバー パッケージでは、デバイスによって開示される、ファイルのパスまたはデバイス インターフェイスを示す状態を設定する必要があります。

たとえば、ドライバー パッケージで HKR [**AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) を使用してこの状態を設定できます。 この例では、`ExampleFile.dll` について、ドライバー パッケージは *subdir* のない [**SourceDisksFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section) エントリを持つとします。  この結果、このファイルはドライバー パッケージの root に存在し、[**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive) ディレクティブの [**DestinationDirs**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section) には **dirid** 13 が指定されます。

デバイスの状態としてこれを設定する INF の例を次に示します。

```cpp
[ExampleDDInstall.HW]
AddReg = Example_DDInstall.AddReg

[Example_DDInstall.AddReg]
HKR,,ExampleValue,,%13%\ExampleFile.dll
```

デバイス インターフェイスの状態としてこれを設定する INF の例は次のようになります。 

```cpp
[ExampleDDInstall.Interfaces]
AddInterface = {<fill in an interface class GUID for an interface exposed by the device>},,Example_Add_Interface_Section

[Example_Add_Interface_Section]
AddReg = Example_Add_Interface_Section.AddReg

[Example_Add_Interface_Section.AddReg]
HKR,,ExampleValue,,%13%\ExampleFile.dll
```
上記の例では、空フラグの値が使用されているため、REG_SZ レジストリ値になります。 これにより、 **%13%** が完全修飾ユーザー モード ファイル パスに変換されます。 多くの場合、このパスは環境変数の相対パスであることが望ましいです。 フラグ値 **0x20000** を使用すると、レジストリ値はタイプ REG_EXPAND_SZ となり、 **%13%** は適切な環境変数で変換され、パスの場所が抽象化されます。 このレジストリ値を取得する場合、[**ExpandEnvironmentStrings**](https://msdn.microsoft.com/library/windows/desktop/ms724265) を呼び出して、パスの環境変数を解決します。 

カーネル モード コンポーネントによってこの値を読み取る必要がある場合、値は REG_SZ 値でなければなりません。 カーネル モード コンポーネントはこの値を読み取るときに、先頭に `\??\` を付けてから、[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenfile) などの API に渡す必要があります。 

この設定がデバイスの状態の一部である場合にアクセスするには、まずアプリケーションはデバイスの ID を検索する必要があります。  ユーザー モード コードでは、[**CM_Get_Device_ID_List_Size**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_list_sizea) および [**CM_Get_Device_ID_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_lista) を使用してデバイスの一覧 (必要に応じて、フィルタ適用) を取得できます。 このデバイスの一覧には複数のデバイスが含まれている場合があるため、デバイスから状態を読み取る前に、適切なデバイスを検索します。 たとえば、特定の条件に一致するデバイスを検索するときに、[**CM_Get_DevNode_Property**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_propertyw) を呼び出して、そのデバイスのプロパティを取得します。

適切なデバイスが見つかったら、[**CM_Open_DevNode_Key**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key) を呼び出して、デバイスの状態が格納されたレジストリの場所へのハンドルを取得します。 

カーネル モード コードでは、PDO (物理デバイス オブジェクト) を取得し、[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey) を呼び出す必要があります。 

デバイス インターフェイスの状態の場合にこの設定にアクセスするために、ユーザー モード コードで [**CM_Get_Device_Interface_List_Size**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_list_sizea) および [**CM_Get_Device_Interface_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista) を呼び出すことができます。

また、デバイス インターフェイスの接続や削除の通知を受けるために、[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification) を使用できます。これにより、コードではインターフェイスが有効化されたときに通知を受け、状態を取得できます。 上記の API で使用されるデバイス インターフェイス クラスには、複数のデバイス インターフェイスがある可能性があります。  これらのインターフェイスを確認し、設定を読み込むために適切なインターフェイスを特定します。

適切なインターフェイスが見つかったら、[**CM_Open_Device_Interface_Key**](https://msdn.microsoft.com/library/windows/hardware/hh780223(v=vs.85).aspx) を呼び出します。

カーネル モード コードでは、状態を取得するデバイス インターフェイスのシンボリック リンク名を取得できます。 そのためには、[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification) を呼び出して、適切なデバイス インターフェイス クラスでデバイス インターフェイス通知に登録します。  別の方法として、システム上の現在のデバイス インターフェイスの一覧を取得するために [**IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfaces) を呼び出すこともできます。  上記の API で使用されるデバイス インターフェイス クラスには、複数のデバイス インターフェイスがある可能性があります。  これらのインターフェイスを確認し、読み込まれる設定を持つ適切なインターフェイスを特定します。

適切なシンボリック リンク名が見つかったら、[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) を呼び出して、デバイス インターフェイスの状態が格納されたレジストリの場所へのハンドルを取得します。 

> [!NOTE]
> **CM_GETIDLIST_FILTER_PRESENT** フラグと [CM_Get_Device_ID_List_Size](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_list_sizea) および [**CM_Get_Device_ID_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_lista) を使用するか、**CM_GET_DEVICE_INTERFACE_LIST_PRESENT** フラグと [**CM_Get_Device_Interface_List_Size**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_list_sizew) および [**CM_Get_Device_Interface_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista) を使用します。 これにより、ハードウェアが存在し、通信の準備ができていることを確認します。 

## <a name="summary"></a>概要

次の図は、Fabrikam と Contoso がユニバーサル Windows ドライバー用に作成したドライバー パッケージを示したものです。  疎結合の例では、[Windows ハードウェア デベロッパー センター ダッシュボード](https://developer.microsoft.com/dashboard/Registration/Hardware)で、基本パッケージ、拡張パッケージ、コンポーネントパッケージの 3 回にわたってパッケージが別個に提出されます。  密結合の例では、基本パッケージと拡張/コンポーネント パッケージの 2 つが提出されます。

![拡張、基本、コンポーネントの各ドライバー パッケージ](images/universal-scenarios.png)

コンポーネント INF はコンポーネント ハードウェア ID に一致し、基本 INF と拡張 INF はボードのハードウェア ID に一致することに注意してください。

## <a name="see-also"></a>関連項目

[ユニバーサル Windows ドライバーの概要](getting-started-with-universal-drivers.md)

[拡張 INF ファイルの使用](../install/using-an-extension-inf-file.md)

[`osrfx2_DCHU_base.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_base/osrfx2_DCHU_base.inx
[`osrfx2_DCHU_usersvc.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_usersvc/osrfx2_DCHU_usersvc.inx
[`osrfx2_DCHU_component.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_component/osrfx2_DCHU_component.inx
[`osrfx2_DCHU_extension.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx
