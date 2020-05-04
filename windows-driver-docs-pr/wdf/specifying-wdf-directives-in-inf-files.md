---
title: INF ファイルでの WDF ディレクティブの指定
description: INF ファイルでの WDF ディレクティブの指定
ms.assetid: aefc678e-dc81-47dc-a84b-f1a79c16cad9
keywords:
- WDF ディレクティブ WDK UMDF
- DDInstall セクション WDK UMDF
- UmdfService INF ディレクティブ WDK UMDF
- UmdfServiceOrder INF ディレクティブ WDK UMDF
- UmdfImpersonationLevel INF ディレクティブ WDK UMDF
- UmdfMethodNeitherAction INF ディレクティブ WDK UMDF
- Umdfカーネル Modeclientpolicy INF ディレクティブ WDK UMDF
- UmdfLibraryVersion INF ディレクティブ WDK UMDF
- ServiceBinary INF ディレクティブ WDK UMDF
- DriverCLSID INF ディレクティブ WDK UMDF
- ディレクティブ WDK UMDF
- UMDF 固有のディレクティブ WDK
- UMDF サービス-インストールセクション WDK
- INF ファイル WDK UMDF、ディレクティブ
- UmdfDispatcher INF ディレクティブ WDK UMDF、構文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa299b109c31e40bfd7e089b00df42c82b401e5
ms.sourcegitcommit: feee956dcf5581e7564430101d81ff928ec28a3b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82188459"
---
# <a name="specifying-wdf-directives-in-inf-files"></a>INF ファイルでの WDF ディレクティブの指定


このトピックは、ユーザーモードドライバーフレームワーク (UMDF) バージョン1と2の両方に適用されます。

UMDF ドライバーをインストールする INF ファイルには、Microsoft Windows Driver Framework (WDF) 固有の*Ddinstall*セクションが含まれている必要があります。 Inf ファイルに複数の WDF ドライバーがインストールされている場合は、INF ファイルに複数の WDF 固有の*Ddinstall*セクションを含めることができます。 各 WDF 固有の*Ddinstall*セクション:

-   特定の WDF ドライバーに関連付けられている[**ddinstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)および[**Ddinstall. Services**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)セクションに対応します。

-   は、任意の順序で実行される、読み込まれたすべての WDF 共同インストーラーによって処理されます。

-   デバイスの WDF インストールディレクティブが含まれています。 UMDF 固有のディレクティブは、UMDF プレフィックスで始まり、KMDF 固有のディレクティブは KMDF プレフィックスで始まります。

次のコード例は、WDF 固有の*Ddinstall*セクションにある、UMDF 固有のディレクティブを示しています。

```cpp
[Skeleton_Install.Wdf]
UmdfService=UMDFSkeleton,UMDFSkeleton_Install
UmdfServiceOrder=UMDFSkeleton
```

WDF 固有の*Ddinstall*セクションの各 UMDF 固有のディレクティブについては、このページで説明しています。 右側にあるこの記事のリンクを使用して、ディレクティブ間を移動できます。

## <a name="umdfservice"></a>UmdfService

`**Umdfservice** = <*serviceName*>、<*sectionname*>

Umdf ドライバーをインストールするために必要な情報が含まれている、umdf *service-install*セクションに関連付けられています。 *ServiceName*パラメーターは、UMDF ドライバーを指定し、最大31文字に制限されています。 *Sectionname*パラメーターは、 *UMDF service-install*セクションを参照します。 有効な INF ファイルには、通常、少なくとも1つの**Umdfservice**ディレクティブが必要です。 ただし、UMDF ドライバーがオペレーティングシステムの一部である場合は、UMDF ドライバーの**Umdfservice**ディレクティブは必要ありません。 したがって、有効な INF ファイルには**Umdfservice**ディレクティブがない場合がありますが、ほとんどの inf ファイルには、各 UMDF ドライバーに対して1つの**umdfservice**ディレクティブがあります。

## <a name="umdfhostprocesssharing"></a>UmdfHostProcessSharing

*このディレクティブは、UMDF バージョン1.11 以降でサポートされています。*

**Umdfhostprocesssharing** = <**processsharingdisabled** | **processsharingenabled**>


デバイススタックを共有プロセスプール (**Processsharingenabled**) に配置するか、独自の個別のプロセス (**processsharingenabled**) に配置するかを決定します。 既定値は**Processsharingenabled**です。 このディレクティブは、ドライバー固有ではなく、デバイス固有です。

デバイスプールの詳細については、「 [UMDF ドライバーでのデバイスプールの使用](using-device-pooling-in-umdf-drivers.md)」を参照してください。


## <a name="umdfdirecthardwareaccess"></a>UmdfDirectHardwareAccess

*このディレクティブは、UMDF バージョン1.11 以降でサポートされています。*

**UmdfDirectHardwareAccess** = <**AllowDirectHardwareAccess** | **RejectDirectHardwareAccess**> 

フレームワークで、デバイスのレジスタやポートへのアクセス、デバイスに割り当てられたハードウェアリソースのスキャン、ハードウェア割り込みの処理、接続リソースの取得など、直接のハードウェアアクセス機能を使用できるようにする必要があるかどうかを示します。

**UmdfDirectHardwareAccess**が**AllowDirectHardwareAccess**に設定されている場合、このフレームワークは、ドライバーが直接ハードウェアアクセスを実行する UMDF インターフェイスを使用できるようにします。

UMDF ドライバーが、レジスタ、ポート、割り込み、[汎用 i/o](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview) (GPIO) ピン、または I2C、SPI、シリアルポートなどのシリアルバス接続などのハードウェアリソースにアクセスする場合は、 **AllowDirectHardwareAccess**を指定する必要があります。 ドライバーは、 [*EvtdeviceResourcesTranslated ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数の*Resourcesraw*パラメーターと*ResourcesTranslated*パラメーターを使用して、これらのリソースをすべて受信します。

> [!NOTE]
> UMDF バージョン2.15 以降では、UMDF ドライバーは、 [*EvtdeviceAllowDirectHardwareAccess ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバックルーチンでハードウェアリソースリストを受信するために、ハードウェアリソースリストを指定する必要はありません。 **AllowDirectHardwareAccess** 指定しない場合、ドライバーはこれらのリソースを使用するためのアクセス権を持っていません。ただし、1つのデバイスに1つ[*以上の接続*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)リソース (**CmResourceTypeConnection**) と1つ以上の割り込みリソース (**cmresourcetypeinterrupt**) が割り当てられている場合、ドライバーは[*evtdevice ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバックルーチンから[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)を呼び出すことができます

 

UMDF ドライバーを特定の種類のリソースに接続する方法の詳細については、以下を参照してください。

-   [UMDF ドライバーを GPIO i/o ピンに接続する](https://docs.microsoft.com/windows-hardware/drivers/gpio/connecting-a-umdf-driver-to-gpio-i-o-pins)
-   [ユーザーモード SPB 周辺機器ドライバーのハードウェア リソース](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers)
-   [SPB 接続周辺機器の接続 ID](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)
-   [UMDF 周辺機器ドライバーをシリアル ポートに接続する](https://docs.microsoft.com/previous-versions/hh406559(v=vs.85))

**UmdfDirectHardwareAccess**が**RejectDirectHardwareAccess**に設定されている場合、このフレームワークでは、ドライバーが直接ハードウェアアクセス機能を使用することを許可していません。 既定値は**RejectDirectHardwareAccess**です。

UMDF ドライバーがハードウェアリソースにアクセスする方法の詳細については、「[ハードウェアリソースの検索とマッピング](finding-and-mapping-hardware-resources.md)」を参照してください。


## <a name="umdfhostpriority"></a>UmdfHostPriority

*このディレクティブは、UMDF バージョン2.15 以降でサポートされています。*

**Umdfhostpriority** = <優先度**高**>  

UMDF HID クライアントドライバーでは、 **Umdfhostpriority**を優先順位**high**に設定して、スレッドの優先度を上げることができます。 このディレクティブは、ユーザーの応答時間に敏感なタッチドライバーまたは入力ドライバーに対してのみ使用してください。 ドライバーで優先順位**が指定さ**れている場合、システムは別のデバイスプールに同様の優先順位の他のドライバーと共に配置します。 追加のデバイスプールではより多くのメモリが使用されるため、この設定は慎重に行う必要があります。 デバイスプールの詳細については、「 [UMDF ドライバーでのデバイスプールの使用](using-device-pooling-in-umdf-drivers.md)」を参照してください。

## <a name="umdfregisteraccessmode"></a>UmdfRegisterAccessMode

*このディレクティブは、UMDF バージョン1.11 以降でサポートされています。*

**Umdfregisteraccessmode** = <**registeraccessRegisterAccessUsingUserModeMapping systemcall** | **RegisterAccessUsingUserModeMapping**>   

フレームワークがレジスタをユーザーモードアドレス空間にマップする必要があるかどうかを示します (システムコールがレジスタへのアクセスに関与しないようにするため)。または、システム呼び出しを使用してレジスタにアクセスします。

**Umdfregisteraccessmode**が**Registeraccessuses systemcall**に設定されている場合、フレームワークはシステム呼び出しを使用してレジスタにアクセスします。

**Umdfregisteraccessmode**が**RegisterAccessUsingUserModeMapping**に設定されている場合、フレームワークはレジスタをユーザーモードのアドレス空間にマップします。これにより、レジスタにアクセスするためにシステムコールが不要になります。 既定値は**Registeraccessで Systemcall**です。


##  <a name="umdfserviceorder"></a>UmdfServiceOrder

**Umdfserviceorder** = <*serviceName1*> \[、<*serviceName2*>...\]  

共同インストーラーによって、デバイススタックに UMDF ドライバーがインストールされる順序が一覧表示されます。 共同インストーラーによってデバイススタックに UMDF ドライバーが1つだけインストールされている場合でも、INF ファイルにはこのディレクティブが含まれている必要があります。 *ServiceNameXx*パラメーターは、各**umdfservice**ディレクティブの*serviceName*パラメーターに対応します。 UMDF ドライバーは、一覧表示されている順序でデバイススタックに追加されるため、最初のパラメーターでは、デバイススタック内の最も下位の UMDF ドライバーを指定します。

UMDF 共同インストーラーによってデバイスがインストールされるようにするには、特定の WDF 固有の*Ddinstall*セクションに**Umdfserviceorder**ディレクティブを1つだけ指定する必要があります。 つまり、 **Umdfserviceorder**ディレクティブは、 **Include**ディレクティブおよび**必要**なディレクティブを使用してインポートすることはできません。

## <a name="umdfimpersonationlevel"></a>UmdfImpersonationLevel

**UmdfImpersonationLevel** = <*レベル*>  

UMDF ドライバーが持つことができる最大偽装レベルをフレームワークに通知します。 **UmdfImpersonationLevel**ディレクティブは省略可能です。偽装レベルが指定されていない場合、既定値は**id**です。 アプリケーションがファイルハンドルを開くと、アプリケーションは、より高度な偽装レベルをドライバーに付与できます。 ただし、ドライバーは[**IWDFIoRequest:: Impersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-impersonate)メソッドを呼び出して、 **UmdfImpersonationLevel**が指定したレベルよりも高い偽装レベルを要求することはできません。 このディレクティブに指定できる値は次のとおりです。

-   **Anonymous**

-   **[識別]**

-   **偽造**

-   **処理の代行**

これらの値は、 [**\_セキュリティ偽装\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/ne-wudfddi-_security_impersonation_level)の列挙に指定されている値に対応します。

## <a name="umdfmethodneitheraction"></a>Umdfmethodneiand Action

**Umdfmethodneiruncommand action** = <**コピー** | **拒否**>  

[メソッド\_](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)をバッファーアクセス方法として指定しない i/o 制御コードが要求オブジェクトに含まれている場合に、デバイスの i/o 要求を受け入れる (**コピー**する) か拒否する (**拒否**する) かを示します。 **Umdfmethodneitheraction**ディレクティブは省略可能です。 ディレクティブが指定されていない場合、既定値は**Reject**です。

UMDF ベースのドライバーのバッファーアクセス\_メソッドではないメソッドをサポートする方法の詳細については、「 [umdf ドライバーでのバッファリングされた i/o と直接 I/o の両方を使用する](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)」を参照してください。

## <a name="umdfdispatcher"></a>UmdfDispatcher

**Umdfdispatcher** = <**FileHandle** | **winusb** | の場合**usb**>  

I/o がデバイススタックのユーザーモード部分を通過した後に i/o を送信する場所をフレームワークに通知します。 既定では、i/o はリフレクタ (WUDFRd .sys) に送信されます。 **Umdfdispatcher**を**winusb**に設定することにより、ドライバーは UMDF に対して winusb アーキテクチャに i/o を送信するように指示します。 UMDF 2.15 以降では、型の**usb**を指定すると、リフレクターで usb i/o が処理されます。

-   スタック内のいずれかのドライバーがファイルハンドルベースのターゲットを使用している場合は、このディレクティブを**FileHandle**に設定します。
-   ドライバーが UMDF 2.15 以降を使用していて、USB i/o**ターゲットを使用**している場合は、このディレクティブを "を" に設定します。
-   ドライバーが UMDF 2.15 であり、USB i/o ターゲットを使用している場合は、このディレクティブを**Winusb**に設定します。

**Umdfdispatcher**ディレクティブは省略可能です。

次のコード例は、WDF 固有の**Ddinstall**セクションの**umdfdispatcher**ディレクティブを示しています。

```cpp
[Xxx_Install.Wdf]
UmdfDispatcher=NativeUSB
```

## <a name="umdfkernelmodeclientpolicy"></a>Umdfカーネル Modeclientpolicy

*このディレクティブは、UMDF バージョン1.9 以降でサポートされています。*

**Umdfカーネル modeclientpolicy** = <**allowkernelmodeclients** | **RejectKernelModeClients**>  

以前のバージョンの UMDF でカーネルモードドライバーがユーザーモードドライバーより上に読み込まれるようにするには、[以前のバージョンの umdf でのカーネルモードクライアントのサポート](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-kernel-mode-clients-in-umdf-1-x-drivers#kernel-mode-client-support-in-earlier-umdf-versions)に関する説明を参照してください。

カーネルモードドライバーからの i/o 要求を、フレームワークが受信できるようにする必要があるかどうかを示します。

**Umdfo Modeclientpolicy**が**allowに**設定されている場合、このフレームワークにより、カーネルモードドライバーがユーザーモードドライバーの上に読み込まれ、カーネルモードドライバーからユーザーモードドライバーに i/o 要求が配信されます。

**Umdfo Modeclientpolicy**が**RejectKernelModeClients**に設定されている場合、フレームワークはカーネルモードドライバーがユーザーモードドライバーの上に読み込まれることを許可しません。また、カーネルモードドライバーからユーザーモードドライバーへの i/o 要求を配信しません。 ドライバーの INF ファイルにこのディレクティブが含まれていない場合、既定値は**RejectKernelModeClients**です。 詳細については、「[カーネルモードクライアントのサポート](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-kernel-mode-clients-in-umdf-1-x-drivers)」を参照してください。


## <a name="umdffileobjectpolicy"></a>UmdfFileObjectPolicy

*このディレクティブは、UMDF バージョン1.11 以降でサポートされています。*

**Umdffileobjectpolicy** = <**RejectNullAndUnknownFileObjects** | **AllowNullAndUnknownFileObjects**>   

フレームワークで、ファイルオブジェクト ([Iwdffile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)) に関連付けられていない、または不明なファイルオブジェクト (ドライバーが以前に作成要求を検出していないファイルオブジェクト) に関連付けられている i/o 要求 ([IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)) の処理を許可する必要があるかどうかを示します。

**Umdffileobjectpolicy**が**RejectNullAndUnknownFileObjects**に設定されている場合、フレームワークは、NULL または不明なファイルオブジェクトに関連付けられている要求の処理を許可しません。

**Umdffileobjectpolicy**が**AllowNullAndUnknownFileObjects**に設定されている場合、フレームワークは、NULL または不明なファイルオブジェクトに関連付けられている要求の処理を許可します。

既定値は**RejectNullAndUnknownFileObjects**です。


## <a name="umdffscontextusepolicy"></a>UmdfFsContextUsePolicy

*このディレクティブは、UMDF バージョン1.11 以降でサポートされています。*

**UmdfFsContextUsePolicy** = <**canusefscontext** | **CanUseFsContext2** | **CannotUseFsContexts**> 

フレームワークが、WDM ファイルオブジェクトの特定のコンテキストメンバーに内部情報を格納できるかどうかを示します。 同じスタック内のカーネルモードドライバーが file オブジェクトの特定のメンバーを使用する場合、このディレクティブを使用して、フレームワークが同じ場所を使用しないように要求することができます。

**UmdfFsContextUsePolicy**が**Canusefscontext**に設定されている場合、フレームワークは WDM ファイルオブジェクトの**fscontext**メンバーに情報を格納します。

**UmdfFsContextUsePolicy**が**CanUseFsContext2**に設定されている場合、フレームワークは、WDM ファイルオブジェクトの**FsContext2**メンバーに情報を格納します。

**UmdfFsContextUsePolicy**が**CannotUseFsContexts**に設定されている場合、フレームワークでは**fscontext**も**FsContext2**も使用されません。

既定値は**Canusefscontext**です。


次のコード例は、「 *UMDF service-install* 」セクションの必須ディレクティブを示しています。

```cpp
[UMDFSkeleton_Install]
UmdfLibraryVersion=1.0.0
ServiceBinary=%12%\UMDF\UMDFSkeleton.dll
DriverCLSID={d4112073-d09b-458f-a5aa-35ef21eef5de}
```

「 *UMDF-service-install* 」セクションの各ディレクティブについて、次の一覧で説明します。

## <a name="umdflibraryversion"></a>UmdfLibraryVersion

**Umdflibraryversion** = <*バージョン*>  

UMDF ドライバーが使用するフレームワークのバージョン番号について、共同インストーラーに通知します。 *バージョン*文字列の形式は、*メジャー*> <ます。 <の*マイナー*> <*サービス*>。 デバイススタックのドライバーで複数のバージョンのフレームワークが使用されている場合、INF ファイルによって複数の共同インストーラー (フレームワークのバージョンごとに1つ) がハードディスクドライブ上の同じ場所にコピーされます。 ただし、INF ファイルでは、最新バージョンの共同インストーラーだけが**CoInstallers32**レジストリ値に追加されます。 共同インストーラーのコピーの詳細については、「 [UMDF 共同インストーラーの使用](using-the-umdf-co-installer.md)」を参照してください。

共同インストーラーは、バージョン文字列を検証し、それを使用して、UMDF ドライバーのバージョン固有の共同インストーラーを検索します。 その後、共同インストーラーによって、バージョン固有の共同インストーラーからフレームワークが抽出されます。

## <a name="servicebinary"></a>ServiceBinary

**Servicebinary** = <*binarypath*>  

Umdf ドライバーのバイナリをハードディスクドライブに配置する場所について、UMDF に通知します。

UMDF ドライバーは、 `Windows\System32\Drivers\UMDF`ディレクトリにコピーして、ディレクトリから実行する必要があります。

## <a name="driverclsid"></a>DriverCLSID

**注**  このディレクティブは、1.x の1.x バージョンでのみサポートされています。

**Driverclsid** = < {*clsid*} >  

Umdf ドライバーのクラス識別子 (CLSID) について、UMDF に通知します。 Umdf が UMDF ドライバーを読み込むと、umdf ホストは UMDF ドライバーの CLSID を使用して、UMDF ドライバーの[Idriverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)インターフェイスのインスタンスを作成します。

## <a name="umdfextensions"></a>UmdfExtensions

**Umdfextensions** = <*cxservicename*>  

Microsoft によって提供されるクラス拡張ドライバーと通信するドライバーに必要です。  CxServiceName パラメーターは、クラス拡張ドライバーバイナリに関連付けられているサービスに対応しています。

クラス拡張ドライバーのサービス名は、次のレジストリキーの下にサブキーとして配置されている可能性があります: **HKEY_LOCAL_MACHINE \Software\microsoft\windows NT\CurrentVersion\WUDF\Services**
