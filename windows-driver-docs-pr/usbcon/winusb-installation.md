---
Description: ドライバーを実装するのではなく、デバイスのカーネル モード スタックに WinUSB (Winusb.sys) を USB デバイスの関数ドライバーとしてインストールします。
title: WinUSB (Winusb.sys) のインストール
ms.date: 05/09/2018
ms.localizationpriority: High
ms.openlocfilehash: d2157430a1e220e693d9ae88c3a3a36ce3fd3d2e
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "79437069"
---
# <a name="winusb-winusbsys-installation"></a>WinUSB (Winusb.sys) のインストール


1 つのアプリケーションのみによってアクセスされるデバイスなど、特定のユニバーサル シリアル バス (USB) デバイスについては、ドライバーを実装するのではなく、デバイスのカーネル モード スタックに [WinUSB](winusb.md) (Winusb.sys) を USB デバイスの関数ドライバーとしてインストールできます。

このトピックは次のセクションで構成されます。

-   [INF ファイルを使用せずに WinUSB を自動インストールする](#automatic-installation-of--winusb-without-an-inf-file)
-   [システム提供のデバイス クラスを指定して WinUSB をインストールする](#installing-winusb-by-specifying--the-system-provided-device-class)
-   [WinUSB インストール用のカスタム INF を作成する](#inf)
-   [Winusb.sys をインストールするドライバー パッケージの作成方法](#howto)

## <a name="automatic-installation-of-winusb-without-an-inf-file"></a><a href="" id="automatic-installation-of--winusb-without-an-inf-file"></a>INF ファイルを使用せずに WinUSB を自動インストールする


OEM または独立系ハードウェア ベンダー (IHV) は、Winusb.sys を Windows 8 以降のバージョンのオペレーティング システムに自動的にインストールするようにデバイスを構築できます。 このようなデバイスは、WinUSB デバイスと呼ばれており、組み込みの Winusb.inf を参照するカスタム INF ファイルを作成する必要はありません。

WinUSB デバイスを接続すると、システムによってデバイス情報が読み取られ、Winusb.sys が自動的に読み込まれます。

詳細については、「[WinUSB デバイス](automatic-installation-of-winusb.md)」を参照してください。

## <a name="installing-winusb-by-specifying-the-system-provided-device-class"></a><a href="" id="installing-winusb-by-specifying--the-system-provided-device-class"></a>システム提供のデバイス クラスを指定して WinUSB をインストールする


デバイスを接続すると、Windows によって Winusb.sys が自動的に読み込まれることがわかります (IHV がデバイスを WinUSB デバイスとして定義している場合)。 そうなっていない場合は、次の手順に従ってドライバーを読み込みます。

1.  デバイスをホスト システムに接続します。
2.  デバイス マネージャーを開き、デバイスを見つけます。
3.  デバイスを右クリックし、コンテキスト メニューの **[ドライバー ソフトウェアの更新]** を選択します。
4.  ウィザードで **[コンピューターを参照してドライバー ソフトウェアを検索します]** を選択します。
5.  **[コンピューター上のデバイス ドライバーの一覧から選択します]** を選択します。
6.  デバイス クラスの一覧から、 **[ユニバーサル シリアル バス デバイス]** を選択します。
7.  ウィザードに **[WinUsb デバイス]** が表示されます。 それを選択してドライバーを読み込みます。

デバイス クラスの一覧に **[ユニバーサル シリアル バス デバイス]** が表示されない場合は、カスタム INF を使用してドライバーをインストールする必要があります。
前の手順では、デバイスにアクセスするためのアプリ (UWP アプリまたは Windows デスクトップ アプリ) のデバイス インターフェイス GUID は追加されません。 この手順に従って、手動で GUID を追加する必要があります。

1.  前の手順で説明したように、ドライバーを読み込みます。
2.  guidgen.exe などのツールを使用して、デバイスのデバイス インターフェイス GUID を生成します。
3.  次のキーの下でデバイスのレジストリ キーを探します。

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\USB\\&lt;VID\_vvvv&PID\_pppp&gt;**

4.  **Device Parameters** キーの下で、**DeviceInterfaceGUID** という文字列レジストリ エントリ、または **DeviceInterfaceGUIDs** という複数行文字列エントリを追加します。 値を手順 2 で生成した GUID に設定します。
5.  デバイスをシステムから切断し、同じ物理ポートに再接続します。
    **注**  物理ポートを変更した場合は、手順 1 から 4 を繰り返す必要があります。

     

## <a name="writing-a-custom-inf-for-winusb-installation"></a><a href="" id="inf"></a>WinUSB インストール用のカスタム INF を作成する


ドライバー パッケージの一部として、Winusb.sys を USB デバイスの関数ドライバーとしてインストールする .inf ファイルを提供します。

次の .inf ファイルの例は、ほとんどの USB デバイスの WinUSB インストールを示しています (セクション名の **USB\_Install** を適切な *DDInstall* 値に変更するなど、多少の変更を伴います)。 必要に応じて、バージョン、製造元、モデルのセクションも変更する必要があります。 たとえば、適切な製造元の名前、署名されたカタログ ファイルの名前、正しいデバイス クラス、デバイスのベンダー ID (VID) と製品識別子 (PID) を入力します。

また、セットアップ クラスが "USBDevice" に設定されていることにも注意してください。 ベンダーは、USB ホスト コントローラーまたはハブではなく、別のクラスに属していないデバイスに対して "USBDevice" セットアップ クラスを使用できます。

USB 複合デバイス内のいずれかの機能の関数ドライバーとして WinUSB をインストールする場合は、その機能に関連付けられているハードウェア ID を INF で指定する必要があります。 機能のハードウェア ID は、**デバイス マネージャー**の devnode のプロパティから取得できます。 ハードウェア ID 文字列の形式は、"USB\\VID\_vvvv&PID\_pppp" です。

次の INF では、x64 ベースのシステム上に、OSR USB FX2 ボードの関数ドライバーとして WinUSB をインストールします。

> Windows 10 バージョン 1709 以降、Windows Driver Kit には [InfVerif.exe](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif) が用意されています。これを使用すると、ドライバーの INF ファイルをテストして、構文の問題がないこと、および INF ファイルがユニバーサルであることを確認できます。 ユニバーサル INF を提供することをお勧めします。 詳細については、「[ユニバーサル INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)」を参照してください。

``` syntax
;
;
; Installs WinUsb
;

[Version]
Signature = "$Windows NT$"
Class     = USBDevice
ClassGUID = {88BAE032-5A81-49f0-BC3D-A4FF138216D6}
Provider  = %ManufacturerName%
CatalogFile = WinUSBInstallation.cat
DriverVer=09/04/2012,13.54.20.543

; ========== Manufacturer/Models sections ===========

[Manufacturer]
%ManufacturerName% = Standard,NTamd64

[Standard.NTamd64]
%DeviceName% =USB_Install, USB\VID_0547&PID_1002

; ========== Class definition (for Windows 8 and ealier versions)===========

[ClassInstall32]
AddReg = ClassInstall_AddReg

[ClassInstall_AddReg]
HKR,,,,%ClassName%
HKR,,NoInstallClass,,1
HKR,,IconPath,%REG_MULTI_SZ%,"%systemroot%\system32\setupapi.dll,-20"
HKR,,LowerLogoVersion,,5.2

; =================== Installation ===================

[USB_Install]
Include = winusb.inf
Needs   = WINUSB.NT

[USB_Install.Services]
Include =winusb.inf
Needs   = WINUSB.NT.Services

[USB_Install.HW]
AddReg=Dev_AddReg

[USB_Install.Wdf]
KmdfService=WINUSB, WinUsb_Install

[WinUsb_Install]
KmdfLibraryVersion=1.11

[Dev_AddReg]
HKR,,DeviceInterfaceGUIDs,0x10000,"{9f543223-cede-4fa3-b376-a25ce9a30e74}"

; [DestinationDirs]
; If your INF needs to copy files, you must not use the DefaultDestDir directive here.  
; You must explicitly reference all file-list-section names in this section.

; =================== Strings ===================

[Strings]
ManufacturerName=""
ClassName="Universal Serial Bus devices"
DeviceName="Fx2 Learning Kit Device"
REG_MULTI_SZ = 0x00010000
```
> 新しいカスタム デバイス セットアップ クラスをインストールする場合にのみ、ClassInstall32 セクションをデバイスの INF ファイルに含めます。 システム提供のデバイス セットアップ クラスかカスタム クラスかを問わず、インストール済みクラスのデバイスの INF ファイルには、ClassInstall32 セクションを含めることはできません。 




デバイス固有の値と、次の一覧に記載されているいくつかの問題を除き、これらのセクションとディレクティブを使用して、任意の USB デバイスに WinUSB をインストールすることができます。 以下のリスト項目では、前の .inf ファイル内の**インクルード**と**ディレクティブ**について説明します。

-   **USB\_Install**: **USB\_Install** セクションの **Include** および **Needs** ディレクティブは、WinUSB をインストールするために必要です。 これらのディレクティブは変更しないでください。
-   **USB\_Install.Services**: **USB\_Install.Services** セクションの **Include** ディレクティブにより、システム提供の WinUSB 用 .inf (WinUSB.inf) をインクルードします。 この .inf ファイル (ターゲット システムにまだない場合) は、WinUSB 共同インストーラーによってインストールされます。 **Needs** ディレクティブでは、デバイスの関数ドライバーとして Winusb.sys をインストールするために必要な情報を含む、WinUSB.inf 内のセクションを指定します。 これらのディレクティブは変更しないでください。
    **注**  Windows XP では WinUSB.inf が提供されていないため、そのファイルを共同インストーラーによって Windows XP システムにコピーするか、Windows XP 用に別の修飾されたセクションを用意する必要があります。

     

-   **USB\_Install.HW**: これは .inf ファイルの重要なセクションです。 デバイスのデバイス インターフェイスのグローバル一意識別子 (GUID) を指定します。 **AddReg** ディレクティブは、指定されたインターフェイス GUID を標準レジストリ値に設定します。 Winusb.sys がデバイスの関数ドライバーとして読み込まれると、レジストリ値 DeviceInterfaceGUIDs キーが読み取られ、指定された GUID を使用してデバイス インターフェイスが表されます。 この例の GUID は、お使いのデバイス用に作成した GUID に置き換える必要があります。 デバイスのプロトコルが変更された場合は、新しいデバイス インターフェイス GUID を作成します。

    **注**  ユーザー モード ソフトウェアでは、DeviceInterfaceGUIDs キーの下に指定されているデバイス インターフェイス クラスのいずれかに関連付けられた登録済みデバイス インターフェイスを列挙するために、[**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw) を呼び出す必要があります。 **SetupDiGetClassDevs** からは、デバイスのデバイス ハンドルが返されます。それをユーザー モード ソフトウェアで [**WinUsb\_Initialize**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize) ルーチンに渡し、デバイス インターフェイスの WinUSB ハンドルを取得する必要があります。 これらのルーチンの詳細については、「[WinUSB 関数を使用して USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)」を参照してください。

次の INF では、x64 ベースのシステム上に、OSR USB FX2 ボードの関数ドライバーとして WinUSB をインストールします。 この例は、WDF 共同インストーラーを使用した INF を示しています。

``` syntax
;
;
; Installs WinUsb
;

[Version]
Signature = "$Windows NT$"
Class     = USBDevice
ClassGUID = {88BAE032-5A81-49f0-BC3D-A4FF138216D6}
Provider  = %ManufacturerName%
CatalogFile = WinUSBInstallation.cat
DriverVer=09/04/2012,13.54.20.543

; ========== Manufacturer/Models sections ===========

[Manufacturer]
%ManufacturerName% = Standard,NTamd64

[Standard.NTamd64]
%DeviceName% =USB_Install, USB\VID_0547&PID_1002

; ========== Class definition (for Windows 8 and ealier versions) ===========

[ClassInstall32]
AddReg = ClassInstall_AddReg

[ClassInstall_AddReg]
HKR,,,,%ClassName%
HKR,,NoInstallClass,,1
HKR,,IconPath,%REG_MULTI_SZ%,"%systemroot%\system32\setupapi.dll,-20"
HKR,,LowerLogoVersion,,5.2

; =================== Installation ===================

[USB_Install]
Include = winusb.inf
Needs   = WINUSB.NT

[USB_Install.Services]
Include =winusb.inf
Needs   = WINUSB.NT.Services

[USB_Install.HW]
AddReg=Dev_AddReg

[Dev_AddReg]
HKR,,DeviceInterfaceGUIDs,0x10000,"{9f543223-cede-4fa3-b376-a25ce9a30e74}"

[USB_Install.CoInstallers]
AddReg=CoInstallers_AddReg
CopyFiles=CoInstallers_CopyFiles

[CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,"WdfCoInstaller01011.dll,WdfCoInstaller","WinUsbCoInstaller2.dll"

[CoInstallers_CopyFiles]
WinUsbCoInstaller2.dll
WdfCoInstaller01011.dll

[DestinationDirs]
; If your INF needs to copy files, you must not use the DefaultDestDir directive here.  
CoInstallers_CopyFiles=11
; ================= Source Media Section =====================

[SourceDisksNames]
1 = %DiskName%

[SourceDisksFiles]
WinUsbCoInstaller2.dll=1
WdfCoInstaller01011.dll=1


; =================== Strings ===================

[Strings]
ManufacturerName=""
ClassName="Universal Serial Bus devices"
DeviceName="Fx2 Learning Kit Device"
DiskName="MyDisk"
REG_MULTI_SZ = 0x00010000
```

-   **USB\_Install.CoInstallers**: このセクションには、参照されている **AddReg** セクションと **CopyFiles** セクションがあり、WinUSB および KMDF 共同インストーラーをインストールしてデバイスに関連付けるためのデータと手順が含まれています。 ほとんどの USB デバイスでは、これらのセクションとディレクティブを変更せずに使用できます。
-   x86 ベースと x64 ベースのバージョンの Windows には、別々の共同インストーラーが用意されています。

    **注**  各共同インストーラーには、無料バージョンとチェック済みバージョンがあります。 無料バージョンは、すべての製品版を含む Windows の無償のビルドに WinUSB をインストールするために使用します。 チェック済みバージョン ("\_chk" のサフィックス付き) は、Windows のチェック済みビルドに WinUSB をインストールするために使用します。

Winusb.sys が読み込まれるたびに、レジストリ内で **DeviceInterfaceGUIDs** キーの下に指定されているデバイス インターフェイス クラスを持つデバイス インターフェイスが登録されます。

``` syntax
HKR,,DeviceInterfaceGUIDs, 0x10000,"{D696BFEB-1734-417d-8A04-86D01071C512}"
```

**注**  Windows XP または Windows Server 2003 用の再頒布可能な WinUSB パッケージを使用する場合は、アンインストール パッケージで WinUSB をアンインストールしないようにしてください。 他の USB デバイスによって WinUSB が使用されている可能性があるため、そのバイナリを共有フォルダーに残しておく必要があります。

 

## <a name="how-to-create-a-driver-package-that-installs-winusbsys"></a><a href="" id="howto"></a>Winusb.sys をインストールするドライバー パッケージの作成方法


デバイスの関数ドライバーとして WinUSB を使用するには、ドライバー パッケージを作成します。 ドライバー パッケージには、次のファイルが含まれている必要があります。

-   WinUSB 共同インストーラー (Winusbinstaller.dll)
-   KMDF 共同インストーラー (WdfcoinstallerXXX.dll)
-   デバイスの関数ドライバーとして Winusb.sys をインストールする .inf ファイル。 詳細については、[WinUSB インストール用の .Inf ファイルの作成](#inf)に関するページを参照してください。
-   パッケージ用の署名されたカタログ ファイル。 このファイルは、Vista 以降の x64 バージョンの Windows に WinUSB をインストールするために必要です。

![winusb インストール パッケージ](images/winusb-package.jpg)

**注**  ドライバー パッケージの内容が次の要件を満たしていることを確認してください。
-   KMDF 共同インストーラー ファイルと WinUSB 共同インストーラー ファイルは、同じバージョンの Windows Driver Kit (WDK) から取得する必要があります。
-   共同インストーラー ファイルは最新バージョンの WDK から取得する必要があります。これにより、ドライバーで最新の Windows リリースをすべてサポートできるようになります。
-   ドライバー パッケージの内容は、Winqual リリース署名を使用してデジタル署名されている必要があります。 署名されたカタログ ファイルを作成してテストする方法の詳細については、Windows デベロッパー センター - ハードウェア サイトの「[カーネルモードのコード署名のチュートリアル](https://go.microsoft.com/fwlink/p/?linkid=129409)」を参照してください。

 

1. [Windows Driver Kit (WDK) をダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)してインストールします。
2. USB デバイスが接続されているコンピューターにドライバー パッケージ フォルダーを作成します。 たとえば、c:\\UsbDevice です。
3. WinUSB 共同インストーラー (WinusbcoinstallerX.dll) を **WinDDK\\** <em>BuildNumber</em> **\\redist\\winusb** フォルダーからドライバー パッケージ フォルダーにコピーします。

   WinUSB 共同インストーラー (Winusbinstaller.dll) により、ターゲット システムに WinUSB が必要に応じてインストールされます。 WDK には、アーキテクチャ (x86 ベース、x64 ベース、Itanium ベースのシステム) に応じて、3 つのバージョンの共同インストーラーが含まれています。 それらはすべて WinusbcoinstallerX.dll という名前であり、**WinDDK\\** <em>BuildNumber</em> **\\redist\\winusb** フォルダーの適切なサブディレクトリにあります。

4. KMDF 共同インストーラー (WdfcoinstallerXXX.dll) を **WinDDK\\** <em>BuildNumber</em> **\\redist\\wdf** フォルダーからドライバー パッケージ フォルダーにコピーします。

   KMDF 共同インストーラー (WdfcoinstallerXXX.dll) により、ターゲット システムに正しいバージョンの KMDF が必要に応じてインストールされます。 Winusb.sys などの KMDF ベースのクライアント ドライバーでは、対応するバージョンの KMDF フレームワークがシステムに適切にインストールされる必要があるため、WinUSB 共同インストーラーのバージョンは、KMDF 共同インストーラーと一致している必要があります。 たとえば、Winusbcoinstaller2.dll では、Wdfcoinstaller01009.dll によってインストールされる KMDF バージョン 1.9 が必要とされます。 WdfcoinstallerXXX.dll の x86 バージョンと x64 バージョンは、WDK の **WinDDK\\** <em>BuildNumber</em> **\\redist\\wdf** フォルダーの下に含まれています。 次の表は、ターゲット システムに対して使用する、WinUSB 共同インストーラーおよび関連する KMDF 共同インストーラーを示しています。

   この表を使用して、WinUSB 共同インストーラーおよび関連する KMDF 共同インストーラーを確認してください。

   <table>
   <colgroup>
   <col width="33%" />
   <col width="33%" />
   <col width="33%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th>WinUSB 共同インストーラー</th>
   <th>KMDF ライブラリのバージョン</th>
   <th>KMDF 共同インストーラー</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td>Winusbcoinstaller.dll</td>
   <td>KMDF バージョン 1.5 以降が必要です</td>
   <td><p>Wdfcoinstaller01005.dll</p>
   <p>Wdfcoinstaller01007.dll</p>
   <p>Wdfcoinstaller01009.dll</p></td>
   </tr>
   <tr class="even">
   <td>Winusbcoinstaller2.dll</td>
   <td>KMDF バージョン 1.9 以降が必要です</td>
   <td>Wdfcoinstaller01009.dll</td>
   </tr>
   <tr class="odd">
   <td>Winusbcoinstaller2.dll</td>
   <td>KMDF バージョン 1.11 以降が必要です</td>
   <td>WdfCoInstaller01011.dll</td>
   </tr>
   </tbody>
   </table>

     

5. USB デバイスの関数ドライバーとして Winusb.sys をインストールする .inf ファイルを作成します。
6. パッケージ用の署名されたカタログ ファイルを作成します。 このファイルは、x64 バージョンの Windows に WinUSB をインストールするために必要です。
7. USB デバイスをコンピューターに接続します。
8. ドライバーをインストールするために**デバイス マネージャー**を開きます。 **ドライバー ソフトウェアの更新**ウィザードに表示される手順に従って、手動インストールを選択します。 インストールを完了するには、ドライバー パッケージ フォルダーの場所を指定する必要があります。

## <a name="related-topics"></a>関連トピック
[WinUSB アーキテクチャとモジュール](winusb-architecture.md)  
[USB クライアント ドライバー開発用のドライバー モデルの選択](winusb-considerations.md)  
[WinUSB 関数を使用して USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 電源管理](winusb-power-management.md)  
[パイプ ポリシー修正のための WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB](winusb.md)  



