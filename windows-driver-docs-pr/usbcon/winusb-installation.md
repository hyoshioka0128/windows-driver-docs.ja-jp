---
Description: ドライバーを実装する代わりに、デバイスのカーネルモードスタックに WinUSB (Winusb .sys) を USB デバイスの関数ドライバーとしてインストールします。
title: WinUSB (Winusb.sys) のインストール
ms.date: 05/09/2018
ms.localizationpriority: High
ms.openlocfilehash: d2157430a1e220e693d9ae88c3a3a36ce3fd3d2e
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402524"
---
# <a name="winusb-winusbsys-installation"></a>WinUSB (Winusb.sys) のインストール


1つのアプリケーションのみによってアクセスされるデバイスなど、特定のユニバーサルシリアルバス (USB) デバイスについては、ドライバーを実装する代わりに、デバイスのカーネルモードスタックに[winusb](winusb.md) (winusb .sys) を USB デバイスの関数ドライバーとしてインストールできます。

このトピックは次のセクションで構成されます。

-   [INF ファイルを使用せずに WinUSB を自動インストールする](#automatic-installation-of--winusb-without-an-inf-file)
-   [システム指定のデバイスクラスを指定して WinUSB をインストールする](#installing-winusb-by-specifying--the-system-provided-device-class)
-   [WinUSB インストール用のカスタム INF の作成](#inf)
-   [Winusb .sys をインストールするドライバーパッケージを作成する方法](#howto)

## <a href="" id="automatic-installation-of--winusb-without-an-inf-file"></a>INF ファイルを使用せずに WinUSB を自動インストールする


OEM または独立系ハードウェアベンダー (IHV) は、Winusb を Windows 8 以降のバージョンのオペレーティングシステムに自動的にインストールするようにデバイスを構築できます。 このようなデバイスは、WinUSB デバイスと呼ばれており、組み込みの Winusb .inf を参照するカスタム INF ファイルを作成する必要はありません。

WinUSB デバイスを接続すると、システムによってデバイス情報が読み取られ、Winusb .sys が自動的に読み込まれます。

詳細については、「 [Winusb デバイス](automatic-installation-of-winusb.md)」を参照してください。

## <a href="" id="installing-winusb-by-specifying--the-system-provided-device-class"></a>システム指定のデバイスクラスを指定して WinUSB をインストールする


デバイスに接続すると、Windows によって Winusb が自動的に読み込まれることがわかります (IHV がデバイスを WinUSB デバイスとして定義している場合)。 それ以外の場合は、次の手順に従ってドライバーを読み込みます。

1.  デバイスをホストシステムに接続します。
2.  デバイスマネージャーを開き、デバイスを見つけます。
3.  デバイスを右クリックし、コンテキストメニューの **[ドライバーソフトウェアの更新...]** を選択します。
4.  ウィザードで、 **[コンピューターを参照してドライバーソフトウェアを参照する]** を選択します。
5.  **[コンピューターのデバイスドライバーの一覧から選択できるようにする]** を選択します。
6.  デバイスクラスの一覧から、 **[ユニバーサルシリアルバスデバイス]** を選択します。
7.  **Winusb デバイス**が表示されます。 ドライバーを読み込むには、このチェックボックスをオンにします。

**ユニバーサルシリアルバスデバイス**がデバイスクラスの一覧に表示されない場合は、カスタム INF を使用してドライバーをインストールする必要があります。
前の手順では、デバイスにアクセスするためのアプリ (UWP アプリまたは Windows デスクトップアプリ) のデバイスインターフェイス GUID は追加されません。 この手順に従って、手動で GUID を追加する必要があります。

1.  前の手順で説明したように、ドライバーを読み込みます。
2.  Guidgen.exe などのツールを使用して、デバイスのデバイスインターフェイス GUID を生成します。
3.  次のキーで、デバイスのレジストリキーを探します。

    **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\列挙\\USB\\&lt;VID\_vvvv & PID\_pppp&gt;**

4.  **Device Parameters**キーの下に、 **deviceinterfaceguid**という名前の文字列レジストリエントリ、または**Deviceinterfaceguid**という名前の複数文字列エントリを追加します。 値を、手順 2. で生成した GUID に設定します。
5.  デバイスをシステムから切断し、同じ物理ポートに再接続します。
    **注**  物理ポートを変更した場合は、手順 1. ~ 4. を繰り返す必要があります。

     

## <a href="" id="inf"></a>WinUSB インストール用のカスタム INF の作成


ドライバーパッケージの一部として、Winusb を USB デバイスの関数ドライバーとしてインストールする .inf ファイルを指定します。

次の例の .inf ファイルは、ほとんどの USB デバイスの WinUSB インストールを示しています。たとえば、セクション名に「」という名前の**usb\_インストール**すると、適切な*ddinstall*値が表示されます。 必要に応じて、バージョン、製造元、およびモデルのセクションも変更する必要があります。 たとえば、適切な製造元の名前、署名されたカタログファイルの名前、正しいデバイスクラス、およびデバイスのベンダー id (VID) と製品識別子 (PID) を入力します。

また、セットアップクラスが "USBDevice" に設定されていることにも注意してください。 ベンダーは、USB ホストコントローラーまたはハブではなく、別のクラスに属していないデバイスに対して "USBDevice" セットアップクラスを使用できます。

USB 複合デバイス内のいずれかの関数の関数ドライバーとして WinUSB をインストールする場合は、その関数に関連付けられているハードウェア ID を INF で指定する必要があります。 **デバイスマネージャー**の devnode のプロパティから、関数のハードウェア ID を取得できます。 ハードウェア ID 文字列の形式は、"USB\\VID\_vvvv & PID\_pppp" です。

次の INF は、x64 ベースのシステム上に、OSR USB FX2 ボードの関数ドライバーとして WinUSB をインストールします。

> Windows 10 バージョン1709以降、Windows Driver Kit には InfVerif が用意されてい[ます。](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)このキットを使用すると、ドライバーの inf ファイルをテストして、構文の問題がないこと、および INF ファイルがユニバーサルであることを確認できます。 ユニバーサル INF を提供することをお勧めしています。 詳細については、「 [UNIVERSAL INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)」を参照してください。

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
> 新しいカスタムデバイスセットアップクラスをインストールするには、デバイスの INF ファイルに ClassInstall32 セクションのみを含めます。 インストールされているクラスのデバイスの INF ファイル。システムが提供するデバイスセットアップクラスまたはカスタムクラスに ClassInstall32 セクションを含めることはできません。 




デバイス固有の値と、次の一覧に記載されているいくつかの問題を除き、これらのセクションとディレクティブを使用して、任意の USB デバイスに WinUSB をインストールすることができます。 これらのリスト項目は、前の .inf ファイルの**インクルード** **ディレクティブとディレクティブ**を記述します。

-   **Usb\_インストール**: winusb をインストールするには、[ **usb\_インストール**] セクションの [**インクルード**と**ニーズ**] ディレクティブが必要です。 これらのディレクティブは変更しないでください。
-   **Usb\_install. services**: **usb\_install. Services**セクションの**Include**ディレクティブには、winusb (winusb .inf) 用のシステム提供の .inf が含まれています。 この .inf ファイルは、WinUSB 共同インストーラー (ターゲットシステムにまだインストールされていない場合) によってインストールされます。 **必要**に応じて、winusb .inf 内のセクションを指定します。これには、デバイスの関数ドライバーとして winusb をインストールするために必要な情報が含まれています。 これらのディレクティブは変更しないでください。
    **注**  windows xp では winusb .inf が提供されていないため、ファイルは共同インストーラーによって windows xp システムにコピーするか、windows xp 用に別の修飾されたセクションを指定する必要があります。

     

-   **USB\_Install. HW**: このセクションは .inf ファイルのキーです。 デバイスのデバイスインターフェイスグローバル一意識別子 (GUID) を指定します。 **AddReg**ディレクティブは、標準レジストリ値に指定されたインターフェイス GUID を設定します。 Winusb .sys がデバイスの関数ドライバーとして読み込まれると、レジストリ値 DeviceInterfaceGUIDs キーを読み取り、指定された GUID を使用してデバイスインターフェイスを表します。 この例の GUID は、デバイス専用に作成したものに置き換える必要があります。 デバイスのプロトコルが変更された場合は、新しいデバイスインターフェイス GUID を作成します。

      ユーザーモードソフトウェアでは、DeviceInterfaceGUIDs キーの下で指定されたデバイスインターフェイスクラスのいずれかに関連付けられている登録済みのデバイスインターフェイスを列挙するために、 [**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)を呼び出す必要がある**ことに注意**してください。 **SetupDiGetClassDevs**は、デバイスのデバイスハンドルを返します。ユーザーモードソフトウェアは、 [**Winusb\_Initialize**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)ルーチンに渡す必要があり、デバイスインターフェイスの winusb ハンドルを取得します。 これらのルーチンの詳細については、「 [Winusb 機能を使用して Usb デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)」を参照してください。

次の INF は、x64 ベースのシステム上に、OSR USB FX2 ボードの関数ドライバーとして WinUSB をインストールします。 この例は、WDF coinstallers を使用した INF を示しています。

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

-   **CoInstallers**: このセクションには、参照される**AddReg**と**CopyFiles**セクションが含まれています。このセクションには、winusb と kmdf の共同インストーラーをインストールしてデバイスに関連付けるためのデータと手順が含まれています。\_ ほとんどの USB デバイスでは、これらのセクションとディレクティブを変更せずに使用できます。
-   X86 ベースおよび x64 ベースのバージョンの Windows では、個別の共同インストーラーが用意されています。

    各共同インストーラーには、無料バージョンとチェックされたバージョンがあり  **ことに注意**してください。 無料バージョンを使用して、すべての製品版を含む Windows の無償のビルドに WinUSB をインストールします。 チェックされたバージョン ("\_chk" サフィックス) を使用して、Windows のチェックされたビルドに WinUSB をインストールします。

Winusb .sys が読み込まれるたびに、 **Deviceinterfaceguids**キーの下にあるレジストリに指定されているデバイスインターフェイスクラスを持つデバイスインターフェイスが登録されます。

``` syntax
HKR,,DeviceInterfaceGUIDs, 0x10000,"{D696BFEB-1734-417d-8A04-86D01071C512}"
```

**注**  windows XP または windows Server 2003 の再頒布可能な winusb パッケージを使用する場合は、アンインストールパッケージで winusb をアンインストールしないようにしてください。 他の USB デバイスは WinUSB を使用している可能性があるため、バイナリを共有フォルダーに残しておく必要があります。

 

## <a href="" id="howto"></a>Winusb .sys をインストールするドライバーパッケージを作成する方法


デバイスの関数ドライバーとして WinUSB を使用するには、ドライバーパッケージを作成します。 ドライバーパッケージには、次のファイルが含まれている必要があります。

-   WinUSB 共同インストーラー (winusbinstaller .dll)
-   KMDF 共同インストーラー (Wdfcoinstaller Xxx .dll)
-   デバイスの関数ドライバーとして Winusb .sys をインストールする .inf ファイル。 詳細については、「の書き込み」を参照してください[。WinUSB インストール用の Inf ファイル](#inf)。
-   パッケージ用に署名されたカタログファイル。 このファイルは、Vista 以降の x64 バージョンの Windows に WinUSB をインストールするために必要です。

![winusb インストールパッケージ](images/winusb-package.jpg)

**注**  ドライバパッケージの内容が次の要件を満たしていることを確認してください。
-   KMDF および WinUSB 共同インストーラーファイルは、同じバージョンの Windows Driver Kit (WDK) から取得する必要があります。
-   共同インストーラーファイルは最新バージョンの WDK から取得する必要があります。これにより、ドライバーは最新のすべての Windows リリースをサポートできるようになります。
-   ドライバーパッケージの内容は、Winqual リリースシグネチャを使用してデジタル署名されている必要があります。 署名されたカタログファイルを作成してテストする方法の詳細については、Windows デベロッパーセンターのハードウェアサイトの「[カーネルモードコード署名のチュートリアル](https://go.microsoft.com/fwlink/p/?linkid=129409)」を参照してください。

 

1. [Windows Driver Kit (WDK) をダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)し、インストールします。
2. USB デバイスが接続されているコンピューターにドライバーパッケージフォルダーを作成します。 たとえば、c:\\UsbDevice です。
3. WinUSB 共同インストーラー (WinusbcoinstallerX .dll) を、 **WinDDK\\** の\\再頒布可能ファイルの **\\winusb**フォルダーからドライバーパッケージフォルダーにコピーします。

   WinUSB 共同インストーラー (Winusbinstaller .dll) は、必要に応じて、ターゲットシステムに WinUSB をインストールします。 WDK には、x86 ベース、x64 ベース、および Itanium ベースのシステムアーキテクチャに応じて、3つのバージョンの共同インストーラーが含まれています。 これらはすべて WinusbcoinstallerX という名前であり、適切なサブディレクトリにあります。このファイルは、 **\\** の\\の再**頒布可能パッケージ\\winusb**フォルダーにあります。

4. **WinDDK\\** の **\\redist\\wdf**フォルダーから、ドライバーパッケージフォルダーに Kmdf 共同インストーラー (wdfcoinstaller xxx .dll) をコピーします。

   必要に応じて、KMDF 共同インストーラー (Wdfcoinstaller Xxx .dll) によってターゲットシステムに適切なバージョンの KMDF がインストールされます。 Winusb (Winusb) などの KMDF ベースのクライアントドライバーでは、対応するバージョンの KMDF フレームワークがシステムに適切にインストールされている必要があるため、WinUSB 共同インストーラーのバージョンは KMDF 共同インストーラーと一致している必要があります。 たとえば、Winusbcoinstaller2 では、Wdfcoinstaller01009 によってインストールされる KMDF バージョン1.9 が必要です。 **WinDDK\\** の **\\/redist\\wdf**フォルダーにある WDK には、X86 および X64 バージョンの wdfcoインストーラ xxx が含まれます。 次の表は、WinUSB 共同インストーラーと、ターゲットシステムで使用する関連する KMDF 共同インストーラーを示しています。

   この表を使用して、WinUSB 共同インストーラーと関連付けられている KMDF 共同インストーラーを確認します。

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
   <td>Winusbcoinstaller インストーラー .dll</td>
   <td>KMDF バージョン1.5 以降が必要です</td>
   <td><p>Wdfcoinstaller01005</p>
   <p>Wdfcoinstaller01007</p>
   <p>Wdfcoinstaller01009</p></td>
   </tr>
   <tr class="even">
   <td>Winusbcoinstaller2</td>
   <td>KMDF バージョン1.9 以降が必要です</td>
   <td>Wdfcoinstaller01009</td>
   </tr>
   <tr class="odd">
   <td>Winusbcoinstaller2</td>
   <td>KMDF バージョン1.11 以降が必要です</td>
   <td>WdfCoInstaller01011</td>
   </tr>
   </tbody>
   </table>

     

5. USB デバイスの関数ドライバーとして Winusb .sys をインストールする .inf ファイルを作成します。
6. パッケージ用に署名されたカタログファイルを作成します。 このファイルは、x64 バージョンの Windows に WinUSB をインストールするために必要です。
7. USB デバイスをコンピューターに接続します。
8. **デバイスマネージャー**を開いてドライバーをインストールします。 **ドライバーソフトウェアの更新**ウィザードの指示に従って、[手動インストール] を選択します。 インストールを完了するには、ドライバーパッケージフォルダーの場所を指定する必要があります。

## <a name="related-topics"></a>関連トピック
[WinUSB アーキテクチャとモジュール](winusb-architecture.md)  
[USB クライアントドライバーを開発するためのドライバーモデルの選択](winusb-considerations.md)  
[WinUSB 機能を使用して USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 電源管理](winusb-power-management.md)  
[パイプ ポリシー修正のための WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB](winusb.md)  



