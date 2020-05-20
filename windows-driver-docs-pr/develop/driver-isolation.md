---
title: ドライバー パッケージの分離
description: このページでは、Windows ドライバーの要件であるドライバーの分離について説明します。
ms.date: 10/01/2019
ms.assetid: 3955fb29-ee49-4c3e-ac6d-700dcba3f884
ms.localizationpriority: medium
ms.openlocfilehash: e6b6b1704252cd436ba137f939f09d48818cd65e
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235323"
---
# <a name="driver-package-isolation"></a>ドライバー パッケージの分離

ドライバー パッケージの分離は、外部の変更に対するドライバーの回復性を高め、更新を容易にし、インストールをよりわかりやすいものにする、Windows ドライバーの要件です。

> [!NOTE]
> ドライバー パッケージの分離は Windows ドライバーで必須ですが、Windows デスクトップ ドライバーでも回復性とサービス性の向上を通じてメリットが得られます。

次の表では、Windows ドライバーで使用できなくなった従来のドライバー手法を左の列に、Windows ドライバーで必須の動作を右の列に示します。

|分離されていないドライバー|分離されているドライバー|
|-|-|
|INF でファイルを System32\drivers にコピーする|ドライバー ファイルはドライバー ストアから実行される|
|ハードコーディングされたパスを使用して他のドライバーと対話する|システムが提供する関数またはデバイス インターフェイスを使用して他のドライバーと対話する|
|パスをグローバルなレジストリの場所にハードコーディングする|レジストリの相対的な場所とファイルの状態を指定するために、HKR とシステムが提供する関数を使用する|
|ランタイム ファイルは任意の場所に書き込まれる|ドライバーはシステムが提供する場所にファイルを書き込む|


## <a name="run-from-driver-store"></a>ドライバー ストアから実行する

分離されているすべてのドライバー パッケージでは、ドライバー パッケージ ファイルがドライバー ストアに配置されます。 つまり、インストール時のドライバー パッケージ ファイルの場所を指定するため、INF に [**DIRID 13**](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids) と指定されるということです。

ドライバー ストアから実行されているカーネル モード ドライバーは、[**IoQueryFullDriverPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioqueryfulldriverpath) を呼び出してそのパスを使用し、パスを基準として構成ファイルを見つけます。  カーネル モード ドライバーが KMDF ドライバーの場合、[**WdfDriverWdmGetDriverObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverwdmgetdriverobject) を使用して、IoQueryFullDriverPath に渡す WDM ドライバー オブジェクトを取得できます。 UMDF ドライバーは、[**GetModuleHandleExW**](https://docs.microsoft.com/windows/desktop/api/libloaderapi/nf-libloaderapi-getmodulehandleexw) および [**GetModuleFileNameW**](https://docs.microsoft.com/windows/desktop/api/libloaderapi/nf-libloaderapi-getmodulefilenamew) を使用してドライバーがどこから読み込まれたかを特定できます。  たとえば、次のように入力します。

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

ドライバー ストアから実行されていて、ドライバー パッケージの他のファイルにアクセスする必要がある WDM または KMDF ドライバーでは、[**IoQueryFullDriverPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioqueryfulldriverpath) を使用してそのパスを見つけ、読み込み元のディレクトリ パスを取得し、そのパスから見て相対的な場所にある構成ファイルを探します。

あるいは、Windows 10 バージョン 1803 以降では、ディレクトリの種類として *DriverDirectoryImage* を指定して [**IoGetDriverDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdriverdirectory) を呼び出し、ドライバーの読み込み元であるディレクトリ パスを取得します。

INF によってペイロードされたファイルの場合、INF 内のそのファイルに対する [**SourceDisksFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section) エントリにリストされている *subdir* は、INF 内の同じファイルに対する [**DestinationDirs**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section) エントリにリストされている subdir と一致している必要があります。

また、[**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive) ディレクティブをファイルの名前を変更するために使用することはできません。 こうした制限が必要なのは、デバイスへの INF のインストールによって DriverStore ディレクトリに新しいファイルが作成されないようにするためです。

[**SourceDisksFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section) エントリにファイル名が同じ複数のエントリを含めることはできず、かつ CopyFiles をファイルの名前変更に使用することはできないため、INF が参照する各ファイルは、一意のファイル名を持つ必要があります。

### <a name="dynamically-finding-and-loading-files-from-the-driver-store"></a>ドライバー ストアから動的にファイルを見つけて読み込む

ドライバー パッケージには、別のドライバー パッケージのバイナリまたはユーザー モード コンポーネントによって読み込まれるファイルが含まれている場合があります。

次にいくつかの例を示します。

* ユーザー モード DLL が、ドライバー パッケージ内のドライバーと通信するためのインターフェイスを提供する。
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

前の例では、空のフラグ値が使用されているため、REG_SZ レジストリ値になります。 これにより、 **%13%** が完全修飾ユーザー モード ファイル パスに変換されます。 多くの場合、このパスは環境変数の相対パスであることが望ましいです。 フラグ値 **0x20000** を使用すると、レジストリ値はタイプ REG_EXPAND_SZ となり、 **%13%** は適切な環境変数で変換され、パスの場所が抽象化されます。 このレジストリ値を取得する場合、[**ExpandEnvironmentStrings**](https://docs.microsoft.com/windows/desktop/api/rrascfg/nn-rrascfg-ieapproviderconfig) を呼び出して、パスの環境変数を解決します。

カーネル モード コンポーネントによってこの値を読み取る必要がある場合、値は REG_SZ 値でなければなりません。 カーネル モード コンポーネントはこの値を読み取るときに、先頭に `\??\` を付けてから、[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenfile) などの API に渡す必要があります。

この設定がデバイスの状態の一部である場合にアクセスするには、まずアプリケーションはデバイスの ID を検索する必要があります。  ユーザー モード コードでは、[**CM_Get_Device_ID_List_Size**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_list_sizea) および [**CM_Get_Device_ID_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_lista) を使用してデバイスの一覧 (必要に応じて、フィルタ適用) を取得できます。 このデバイスの一覧には複数のデバイスが含まれている場合があるため、デバイスから状態を読み取る前に、適切なデバイスを検索します。 たとえば、特定の条件に一致するデバイスを検索するときに、[**CM_Get_DevNode_Property**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_propertyw) を呼び出して、そのデバイスのプロパティを取得します。

適切なデバイスが見つかったら、[**CM_Open_DevNode_Key**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key) を呼び出して、デバイスの状態が格納されたレジストリの場所へのハンドルを取得します。

カーネル モード コードでは、PDO (物理デバイス オブジェクト) を取得し、[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey) を呼び出す必要があります。

デバイス インターフェイスの状態の場合にこの設定にアクセスするために、ユーザー モード コードで [**CM_Get_Device_Interface_List_Size**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_list_sizea) および [**CM_Get_Device_Interface_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista) を呼び出すことができます。

また、デバイス インターフェイスの接続や削除の通知を受けるために、[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification) を使用できます。これにより、コードではインターフェイスが有効化されたときに通知を受け、状態を取得できます。 上記の API で使用されるデバイス インターフェイス クラスには、複数のデバイス インターフェイスがある可能性があります。  これらのインターフェイスを確認し、設定を読み込むために適切なインターフェイスを特定します。

適切なインターフェイスが見つかったら、[**CM_Open_Device_Interface_Key**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_open_device_interface_keyw) を呼び出します。

カーネル モード コードでは、状態を取得するデバイス インターフェイスのシンボリック リンク名を取得できます。 そのためには、[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification) を呼び出して、適切なデバイス インターフェイス クラスでデバイス インターフェイス通知に登録します。  別の方法として、システム上の現在のデバイス インターフェイスの一覧を取得するために [**IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) を呼び出すこともできます。  上記の API で使用されるデバイス インターフェイス クラスには、複数のデバイス インターフェイスがある可能性があります。  これらのインターフェイスを確認し、読み込まれる設定を持つ適切なインターフェイスを特定します。

適切なシンボリック リンク名が見つかったら、[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) を呼び出して、デバイス インターフェイスの状態が格納されたレジストリの場所へのハンドルを取得します。

> [!NOTE]
> **CM_GETIDLIST_FILTER_PRESENT** フラグと [CM_Get_Device_ID_List_Size](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_list_sizea) および [**CM_Get_Device_ID_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_lista) を使用するか、**CM_GET_DEVICE_INTERFACE_LIST_PRESENT** フラグと [**CM_Get_Device_Interface_List_Size**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_list_sizew) および [**CM_Get_Device_Interface_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista) を使用します。 これにより、ハードウェアが存在し、通信の準備ができていることを確認します。


## <a name="using-device-interfaces"></a>デバイス インターフェイスの使用

ドライバー間で状態を共有する必要がある場合、共有された状態を所有する単一のドライバーが存在する必要があり、そのドライバーでは、他のドライバーがその状態を*読み取り*、*修正する*ための方法を公開する必要があります。

通常、状態を所有するドライバーはカスタムのデバイス インターフェイス クラス内でデバイス インターフェイスを公開します。 そのドライバーの準備が整い、他のドライバーから状態にアクセスできるようになると、インターフェイスが有効になります。 他のドライバーは、[デバイス インターフェイスの到着通知](https://docs.microsoft.com/windows-hardware/drivers/install/registering-for-notification-of-device-interface-arrival-and-device-removal)に登録できます。 状態にアクセスするために、カスタムのデバイス インターフェイス クラスは、2 つのコントラクトのうち 1 つを定義できます。

* *I/O コントラクト* は、状態へのアクセスの仕組みを提供する、そのデバイス インターフェイス クラスと関連付けることができます。 他のドライバーは、有効化されたデバイス インターフェイスを使用して、コントラクトに適合する I/O リクエストを送信します。
* クエリ インターフェイス経由で返される*直接呼び出しインターフェイス*。 他のドライバーは、[IRP_MN_QUERY_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) を送信して、呼び出すドライバーから関数ポインターを取得できます。

または、状態を所有するドライバーによって状態への直接アクセスが許可される場合、他のドライバーは、デバイス インターフェイスの状態にプログラムでアクセスできるようにするためにシステムによって提供されている関数を使用して、状態にアクセスすることができます。

これらのインターフェイスまたは状態 (使用する共有方法による) は、適切にバージョン管理される必要があります。これは、状態を所有するドライバーが、状態にアクセスする他のドライバーから独立してサービスの提供を受けられるようにするためです。 ドライバー ベンダーは、両方のドライバーが同時にサービスを受け、同じバージョンを保つと見なすことはできません。  

インターフェイスを制御するデバイスとドライバーは頻繁に切り替わるので、ドライバーとアプリケーションは、コンポーネントの起動時に [**IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) を呼び出して有効なインターフェイスのリストを取得すべきではありません。

ベスト プラクティスは、デバイス インターフェイスの到着と削除の通知に登録してから適切な関数を呼び出し、マシン上の既存の有効なインターフェイスのリストを取得することです。

デバイス インターフェイスの詳細については、次を参照してください。

* [デバイス インターフェイスの使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)
* [デバイス インターフェイスの到着とデバイスの削除の通知の登録](https://docs.microsoft.com/windows-hardware/drivers/install/registering-for-notification-of-device-interface-arrival-and-device-removal)
* [デバイス インターフェイス変更の通知登録](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-for-device-interface-change-notification)

## <a name="reading-and-writing-state"></a>状態の読み取りと書き込み

> [!NOTE]
> コンポーネントがデバイスまたはデバイス インターフェイスの*プロパティ*を使用して状態を保存している場合、引き続きその方法および適切な OS API を使用して、状態を保存し、アクセスしてください。 次のガイダンスは、コンポーネントが保存する必要がある*その他の*状態のためのものです。

様々な状態にアクセスするには、状態の場所を呼び出し元に示す関数を実行します。次いで、その場所から見た相対位置で、読み書きを行います。 ハードコーディングされた絶対レジストリ パスとファイル パスを使用すべきではありません。

このセクションには、次のサブセクションが含まれています。

* [PnP デバイス レジストリの状態](#pnp-device-registry-state)
* [デバイス インターフェイス レジストリの状態](#device-interface-registry-state)
* [サービス レジストリの状態](#service-registry-state)
* [デバイス ファイルの状態](#device-file-state)
* [サービス ファイルの状態](#service-file-state)

### <a name="pnp-device-registry-state"></a>PnP デバイス レジストリの状態

分離されているドライバー パッケージとユーザーモード コンポーネントは、通常 2 つの場所を使用してデバイスの状態をレジストリ内に保存します。 デバイスの*ハードウェア キー* (デバイス キー) と、デバイスの*ソフトウェア キー* (ドライバーキー) です。 これらのレジストリの場所へのハンドルを取得するには、使用しているプラットフォームに基づいて、次のオプションのうちの 1 つをご使用ください。


* [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey) (WDM)
* [**WdfDeviceOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)、[**WdfFdoInitOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey) (WDF)
* [**CM_Open_DevNode_Key**](https://docs.microsoft.com/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key) (ユーザーモード コード)
* [**INF AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) ディレクティブ。次に示すとおり、[INF DDInstall](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section) セクションまたは [DDInstall.HW](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section) セクションから参照される *add-registry-section* 内で HKR *reg-root* エントリを使用します。

```
[ExampleDDInstall.HW]
AddReg = Example_DDInstall.AddReg

[Example_DDInstall.AddReg] 
HKR,,ExampleValue,,%13%\ExampleFile.dll
```
### <a name="device-interface-registry-state"></a>デバイス インターフェイス レジストリの状態

デバイス インターフェイスを使用して、他のドライバーやコンポーネントと状態を共有します。 パスをグローバル レジストリの場所にハードコーディングしないでください。

デバイス インターフェイスのレジストリの状態を読み取りおよび書き込みするには、使用しているプラットフォームに基づいて、次のオプションのうち 1 つを使用します。

* [**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) (WDM)
* [**CM_Open_Device_Interface_Key**](https://docs.microsoft.com/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_device_interface_keyw) (ユーザーモード コード)
* [INF AddReg](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) ディレクティブ。*add-interface-section* セクションから参照される [add-registry-section](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive) 内の HKR *reg-root* エントリを使用します。

### <a name="service-registry-state"></a>サービス レジストリの状態

ドライバーおよび Win32 サービスの INF により設定されるレジストリの値は、[AddReg](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) セクション内に HKR 行を追加して、INF のサービス インストール セクション内でそのセクションを参照することにより、サービスの "Parameters" サブキーの下に保存する必要があります。  たとえば、次のように入力します。

```
[ExampleDDInstall.Services]
Addservice = ExampleService, 0x2, Example_Service_Inst

[Example_Service_Inst]
DisplayName    = %ExampleService.SvcDesc%
ServiceType    = 1
StartType      = 3
ErrorControl   = 1
ServiceBinary  = %13%\ExampleService.sys
AddReg=Example_Service_Inst.AddReg

[Example_Service_Inst.AddReg]
HKR, Parameters, ExampleValue, 0x00010001, 1
```

この状態の場所にアクセスするには、お使いのプラットフォームに基づいて次の関数のうちの 1 つを使用します。

* [**IoOpenDriverRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendriverregistrykey) (WDM)
* [**WdfDriverOpenParametersRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriveropenparametersregistrykey) (WDF)

### <a name="device-file-state"></a>デバイス ファイルの状態

デバイスと関連するファイルに書き込む必要がある場合、これらのファイルは、OS API を介して提供されるハンドルまたはファイル パスに対する相対的な位置に保存される必要があります。 そのデバイスに特有の構成ファイルは、そこに保存すべきファイルの種類の一例です。

* [**IoGetDeviceDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdevicedirectory) (WDM)
* [**WdfDeviceRetrieveDeviceDirectoryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceretrievedevicedirectorystring) (WDF)

### <a name="service-file-state"></a>サービス ファイルの状態

Win32 とドライバー サービスは両方とも、自分自身の状態の読み取りおよび書き込みをします。

自身の内部状態の値にアクセスするには、サービスは次のオプションの 1 つを使用します。 

* [**IoGetDriverDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdriverdirectory) (WDM)
* [**IoGetDriverDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdriverdirectory) (KMDF)
* [**WdfDriverRetrieveDriverDataDirectoryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverretrievedriverdatadirectorystring) (UMDF)

サービスの内部状態を他のコンポーネントと共有するには、レジストリまたはファイルを直接読み取るのではなく、制御され、バージョン管理されたインターフェイスを使用します。

## <a name="driverdata-and-programdata"></a>DriverData と ProgramData

他のコンポーネントと共有される中間の操作の一部として使用されるファイルは、*DriverData* または *ProgramData* の場所のいずれかに書き込まれる必要があります。

これらの場所は、コンポーネントに対し、一時的な状態、つまり他のコンポーネントによって使用されることになる状態を書き込む場所を提供します。こうした状態は、あるシステムから収集およびコピーされ、別のシステムによって処理される可能性があります。  たとえば、カスタム ログ ファイルやクラッシュ ダンプがこの説明にあてはまります。

### <a name="driverdata"></a>DriverData

`DriverData` ディレクトリは、Windows 10 のバージョン 1803 以降で利用できます。 このディレクトリには、異なるメカニズムにより、ユーザーモードおよびカーネルモードのコンポーネントの両方からアクセスすることができます。

カーネルモード ドライバーは、`\DriverData` と呼ばれるシステム提供のシンボリック リンクを使用して `DriverData` ディレクトリにアクセスする必要があります。
ユーザー モード プログラムは、環境変数 `%DriverData%` を使用して `DriverData` ディレクトリにアクセスする必要があります。

### <a name="programdata"></a>ProgramData

ユーザーモード コンポーネントは、データを保存する際に `%ProgramData%` ユーザーモード環境変数を使用できます。 

`DriverData` または `ProgramData` ディレクトリのルートにファイルを書き込まないでください。 代わりに、会社名でサブディレクトリを作成し、そのディレクトリ内にファイルを書き込んだり、サブディレクトリをさらに作成したりしてください。

たとえば、会社名が Contoso だとすると、カーネルモード ドライバーはカスタム ログを `\DriverData\Contoso\Logs` に書き込み、ユーザーモード アプリケーションは `%DriverData%\Contoso\Logs` からログ ファイルを収集して分析することができます。

