---
title: INF ファイルで WDF ディレクティブの指定
description: INF ファイルで WDF ディレクティブの指定
ms.assetid: aefc678e-dc81-47dc-a84b-f1a79c16cad9
keywords:
- WDF ディレクティブ WDK UMDF
- DDInstall セクション WDK UMDF
- UmdfService INF ディレクティブ WDK UMDF
- UmdfServiceOrder INF ディレクティブ WDK UMDF
- UmdfImpersonationLevel INF ディレクティブ WDK UMDF
- UmdfMethodNeitherAction INF ディレクティブ WDK UMDF
- UmdfKernelModeClientPolicy INF ディレクティブ WDK UMDF
- UmdfLibraryVersion INF ディレクティブ WDK UMDF
- ServiceBinary INF ディレクティブ WDK UMDF
- DriverCLSID INF ディレクティブ WDK UMDF
- WDK UMDF ディレクティブ
- WDK UMDF 固有のディレクティブ
- UMDF サービス-インストール セクション WDK
- INF ファイル WDK UMDF、ディレクティブ
- UmdfDispatcher INF ディレクティブ WDK UMDF、構文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 265a68ae5e2139051e497fbd32321215bac2a70c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551261"
---
# <a name="specifying-wdf-directives-in-inf-files"></a>INF ファイルで WDF ディレクティブの指定


このトピックでは、両方のユーザー モード ドライバー フレームワーク (UMDF) バージョン 1 と 2 に適用されます。

UMDF ドライバーをインストールする INF ファイルは、Microsoft Windows Driver Frameworks (WDF) を含める必要があります-特定*DDInstall*セクション。 WDF に固有の 1 つ以上を含めることができます、INF ファイル*DDInstall*セクションの場合は、INF ファイルには、1 つ以上の WDF ドライバーがインストールされます。 各 WDF 固有*DDInstall*セクション。

-   対応する、 [ **DDInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff547344)と[ **DDInstall.Services** ](https://msdn.microsoft.com/library/windows/hardware/ff547349)セクションでは特定の WDF ドライバーに関連付けられています。

-   すべての読み込まれた WDF co-installer、任意の順序で実行されるによって処理されます。

-   デバイスの WDF のインストールのディレクティブが含まれています。 UMDF 固有のディレクティブは、UMDF プレフィックスで始まるし、KMDF 固有のディレクティブは、KMDF プレフィックスで始まります。

次のコード例は、WDF 固有の UMDF 固有のディレクティブを示します*DDInstall*セクション。

```cpp
[Skeleton_Install.Wdf]
UmdfService=UMDFSkeleton,UMDFSkeleton_Install
UmdfServiceOrder=UMDFSkeleton
```

WDF 固有では、各 UMDF 固有ディレクティブ*DDInstall*セクションは、次の一覧で説明します。

<a href="" id="umdfservice----servicename----sectionname-"></a>**UmdfService** = &lt;*serviceName*&gt;、 &lt; *sectionName*&gt;  
UMDF ドライバーを関連付けます、 *UMDF サービス-インストール*UMDF ドライバーをインストールするために必要な情報が含まれるセクション。 *ServiceName*パラメーター、UMDF ドライバーを指定します、31 文字の長さの最大数に制限されています。 *SectionName*パラメーターの参照、 *UMDF サービス-インストール*セクション。 有効な INF ファイルが通常 1 つ以上必要**UmdfService**ディレクティブ。 ただし、UMDF ドライバー、オペレーティング システムの一部である場合、 **UmdfService** UMDF ドライバーのディレクティブは必要ありません。 そのため、有効な INF ファイルいない**UmdfService**ディレクティブでは、ほとんどの INF ファイルが 1 つ**UmdfService** UMDF ドライバーごとにディレクティブ。

<a href="" id="umdfhostprocesssharing-------------processsharingdisabled---processsharingenabled-"></a>**UmdfHostProcessSharing** = &lt;**ProcessSharingDisabled** | **ProcessSharingEnabled**&gt;  
デバイス スタックを共有プロセス プールに配置するかどうかを決定します (**ProcessSharingEnabled**) または独自の個別のプロセス (**ProcessSharingDisabled**)。 既定値は**ProcessSharingEnabled**します。 このディレクティブは、ドライバー固有ではなく、デバイスに固有です。

デバイスのプールに関する詳細については、次を参照してください。[デバイスの UMDF ドライバーでプールを使用して](using-device-pooling-in-umdf-drivers.md)します。

UMDF バージョン 1.11 以降をサポート、 **UmdfHostProcessSharing**ディレクティブ。

<a href="" id="umdfdirecthardwareaccess----allowdirecthardwareaccess---rejectdirecthardwareaccess---"></a>**UmdfDirectHardwareAccess** = &lt;**AllowDirectHardwareAccess** | **RejectDirectHardwareAccess**&gt;   
フレームワークがへのアクセスのデバイスの登録などの直接ハードウェア アクセス機能を使用するドライバーとハードウェアの割り込みを処理または接続を取得する、デバイスに割り当てられたハードウェア リソースをスキャンするポートを許可するかどうかを指定します。リソース。

場合**UmdfDirectHardwareAccess**に設定されている**AllowDirectHardwareAccess**、フレームワークにより、ハードウェアに直接アクセスを実行する UMDF インターフェイスを使用するドライバー。

指定する必要があります**AllowDirectHardwareAccess** UMDF ドライバー レジスタまたはポート、割り込みなどのハードウェア リソースにアクセスする場合[汎用 I/O](https://msdn.microsoft.com/library/windows/hardware/hh439512) (GPIO) ピン、またはこのようなシリアル バス接続I2C、SPI、およびシリアル ポート。 ドライバーをすべてを通じてこれらのリソース受信、 *ResourcesRaw*と*ResourcesTranslated*のパラメーターの[ *EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数。

**注**   UMDF 2.15 バージョン以降、UMDF ドライバーは指定する必要ありません**AllowDirectHardwareAccess**でリストするハードウェア リソースを受信するためにその[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック ルーチン。 指定しない場合、ドライバーには、これらのリソースを使用して、1 つの例外へのアクセス権がありません。

デバイスが 1 つまたは複数の接続リソースを割り当てられている場合 (**CmResourceTypeConnection**) と 1 つまたは複数の割り込みリソース (**CmResourceTypeInterrupt**)、ドライバーを呼び出すことができます[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)からその[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック ルーチン (がからではなく[ *EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693))。

 

UMDF ドライバーを特定の種類のリソースに接続する方法についてを参照してください。

-   [UMDF ドライバーを GPIO I/O ピンに接続します。](https://msdn.microsoft.com/library/windows/hardware/hh698244)
-   [ユーザー モード SPB の周辺機器のドライバーのハードウェア リソース](https://msdn.microsoft.com/library/windows/hardware/hh450837)
-   [Sp B に接続されている周辺機器の接続 Id](https://msdn.microsoft.com/library/windows/hardware/hh698216)
-   [周辺機器の UMDF ドライバーをシリアル ポートに接続します。](https://msdn.microsoft.com/library/windows/hardware/hh406559)

場合**UmdfDirectHardwareAccess**に設定されている**RejectDirectHardwareAccess**フレームワークでは、ドライバーを直接ハードウェア アクセス機能を使用することはできません。 既定値は**RejectDirectHardwareAccess**します。

UMDF ドライバーがハードウェア リソースにアクセスする方法については、次を参照してください。[マッピング ハードウェア リソースの検索と](finding-and-mapping-hardware-resources.md)します。

UMDF バージョン 1.11 以降をサポート、 **UmdfDirectHardwareAccess**ディレクティブ。

<a href="" id="umdfhostpriority----priorityhigh-"></a>**UmdfHostPriority** = &lt;**PriorityHigh**&gt;  
クライアント ドライバーを設定できる UMDF UMDF HID 2.15 バージョン以降**UmdfHostPriority**に**PriorityHigh**そのスレッドの優先順位を上げる。 このディレクティブは、ユーザーの応答時間を区別できるタッチまたは入力のドライバのみに使用する必要があります。 ドライバーを指定すると**PriorityHigh**システムのような優先順位の他のドライバーとは別のデバイスのプール内に配置します。 追加のデバイスのプールより多くのメモリを使用するため、慎重にこの設定を使用する必要があります。 デバイスのプールに関する詳細については、次を参照してください。[デバイスの UMDF ドライバーでプールを使用して](using-device-pooling-in-umdf-drivers.md)します。

<a href="" id="umdfregisteraccessmode----registeraccessusingsystemcall---registeraccessusingusermodemapping--"></a>**UmdfRegisterAccessMode** = &lt;**RegisterAccessUsingSystemCall** | **RegisterAccessUsingUserModeMapping**&gt;   
フレームワークがユーザー モードのアドレスにレジスタにマップする必要があるかどうかを示します (レジスタへのアクセスでは、システムの呼び出しが含まれていない) するための領域、またはレジスタにアクセスするシステム コールを使用します。

場合**UmdfRegisterAccessMode**に設定されている**RegisterAccessUsingSystemCall**フレームワークでは、システム コールを使用して、レジスタにアクセスします。

場合**UmdfRegisterAccessMode**に設定されている**RegisterAccessUsingUserModeMapping**フレームワークはシステム コールがレジスタにアクセスする必要はありませんされるため、ユーザー モード アドレス空間にレジスタにマップします。 既定値は**RegisterAccessUsingSystemCall**します。

UMDF バージョン 1.11 以降をサポート、 **UmdfRegisterAccessMode**ディレクティブ。

<a href="" id="--------umdfserviceorder----servicename1------servicename2------"></a> **UmdfServiceOrder** = &lt;*serviceName1*&gt; \[, &lt;*serviceName2*&gt; ...\]  
共同インストーラーがデバイス スタックに UMDF ドライバーをインストールする順序を一覧表示します。 共同インストーラーは、デバイス スタックの 1 つだけの UMDF ドライバーをインストールする場合でも、INF ファイルは、このディレクティブを含める必要があります。 *ServiceNameXx*パラメーターに対応、 *serviceName*ごとパラメーター **UmdfService**ディレクティブ。 UMDF ドライバーは記載されている順序でデバイス スタックに追加するため、最初のパラメーターは、デバイス スタックの最下位の UMDF ドライバーを指定します。

UMDF 共同インストーラーが、デバイスは、1 つだけがインストールされることを確認する**UmdfServiceOrder**ディレクティブが必要である、特定の WDF 特定*DDInstall*セクション。 つまり、 **UmdfServiceOrder**ディレクティブを使用してインポートすることはできません、 **Include**と**必要がある**ディレクティブ。

<a href="" id="umdfimpersonationlevel----level-"></a>**UmdfImpersonationLevel** = &lt;*レベル*&gt;  
フレームワークを UMDF ドライバーができる最大の偽装レベルを通知します。 A **UmdfImpersonationLevel**ディレクティブは省略可能です。 偽装レベルが指定されていない場合、既定値は**識別**します。 アプリケーションでは、ファイル ハンドルが開いたら、アプリケーションは、ドライバーに大きい偽装レベルを付与できます。 ただし、ドライバーを呼び出すことはできません、 [ **IWDFIoRequest::Impersonate** ](https://msdn.microsoft.com/library/windows/hardware/ff559136)レベルの権限の借用を要求するメソッドが、レベルよりも大きいを**UmdfImpersonationLevel**を指定します。 このディレクティブを指定できる値は次のとおりです。

-   **匿名**

-   **識別**

-   **権限借用**

-   **委任**

これらの値で指定されている値に対応、 [**セキュリティ\_偽装\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560499)列挙体。

<a href="" id="umdfmethodneitheraction------------copy---reject-"></a>**UmdfMethodNeitherAction** = &lt;**コピー** | **拒否**&gt;  
フレームワークはそのまま使用するかどうかを示します (**コピー**) または拒否 (**拒否**) デバイスの I/O を要求する場合は、要求オブジェクトを指定する I/O 制御コードを含む、[メソッド\_NEITHER](https://msdn.microsoft.com/library/windows/hardware/ff540663)アクセス メソッドをバッファーします。 A **UmdfMethodNeitherAction**ディレクティブは省略可能です。 ディレクティブが指定されていない場合、既定値は**拒否**します。

メソッドのサポートの詳細については\_UMDF ベースのドライバーでどちらバッファーへのアクセス方法を確認する[I/O を使用していないバッファーも UMDF ドライバーでのダイレクト I/O](https://msdn.microsoft.com/library/windows/hardware/ff554413#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)します。

<a href="" id="umdfdispatcher----filehandle---winusb---nativeusb-"></a>**UmdfDispatcher** = &lt;**FileHandle** | **WinUsb** | **NativeUSB**&gt;  
I/O デバイス スタックのユーザー モードの部分を通過した後に、I/O を送信する場所をフレームワークに通知します。 既定では、I/O は、reflector (WUDFRd.sys) に送信されます。 設定して**UmdfDispatcher**に**WinUsb**ドライバーが UMDF WinUsb アーキテクチャに I/O を送信するように指示します。 UMDF 2.15 で始まる、指定する**NativeUSB** USB I/O を処理するために、reflector をによりします。

-   スタック内の任意のドライバーは、ファイル ハンドル ベースのターゲットを使用している場合にこのディレクティブを設定**FileHandle**します。
-   ドライバーが UMDF 2.15 またはそれ以降を使用して、USB I/O ターゲットを使用する場合にこのディレクティブを設定**NativeUSB**します。
-   場合は、ドライバーが事前 UMDF 2.15 USB I/O ターゲットを使用し、このディレクティブを設定**WinUsb**します。

A **UmdfDispatcher**ディレクティブは省略可能です。

次のコード例は、 **UmdfDispatcher** WDF 固有のディレクティブ**DDInstall**セクション。

```cpp
[Xxx_Install.Wdf]
UmdfDispatcher=NativeUSB
```

<a href="" id="umdfkernelmodeclientpolicy------------allowkernelmodeclients---rejectkernelmodeclients-"></a>**UmdfKernelModeClientPolicy** = &lt;**AllowKernelModeClients** | **RejectKernelModeClients**&gt;  
フレームワークがカーネル モード ドライバーからの I/O 要求を受信するドライバーを許可するかどうかを指定します。

場合**UmdfKernelModeClientPolicy**に設定されている**AllowKernelModeClients**フレームワークにより、ユーザー モード ドライバーでは、上記の読み込みにカーネル モード ドライバーやカーネル モード ドライバーからの I/O 要求を配信ユーザー モード ドライバー。

場合**UmdfKernelModeClientPolicy**に設定されている**RejectKernelModeClients**フレームワークでは、カーネル モード ドライバー ユーザー モード ドライバーでは、上記の読み込みにすることはできません、いずれかからの I/O 要求が含まれていませんユーザー モード ドライバーにカーネル モード ドライバーです。 ドライバーの INF ファイルにこのディレクティブが含まれていない場合、既定値は、 **RejectKernelModeClients**します。 詳細については、次を参照してください。[サポート カーネル モードのクライアント](https://msdn.microsoft.com/library/windows/hardware/ff561214)します。

UMDF バージョン 1.9 以降のサポート、 **UmdfKernelModeClientPolicy**ディレクティブ。 カーネル モード ドライバーを読み込む UMDF の以前のバージョンでのユーザー モード ドライバーの上位を許可するのを参照してください。 [UMDF の以前のバージョンのカーネル モードのクライアント サポート](https://msdn.microsoft.com/library/windows/hardware/ff561214#kernel-mode-client-support-in-earlier-umdf-versions)します。

<a href="" id="umdffileobjectpolicy----rejectnullandunknownfileobjects---allownullandunknownfileobjects--"></a>**UmdfFileObjectPolicy** = &lt;**RejectNullAndUnknownFileObjects** | **AllowNullAndUnknownFileObjects**&gt;   
フレームワークが I/O 要求の処理を許可するかどうかを指定 ([IWDFIoRequest](https://msdn.microsoft.com/library/windows/hardware/ff558985)) ことがいずれかに関連付けられていないファイル オブジェクト ([IWDFFile](https://msdn.microsoft.com/library/windows/hardware/ff558912)) に関連付けられた (未知のファイル オブジェクトまたはファイル オブジェクトをドライバーが以前は存在しなかった要求の作成) します。

場合**UmdfFileObjectPolicy**に設定されている**RejectNullAndUnknownFileObjects**フレームワークでは、NULL または不明なファイルのオブジェクトに関連付けられている要求の処理をすることはできません。

場合**UmdfFileObjectPolicy**に設定されている**AllowNullAndUnknownFileObjects**フレームワークがファイルを NULL または不明なオブジェクトに関連付けられている要求の処理を許可します。

既定値は**RejectNullAndUnknownFileObjects**します。

UMDF バージョン 1.11 以降をサポート、 **UmdfFileObjectPolicy**ディレクティブ。

<a href="" id="umdffscontextusepolicy----canusefscontext---canusefscontext2----cannotusefscontexts-"></a>**UmdfFsContextUsePolicy** = &lt;**CanUseFsContext** | **CanUseFsContext2**  |  **CannotUseFsContexts**&gt;  
WDM ファイル オブジェクトのメンバーを特定のコンテキストで、フレームワークが内部の情報を格納できるかどうかを示します。 同じスタックでのカーネル モード ドライバーでは、ファイル オブジェクトの特定のメンバーを使用している場合は、フレームワークでは、同じ場所を使用しないことを要求するこのディレクティブを使用することができます。

場合**UmdfFsContextUsePolicy**に設定されている**CanUseFsContext**、情報を格納するために、フレームワーク、 **FsContext** WDM ファイル オブジェクトのメンバー。

場合**UmdfFsContextUsePolicy**に設定されている**CanUseFsContext2**、情報を格納するために、フレームワーク、 **FsContext2** WDM ファイル オブジェクトのメンバー。

場合**UmdfFsContextUsePolicy**に設定されている**CannotUseFsContexts**、フレームワークで使用するかしない**FsContext**または**FsContext2**します。

既定値は**CanUseFsContext**します。

UMDF バージョン 1.11 以降をサポート、 **UmdfFsContextUsePolicy**ディレクティブ。




次のコード例で必要なディレクティブを示しています、 *UMDF サービス-インストール*セクション。

```cpp
[UMDFSkeleton_Install]
UmdfLibraryVersion=1.0.0
ServiceBinary=%12%\UMDF\UMDFSkeleton.dll
DriverCLSID={d4112073-d09b-458f-a5aa-35ef21eef5de}
```

各ディレクティブに、 *UMDF サービス-インストール*セクションは、次の一覧で説明。

<a href="" id="umdflibraryversion------------version-"></a>**UmdfLibraryVersion** = &lt;*バージョン*&gt;  
UMDF ドライバーを使用するフレームワークのバージョン番号については、共同インストーラーを通知します。 形式、*バージョン*文字列が&lt;*メジャー*&gt;.&lt;*マイナー*&gt;.&lt;*サービス*&gt;します。 デバイス スタック上のドライバーは、1 つ以上のバージョンの framework を使用して、INF ファイルは、複数の共同インストーラー----各フレームワークのバージョンのいずれかをハード ディスク ドライブ上の同じ場所にコピーします。 ただし、INF ファイルが追加、最高バージョン共同インストーラーのみを**CoInstallers32**レジストリ値。 共同インストーラーをコピーする方法の詳細については、次を参照してください。 [UMDF 共同インストーラーを使用して](using-the-umdf-co-installer.md)します。

共同インストーラーは、バージョン文字列を確認し、UMDF ドライバーのバージョンに固有の共同インストーラーの検索に使用します。 次に、共同インストーラーは、バージョン固有の共同インストーラーからフレームワークを抽出します。

<a href="" id="servicebinary----binarypath-"></a>**ServiceBinary** = &lt;*binarypath*&gt;  
ハード ディスク ドライブの UMDF ドライバーのバイナリを配置する場所については、UMDF を通知します。

UMDF ドライバーのコピー先と、そこから起動する必要があります、 \\Windows\\System32\\ドライバー\\UMDF ディレクトリ。

<a href="" id="driverclsid-----clsid--"></a>**DriverCLSID** = &lt;{*CLSID*}&gt;  
**注**  このディレクティブは、UMDF バージョン 1.11 以降。

UMDF は、UMDF ドライバーのクラス id (CLSID) を通知します。 UMDF ホストが、UMDF ドライバーの CLSID を使用して、UMDF のインスタンスを作成する UMDF ドライバーが読み込まれる UMDF ドライバーの[IDriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff554885)インターフェイス。

<a href="" id=" umdfextensions-----cxservicename--"></a>**UmdfExtensions** = &lt;cxServiceName&gt; Microsoft によって提供されるクラスの拡張機能ドライバーをドライバーと通信するために必要です。  CxServiceName パラメーターは、クラスの拡張機能ドライバーをバイナリに関連付けられているサービスに対応します。

クラスの拡張機能ドライバーのサービス名は、次のレジストリ キーの下のサブキーとして見つかりませんでした。**Hkey_local_machine \software\microsoft\windows NT\CurrentVersion\WUDF\Services**

Windows 8.1 以前で必要な再起動を避けるためには、UMDF ドライバーを更新するときに、指定、 **COPYFLG\_IN\_使用\_の名前を変更**フラグ、 [ **CopyFilesディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)でこの例で示すように、ドライバーの INF ファイル。

```cpp
[VirtualSerial_Install.NT]
CopyFiles=UMDriverCopy
 
[UMDriverCopy]
Virtualserial.dll,,,0x00004000  ; COPYFLG_IN_USE_RENAME
```

 

 





