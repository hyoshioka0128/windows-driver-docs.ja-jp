---
Description: デバイスのカーネル モード スタックでドライバーを実装する代わりに、USB デバイスの機能のドライバーとして WinUSB (Winusb.sys) をインストールします。
title: WinUSB (Winusb.sys) のインストール
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0898e03722bfa73103966b5855cc016d9ce05ef1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389175"
---
# <a name="winusb-winusbsys-installation"></a>WinUSB (Winusb.sys) のインストール


インストールする単一のアプリケーションによってアクセスされるデバイスなど、ユニバーサル シリアル バス (USB) デバイスの特定[WinUSB](winusb.md) (Winusb.sys) の代わりに、USB デバイスの機能のドライバーとして、デバイスのカーネル モード スタックでドライバーを実装します。

このトピックは次のセクションで構成されます。

-   [WinUSB INF ファイルを使用せずに自動的にインストール](#automatic-installation-of--winusb-without-an-inf-file)
-   [システム指定のデバイス クラスを指定することによって WinUSB をインストールします。](#installing-winusb-by-specifying--the-system-provided-device-class)
-   [WinUSB インストール用のカスタム INF の書き込み](#inf)
-   [Winusb.sys をインストールするドライバー パッケージを作成する方法](#howto)

## <a href="" id="automatic-installation-of--winusb-without-an-inf-file"></a>WinUSB INF ファイルを使用せずに自動的にインストール


OEM または独立系ハードウェア ベンダー (IHV) は、Windows 8 およびそれ以降のバージョンのオペレーティング システムに、Winusb.sys を自動的にインストールできるように、デバイスを構築できます。 このようなデバイスでは、WinUSB デバイスは呼び出され、インボックス Winusb.inf を参照するカスタム INF ファイルを記述する必要はありません。

WinUSB デバイスを接続するときに、システムはデバイスの情報を読み取り、Winusb.sys を自動的に読み込みます。

詳細については、次を参照してください。 [WinUSB デバイス](automatic-installation-of-winusb.md)します。

## <a href="" id="installing-winusb-by-specifying--the-system-provided-device-class"></a>システム指定のデバイス クラスを指定することによって WinUSB をインストールします。


デバイスを接続するときに自動的に (IHV が定義されている場合、デバイス WinUSB デバイスとして)、Windows が Winusb.sys を読み込むことが分かります。 それ以外の場合、ドライバーの読み込み、次の手順に従ってください。

1.  ホスト システムにデバイスを接続します。
2.  デバイス マネージャーを開き、デバイスを探します。
3.  デバイスを右クリックして**ドライバー ソフトウェアを更新しています.** コンテキスト メニュー。
4.  ウィザードで、次のように選択します。**参照コンピューターでドライバー ソフトウェア**します。
5.  選択**コンピューター上のデバイス ドライバーの一覧から選択できるように**します。
6.  デバイス クラスのリストから選択**ユニバーサル シリアル バス デバイス**します。
7.  ウィザードが表示されます**WinUsb デバイス**します。 ドライバーをロードすることを選択します。

場合**ユニバーサル シリアル バス デバイス**がカスタム INF を使用して、ドライバーをインストールする必要がありますにデバイスのクラスの一覧に表示されません。
前の手順では、アプリ (UWP アプリまたは Windows デスクトップ アプリ)、デバイスにアクセスするデバイス インターフェイスの GUID は追加されません。 GUID は、次の手順で手動で追加する必要があります。

1.  前の手順に従って、ドライバーを読み込み。
2.  Guidgen.exe などのツールを使用して、デバイスには、デバイス インターフェイスの GUID を生成します。
3.  このキーの下のデバイスのレジストリ キーを探します。

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\USB\\&lt;VID\_vvvv&PID\_pppp&gt;**

4.  下、**デバイス パラメーター**キー、という名前の文字列のレジストリ エントリを追加**DeviceInterfaceGUID**またはという名前の複数行文字列エントリ**DeviceInterfaceGUIDs**します。 手順 2. で生成された GUID 値を設定します。
5.  システムからデバイスを切断し、同じ物理ポートに再接続します。
    **注**  物理ポートを変更するかどうかは、手順 1. ~ 4. を繰り返す必要があります。

     

## <a href="" id="inf"></a>WinUSB インストール用のカスタム INF の書き込み


ドライバー パッケージの一部として、USB デバイスの機能のドライバーとして Winusb.sys をインストールする .inf ファイルを提供します。

.Inf ファイルの例を次に示します WinUSB インストールの変更など、いくつかの変更のほとんどの USB デバイスの**USB\_インストール**、該当するセクション名で*DDInstall*値。 バージョン、製造元、および必要に応じて、各モデルの説明を変更することも必要があります。 たとえば、デバイスの適切な製造元の名前、署名済みカタログ ファイルは、正しいデバイス クラスと仕入先 id (VID) および製品 id (PID) の名前を提供します。

セットアップ クラスが"USBDevice"に設定されていることにも注目してください。 ベンダーは、別のクラスに属していない、USB ホスト コント ローラーまたはハブではないデバイスの"USBDevice"セットアップ クラスを使用できます。

関数のドライバーを USB 複合デバイス内の関数のいずれかとして WinUSB をインストールする場合は、関数、INF に関連付けられているハードウェア ID を指定する必要があります。 関数のハードウェア ID を取得するで devnode のプロパティから**デバイス マネージャー**します。 ハードウェア ID の文字列形式が"USB\\VID\_vvvv & PID\_pppp"。

次の INF には、x64 ベース システムで OSR USB FX2 ボードの機能のドライバーとして WinUSB がインストールされます。

> Windows 10 バージョン 1709 以降、Windows Driver Kit は、 [InfVerif.exe](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)構文の問題がないと、INF ファイルはユニバーサルかどうかを確認するドライバーの INF ファイルをテストに使用することできます。 私たちユニバーサル INF を提供することです。 詳細については、次を参照してください。[ユニバーサル INF ファイルを使用して](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)します。

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
> 新しいカスタム デバイス セットアップ クラスをインストールするデバイスの INF ファイルで ClassInstall32 セクションにはのみが含まれます。 インストールされているクラスで、デバイスの INF ファイル システム提供のデバイス セットアップ クラスまたはカスタム クラスであるかどうかを含めない ClassInstall32 セクション。 




デバイス固有の値とは、次の一覧に記載されているいくつかの問題、を除き WinUSB を任意の USB デバイスをインストールするのにには、これらのセクションでは、ディレクティブを使用できます。 これらのリスト アイテムについて説明します、**が含まれます**と**ディレクティブ**で上記の .inf ファイル。

-   **USB\_インストール**:**Include**と**必要がある**ディレクティブ、 **USB\_インストール**セクション WinUSB をインストールする必要があります。 これらのディレクティブを変更する必要があります。
-   **USB\_Install.Services**:**Include**ディレクティブで、 **USB\_Install.Services**セクションには、システム提供の .inf には WinUSB (WinUSB.inf) が含まれています。 この .inf ファイルは、ターゲット システムにいない場合は、WinUSB 共同インストーラーによってインストールされます。 **必要がある**ディレクティブは、デバイスの機能のドライバーとして Winusb.sys をインストールするために必要な情報を含む WinUSB.inf 内のセクションを指定します。 これらのディレクティブを変更する必要があります。
    **注**  WinUSB.inf を提供しないため、Windows XP、共同インストーラーによって、ファイルが Windows XP システムにコピーするかする必要があります、または Windows XP の装飾を別のセクションを提供する必要があります。

     

-   **USB\_Install.HW**:このセクションでは、.inf ファイルのキーです。 これには、デバイスのデバイス インターフェイス グローバル一意識別子 (GUID) を指定します。 **AddReg**ディレクティブは、標準のレジストリ値で指定されたインターフェイスの GUID を設定します。 デバイスの機能のドライバーとして Winusb.sys が読み込まれると、レジストリ キーを読み取って値 DeviceInterfaceGUIDs と、指定された GUID を使用して、デバイス インターフェイスを表します。 この例では GUID は、具体的にはお使いのデバイスを作成するものに置き換える必要があります。 デバイスのプロトコルを変更する場合は、新しいデバイス インターフェイスの GUID を作成します。

    **注**  ユーザー モードのソフトウェアを呼び出す必要があります[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)デバイス インターフェイスのいずれかに関連付けられている登録済みデバイスのインターフェイスを列挙するにはDeviceInterfaceGUIDs キーで指定されているクラス。 **SetupDiGetClassDevs**ユーザー モード ソフトウェアに渡す必要がありますし、デバイスのデバイス ハンドルを返します、 [ **WinUsb\_初期化**](https://msdn.microsoft.com/library/windows/hardware/ff540277) WinUSB ハンドルを取得するルーチンデバイスのインターフェイス。 これらのルーチンの詳細については、次を参照してください。 [WinUSB 関数を使用して、USB デバイスへのアクセス方法](using-winusb-api-to-communicate-with-a-usb-device.md)します。

次の INF には、x64 ベース システムで OSR USB FX2 ボードの機能のドライバーとして WinUSB がインストールされます。 この例では、WDF 共同インストーラーを INF を示します。

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

-   **USB\_Install.CoInstallers**:このセクションでは、参照先が含まれています**AddReg**と**CopyFiles**セクションで、データとを WinUSB および KMDF 共同インストーラーをインストールして、デバイスに関連付ける手順が含まれています。 ほとんどの USB デバイスには、これらのセクションと変更を加えなければディレクティブを使用できます。
-   Windows の x86 ベースおよび x64 ベースのバージョンでは、個別の共同インストーラーがあります。

    **注**  各共同インストーラーがチェックされている無料版です。 すべての製品版を含む、Windows の無料のビルドに WinUSB をインストールするのにには、無料版を使用します。 チェック済みバージョンを使用して (で、"\_chk"サフィックス) に Windows のチェック ビルド WinUSB をインストールします。

Winusb.sys 読み込みされるたびに、下のレジストリで指定されているデバイスのインターフェイス クラスを持つデバイス インターフェイスを登録、 **DeviceInterfaceGUIDs**キー。

``` syntax
HKR,,DeviceInterfaceGUIDs, 0x10000,"{D696BFEB-1734-417d-8A04-86D01071C512}"
```

**注**  WinUSB の再頒布可能パッケージのパッケージを使用して Windows XP または Windows Server 2003 の場合、アンインストール パッケージで WinUSB をアンインストールすることはありません確認します。 バイナリは、共有フォルダーに残す必要があるために、他の USB デバイスが WinUSB を使用する場合があります。

 

## <a href="" id="howto"></a>Winusb.sys をインストールするドライバー パッケージを作成する方法


WinUSB 関数ドライバーとしてを使用するには、ドライバー パッケージを作成します。 ドライバー パッケージには、これらのファイルを含める必要があります。

-   WinUSB 共同インストーラー (Winusbcoinstaller.dll)
-   KMDF 共同インストーラー (WdfcoinstallerXXX.dll)
-   デバイスの機能のドライバーとして Winusb.sys をインストールする .inf ファイル。 詳細については、次を参照してください。[書き込み、します。WinUSB インストール用の Inf ファイル](#inf)します。
-   パッケージの署名済みカタログ ファイル。 このファイルは、x64 WinUSB をインストールする必要は Windows Vista 以降のバージョン。

![winusb インストール パッケージ](images/winusb-package.jpg)

**注**  ドライバー パッケージの内容が、これらの要件を満たしていることを確認します。
-   KMDF と WinUSB 共同インストーラー ファイルは、同じバージョンの Windows Driver Kit (WDK) から取得する必要があります。
-   共同インストーラー ファイルは、ドライバーが最新の Windows のすべてのリリースをサポートするよう、WDK の最新バージョンから取得する必要があります。
-   ドライバー パッケージの内容は Winqual のリリースのシグネチャを持つデジタル署名する必要があります。 作成し、署名済みカタログ ファイルをテストする方法の詳細については、次を参照してください。[カーネル モード コード署名のチュートリアル](https://go.microsoft.com/fwlink/p/?linkid=129409)Windows デベロッパー センター - ハードウェア サイト。

 

1. [Windows Driver Kit (WDK) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)し、インストールします。
2. コンピューターに USB デバイスが接続されているドライバー パッケージのフォルダーを作成します。 たとえば、c:\\UsbDevice します。
3. (WinusbcoinstallerX.dll) WinUSB 共同インストーラーをコピー、 **WinDDK\\**<em>BuildNumber</em>**\\redist\\winusb**ドライバー パッケージ フォルダーのフォルダー。

   WinUSB 共同インストーラー (Winusbcoinstaller.dll) は、必要に応じて、ターゲット システムに WinUSB をインストールします。 次の 3 つのバージョン システム アーキテクチャに応じて共同インストーラーにはが WDK に含まれています。 x86 ベース、x64 ベースおよび Itanium ベース システム。 WinusbcoinstallerX.dll すべてという名前は、適切なサブディレクトリにある、 **WinDDK\\**<em>BuildNumber</em>**\\redist\\winusb**フォルダー。

4. (WdfcoinstallerXXX.dll) KMDF 共同インストーラーをコピー、 **WinDDK\\**<em>BuildNumber</em>**\\redist\\wdf**フォルダードライバー パッケージのフォルダー。

   KMDF 共同インストーラー (WdfcoinstallerXXX.dll) は、必要に応じて、ターゲット システムでは、KMDF の正しいバージョンをインストールします。 WinUSB 共同インストーラーのバージョンは、Winusb.sys などの KMDF ベースのクライアント ドライバーは、システムに正しくインストールするために、KMDF フレームワークの対応するバージョンを必要とするため、KMDF 共同インストーラーと一致する必要があります。 たとえば、Winusbcoinstaller2.dll KMDF Wdfcoinstaller01009.dll によってインストールされるバージョン 1.9 が必要です。 WdfcoinstallerXXX.dll の x86 および x64 バージョンでは、下の WDK に含まれています、 **WinDDK\\**<em>BuildNumber</em>**\\redist\\wdf**フォルダー。 次の表は、ターゲット システムで使用するには、WinUSB 共同インストーラーと関連付けられている KMDF 共同インストーラーを示します。

   WinUSB 共同インストーラーと関連付けられている KMDF 共同インストーラーを確認するのにには、このテーブルを使用します。

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
   <td>KMDF バージョン 1.5 以降が必要です。</td>
   <td><p>Wdfcoinstaller01005.dll</p>
   <p>Wdfcoinstaller01007.dll</p>
   <p>Wdfcoinstaller01009.dll</p></td>
   </tr>
   <tr class="even">
   <td>Winusbcoinstaller2.dll</td>
   <td>KMDF バージョン 1.9 以降が必要です。</td>
   <td>Wdfcoinstaller01009.dll</td>
   </tr>
   <tr class="odd">
   <td>Winusbcoinstaller2.dll</td>
   <td>KMDF バージョン 1.11 以降が必要です。</td>
   <td>WdfCoInstaller01011.dll</td>
   </tr>
   </tbody>
   </table>

     

5. USB デバイスの機能のドライバーとして Winusb.sys をインストールする .inf ファイルを作成します。
6. パッケージの署名済みカタログ ファイルを作成します。 このファイルは、x64 WinUSB をインストールする必要は Windows のバージョン。
7. コンピューターに USB デバイスを接続します。
8. 開いている**デバイス マネージャー**ドライバーをインストールします。 指示に従って、**ドライバー ソフトウェアの更新**ウィザード手動インストールを選択します。 ドライバーの場所にインストールを完了するパッケージ フォルダーを指定する必要があります。

## <a name="related-topics"></a>関連トピック
[WinUSB アーキテクチャとモジュール](winusb-architecture.md)  
[USB クライアント ドライバーを開発するためのドライバー モデルの選択](winusb-considerations.md)  
[WinUSB 関数を使用して、USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 電源管理](winusb-power-management.md)  
[ポリシーの変更をパイプ WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 関数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)  
[WinUSB](winusb.md)  



