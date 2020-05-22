---
title: DCH の例
description: 'DCHU ドライバーのサンプルで、DCH 設計原則 (Declarative: 宣言型、Componentized: コンポーネント化済み、Hardware Support Apps [HSA]: ハードウェア サポート アプリ) がどのように適用されるかについて説明します。'
ms.assetid: f46f0ea6-d855-49d2-8c09-a6ad56084742
ms.date: 04/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: d0894525905e2ecbf5fc3e635a17350fbb91b48e
ms.sourcegitcommit: 4d1ed685d198629f792d287619621a87ca42c26f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435380"
---
# <a name="dch-compliant-driver-package-example"></a>DCH 準拠のドライバー パッケージの例

このトピックでは、[DCHU ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)で [DCH 設計原則](dch-principles-best-practices.md)がどのように適用されるのかについて説明します。  これをモデルとして使用し、ご自分のドライバー パッケージに DCH 設計原則を適用できます。  

サンプル リポジトリのローカル コピーが必要な場合は、[Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) から複製できます。

このサンプルの一部では、特定のバージョンの Windows 10 以降でのみ使用できるディレクティブと API を使用する場合があります。  特定のディレクティブがサポートされている OS バージョンを確認するには、「[INF のディレクティブ](../install/inf-directives.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

このセクションを読む前に、[DCH 設計原則](dch-principles-best-practices.md)を理解しておく必要があります。

## <a name="overview"></a>概要

サンプルで提供されているシナリオ例では、2 つのハードウェア パートナー Contoso (システム ビルダーまたは OEM) と Fabrikam (デバイスの製造元または IHV) が共同で、Contoso の次期システムのデバイス向け DCH 準拠ドライバーを作成しています。  対象のデバイスは [OSR USB FX2 学習キット](https://go.microsoft.com/fwlink/p/?linkid=2113717)です。  これまで、Fabrikam は、特定の Contoso 製品ライン用にカスタマイズされたレガシ ドライバー パッケージを作成し、サービスを処理するために OEM に渡していました。  その結果、大きなメンテナンス オーバーヘッドが発生していたため、Fabrikam は、コードをリファクタリングして、代わりに DCH 準拠ドライバー パッケージを作成することを決定しました。

## <a name="use-declarative-sectionsdirectives-and-properly-isolate-inf"></a>宣言型セクションおよびディレクティブを使用して INF を適切に分離する

最初に、Fabrikam は DCH 準拠ドライバー パッケージで無効な [INF のセクションとディレクティブの一覧](../install/using-a-universal-inf-file.md#which-inf-sections-are-invalid-in-a-universal-inf-file)を確認します。  その間に、Fabrikam は無効なセクションとディレクティブの多くをドライバー パッケージで使っていることに気付きます。  

Fabrikam のドライバーの INF は、プラットフォームに依存する設定とファイルを適用する共同インストーラーを登録します。  そのため、ドライバー パッケージが本来のサイズより大きいだけでなく、ドライバーを搭載している OEM システムの一部のみがバグの影響を受ける場合のドライバーの保守作業が困難です。  また、OEM 固有の変更のほとんどはブランドに関連するため、OEM が追加されたり、軽微な問題が OEM システムのサブセットに影響を与えたりするたびに、Fabrikam はドライバー パッケージを更新する必要があります。

Fabrikam は、非宣言型セクションとディレクティブを削除し、[InfVerif](../devtest/infverif.md) ツールを使って新しいドライバー パッケージの INF ファイルが宣言型 INF の要件に従っていることを確認します。

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
[OsrFx2_AddReg]
HKR, OSR, "OperatingMode",, "Default" ; FLG_ADDREG_TYPE_SZ
HKR, OSR, "OperatingParams",, "None" ; FLG_ADDREG_TYPE_SZ
```

[`osrfx2_DCHU_extension.inx`  ] で、Contoso は基本パッケージによって設定された **OperatingParams** レジストリ値をオーバーライドして、**OperatingExceptions** を追加します。

```cpp
[OsrFx2Extension_AddReg]
HKR, OSR, "OperatingParams",, "-Extended"
HKR, OSR, "OperatingExceptions",, "x86"
```

拡張機能は常に基本 INF の後に、しかし順不同で処理されることに注意してください。 基本 INF が新しいバージョンに更新された場合、拡張 INF は新しい基本 INF がインストールされた後で再適用されます。

## <a name="install-a-service-from-an-inf-file"></a>INF ファイルからサービスをインストールする

Fabrikam では、OSR ボード上の LED 制御に Win32 サービスを使用しています。 同社にとってこのコンポーネントはデバイスのコア機能の一部であるため、基本 INF ([`osrfx2_DCHU_base.inx`]) の一部として組み込みます。  このユーザーモード サービス (usersvc) は、INF ファイルに [**AddService**](../install/inf-addservice-directive.md) ディレクティブを指定して宣言することで、追加および開始できます。

```cpp
[OsrFx2_Install.NT]
CopyFiles = OsrFx2_CopyFiles

[OsrFx2_Install.NT.Services]
AddService = WUDFRd, 0x000001fa, WUDFRD_ServiceInstall    ; Flag 0x2 sets this as the service for the device
AddService = osrfx2_DCHU_usersvc,, UserSvc_ServiceInstall

[UserSvc_ServiceInstall]
DisplayName = %UserSvcDisplayName%
ServiceType = 0x10                                ; SERVICE_WIN32_OWN_PROCESS
StartType = 0x3                                   ; SERVICE_DEMAND_START
ErrorControl = 0x1                                ; SERVICE_ERROR_NORMAL
ServiceBinary = %13%\osrfx2_DCHU_usersvc.exe
AddTrigger = UserSvc_AddTrigger                   ; AddTrigger syntax is only available in Windows 10 Version 2004 and above

[UserSvc_AddTrigger]
TriggerType = 1                                   ; SERVICE_TRIGGER_TYPE_DEVICE_INTERFACE_ARRIVAL
Action = 1                                        ; SERVICE_TRIGGER_ACTION_SERVICE_START
SubType = %GUID_DEVINTERFACE_OSRFX2%              ; Interface GUID
DataItem = 2, "USB\VID_0547&PID_1002"             ; SERVICE_TRIGGER_DATA_TYPE_STRING

[OsrFx2_CopyFiles]
osrfx2_DCHU_base.dll
osrfx2_DCHU_filter.dll
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

[Win32 アプリのソース コード](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_componentsoftware)は、サンプルに含まれます。

[Windows ハードウェア デベロッパー センター ダッシュボード](https://partner.microsoft.com/dashboard/Registration/Hardware)でターゲット指定が設定されているため、このコンポーネント ドライバー パッケージは デスクトップ SKU のみに配布されることに注意してください。  詳しくは、「[Windows Update にドライバーを公開する](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)」をご覧ください。

## <a name="allow-communication-with-a-hardware-support-app"></a>ハードウェア サポート アプリとの通信を許可する

Fabrikam は、Windows ドライバー パッケージの一部として GUI ベースのコンパニオン アプリを提供したいと考えています。  Win32 ベースのコンパニオン アプリケーションを Windows ドライバー パッケージの一部にすることはできないため、Win32 アプリをユニバーサル Windows プラットフォーム (UWP) に移植し、[アプリをデバイスとペアリング](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-access-for-universal-windows-platform-apps)します。

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

(サンプルに含まれない) 新しいアプリは、セキュリティで保護され、Microsoft Store で簡単に更新することができます。 UWP アプリケーション対応になったことで、Contoso は [DISM (展開イメージのサービスと管理)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows) を使ってアプリケーションを Windows デスクトップ エディションのイメージに事前に読み込みます。

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

ドライバーを容易に更新できるように、Fabrikam は、可能であれば [**dirid 13**](../install/using-dirids.md) を使って、[ドライバー ストア](../install/driver-store.md)をドライバー ファイルのコピー先として指定します。  コピー先ディレクトリの値として 13 を使うと、ドライバー更新プロセスの間の安定性が向上します。  [`osrfx2_DCHU_base.inx`  ] の例を次に示します。

```cpp
[DestinationDirs]
OsrFx2_CopyFiles = 13 ; copy to Driver Store
```

ファイルを動的に見つけてドライバー ストアから読み込む方法の詳細については、「[ドライバー パッケージの分離](driver-isolation.md#run-from-driver-store)」を参照してください。  

## <a name="summary"></a>要約

次の図は、Fabrikam と Contoso が DCH 準拠ドライバー用に作成したドライバー パッケージを示したものです。  疎結合の例では、[Windows ハードウェア デベロッパー センター ダッシュボード](https://partner.microsoft.com/dashboard/Registration/Hardware)で、基本パッケージ、拡張パッケージ、コンポーネントパッケージの 3 回にわたってパッケージが別個に提出されます。  密結合の例では、基本パッケージと拡張/コンポーネント パッケージの 2 つが提出されます。

![拡張、基本、コンポーネントの各ドライバー パッケージ](images/universal-scenarios.png)

コンポーネント INF はコンポーネント ハードウェア ID に一致し、基本 INF と拡張 INF はボードのハードウェア ID に一致することに注意してください。

## <a name="see-also"></a>関連項目

[Windows ドライバーの概要](getting-started-with-windows-drivers.md)

[拡張 INF ファイルの使用](../install/using-an-extension-inf-file.md)

[`osrfx2_DCHU_base.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_base/osrfx2_DCHU_base.inx

[`osrfx2_DCHU_usersvc.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_usersvc/osrfx2_DCHU_usersvc.inx

[`osrfx2_DCHU_component.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_component/osrfx2_DCHU_component.inx

[`osrfx2_DCHU_extension.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx
