---
title: UMDF バージョン履歴
description: このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) のバージョン、対応する Windows オペレーティングシステムのバージョン、および各リリースで行われた変更について説明します。
ms.assetid: f3e895c6-6801-4033-adaa-d7d04a46db0a
keywords:
- UMDF WDK、リビジョン履歴
- UMDF WDK、バージョン情報
- リビジョン履歴 WDK UMDF
- バージョン情報 WDK UMDF
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 180774b7ef048abac3ea4eb8d9ca05cf1bb63b3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843113"
---
# <a name="umdf-version-history"></a>UMDF バージョン履歴


このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) のバージョン、対応する Windows オペレーティングシステムのバージョン、および各リリースで行われた変更について説明します。

次の表は、UMDF ライブラリのリリース履歴を示しています。

|UMDF バージョン|Release メソッド|このバージョンの Windows に含まれています|これを使用するドライバーは、で実行できます。|
|--- |--- |--- |--- |
|2.29|WDK でリリースされていません|Windows 10、バージョン 1903 (2019 年3月更新、19H1)|Windows 10 バージョン1903以降|
|2.27|Windows 10 バージョン 1809 WDK|Windows 10、バージョン 1809 (2018 年10月の更新プログラム、Redstone 5)|Windows 10 バージョン1809以降|
|2.25|Windows 10 バージョン 1803 WDK|Windows 10、バージョン 1803 (2018 年4月更新、Redstone 4)|Windows 10 バージョン1803以降|
|2.23|Windows 10 バージョン 1709 WDK|Windows 10、バージョン 1709 (作成者の更新プログラム、Redstone 3)|Windows 10 バージョン1709以降|
|2.21|Windows 10 バージョン 1703 WDK|Windows 10、バージョン 1703 (作成者の更新、Redstone 2)|Windows 10 バージョン1703以降|
|2.19|Windows 10 バージョン 1607 WDK|Windows 10、バージョン 1607 (記念日更新、Redstone 1)|Windows 10 バージョン1607、Windows Server 2016 以降|
|2.17|Windows 10 バージョン 1511 WDK|Windows 10 バージョン 1511 (11 月の更新プログラム、しきい値 2)|Windows 10 バージョン1511、Windows Server 2016 以降|
|2.15|Windows 10 WDK|Windows 10 バージョン 1507 (しきい値 1)|Windows 10 バージョン1507、Windows Server 2016 以降|
|2.0|Windows Driver Kit (WDK) 8.1|Windows 8.1|Windows 8.1 以降|
|1.11|Windows Driver Kit (WDK) 8|Windows 8|Windows Vista 以降|
|1.9|Windows 7 WDK|Windows 7|Windows XP 以降|
|1.7|Windows Server 2008 WDK|Windows Vista Service Pack 1 (SP1)、Windows Server 2008|Windows XP 以降|
|1.5|Windows Vista WDK|Windows Vista|Windows XP 以降|


Windows Driver Kit (WDK) と Microsoft Visual Studio 2017 を使用して、Windows 7 以降で実行されるドライバーを構築できます。

使用する WDF のバージョンを確認する方法については、「[使用する必要があるフレームワークのバージョン](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)」を参照してください。

Windows 10 での UMDF ドライバーの新機能の詳細については、「 [WDF drivers の新](index.md)機能」を参照してください。

## <a name="umdf-version-229"></a>UMDF バージョン2.29

バージョン2.27 から変更されていません。

## <a name="umdf-version-227"></a>UMDF バージョン2.27

* 新しい API [**WdfDriverRetrieveDriverDataDirectoryString**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverretrievedriverdatadirectorystring) が追加されました

## <a name="umdf-version-225"></a>UMDF バージョン2.25

* [複数のバージョンの Windows の WDF ドライバーをビルドする](building-a-wdf-driver-for-multiple-versions-of-windows.md)
* [**WdfDeviceRetrieveDeviceDirectoryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceretrievedevicedirectorystring)

## <a name="umdf-version-223"></a>UMDF バージョン2.23

* 内部使用のためだけに追加されたコンパニオン機能。  新しい DDIs については、「 [WDF のコールバックとメソッドの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)」を参照してください。

## <a name="umdf-version-221"></a>UMDF バージョン2.21

* [**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual):*ファイル*パラメーターの型が PCHAR から pcch に変更されました。
* [**Wdfobjectreferenceactual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual):*ファイル*パラメーターの型が PCHAR から pcch に変更されました。

## <a name="umdf-version-219"></a>UMDF バージョン2.19

UMDF Version 2.19 の変更や追加はありません。

## <a name="umdf-version-217"></a>UMDF バージョン2.17

このバージョンでは、次の既存のインターフェイスの UMDF サポートが追加されています。

-   [**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)
-   [*Evtdevicewdmirpq ディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)
-   [**WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)
-   [**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)

詳細については、「 [irp を I/o キューにディスパッチする](dispatching-irps-to-i-o-queues.md)」を参照してください。

## <a name="umdf-version-215"></a>UMDF バージョン2.15

バージョン2.15 の更新された DDIs の一覧を次に示します。

-   新しい[**WdfDeviceOpenDevicemapKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopendevicemapkey)メソッドを使用すると、ドライバーは**HKEY\_ローカル\_マシン\\ハードウェア\\DEVICEMAP**のサブキーと値にアクセスできます。

-   UMDF ドライバーは、 [**WdfIoTargetWdmGetTargetFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)を呼び出して、スタック内の次に低いカーネルモードドライバーへのファイルハンドルを取得できます。 ドライバーは、ローカル i/o ターゲットに i/o を送信するためのフレームワークの抽象化をバイパスして、そのハンドルにデータを書き込むことができます。

-   UMDF ドライバーは、基になるバスドライバーが再列挙するように要求できます。 「 [**Wdfdevicesetfailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)」を参照してください。

-   接続リソースを持つデバイスでは、 **UmdfDirectHardwareAccess**ディレクティブの設定は常に必要ではなくなりました。 「[Specifying WDF Directives in INF Files](specifying-wdf-directives-in-inf-files.md)」 (INF ファイルに WDF ディレクティブを指定する) を参照してください。

## <a name="umdf-version-20"></a>UMDF バージョン2.0


[はじめに「umdf WITH umdf](getting-started-with-umdf-version-2.md)」で説明されている共有機能に加えて、次のように、umdf version 2.0 が追加されます。

-   システムが低電力状態のときにシステムをスリープ解除しない場合のタイマーのサポート。 詳細については、「[タイマーの使用](using-timers.md)」を参照してください。
-   **CanWakeDevice**メンバーを[**WDF\_INTERRUPT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体に追加して、デバイスを低電力の Dx 状態から完全な D0 状態に戻すために使用できる割り込みをサポートするようになりました。 詳細については、「[割り込みを使用したデバイスのスリープ解除](using-an-interrupt-to-wake-a-device.md)」を参照してください。
-   UMDF ドライバーの単一コンポーネントのシングルステート (F0) 電源管理。 詳細については、「 [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)」を参照してください。

-   これで、Wdfkd のいくつかのデバッガー拡張コマンドを、UMDF 2.0 ドライバーにも使用できるようになりました。 拡張ライブラリには、UMDF 2.0 ドライバーのデバッグ専用に設計された次の新しい拡張コマンドも含まれています。

    -   [ **! wdfkd. wdfumdevstack**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack)
    -   [ **! wdfkd. wdfumdevstacks**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks)
    -   [ **! wdfkd. wdfumdownirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdownirp)
    -   [ **! wdfkd. wdfumfile**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumfile)
    -   [ **! wdfkd. wdfumirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp)
    -   [ **! wdfkd. wdfumirps**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)
    -   [ **! wdfkd. wdfdevice割込み**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdeviceinterrupts)

    拡張機能コマンドとフレームワークの適用性の一覧については、「[デバッガー拡張機能](debugger-extensions-for-kmdf-drivers.md)」を参照してください。

-   [フレームワークのイベントロガー](using-the-framework-s-event-logger.md)または*インフライトレコーダー* (IFR) は、UMDF 2.0 ドライバーで動作するように更新されました。
-   他の WDF デバッガー拡張機能が、UMDF 2.0 ドライバーで動作するように更新されました。 どのフレームワークに適用されるかに関する情報など、拡張機能コマンドの完全な一覧については、「 [Debugger Extensions FOR WDF Drivers](debugger-extensions-for-kmdf-drivers.md)」を参照してください。
-   **WdfIoTargetOpenLocalTargetByFile**を[**WDF\_IO\_ターゲット\_開いて\_の種類を開き**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_open_type)、UMDF ドライバーが、関連付けられているファイルオブジェクトを必要とする下位ターゲットにドライバーで作成された要求を送信できるようにしました。 詳細については、「 **WDF\_IO\_TARGET\_OPEN\_TYPE**」を参照してください。
-   次の UMDF のみのルーチン。

    -   [*EvtRequestImpersonate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)
    -   [**WDF\_IO\_ターゲット\_OPEN\_PARAMS\_FILE\_OPEN\_ファイルによって開く**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_open_by_file)
    -   [**WdfDeviceAllocAndQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryinterfaceproperty)
    -   [**Wdfdevice割り当て Interfaceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigninterfaceproperty)
    -   [**WdfDeviceGetDeviceStackIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestackiotype)
    -   [**WdfDeviceGetHardwareRegisterMappedAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegethardwareregistermappedaddress)
    -   [**WdfDeviceMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicemapiospace)
    -   [**WdfDevicePostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicepostevent)
    -   [**WdfDeviceQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequeryinterfaceproperty)
    -   [**WdfDeviceUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceunmapiospace)
    -   [**WdfFileObjectGetInitiatorProcessId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetinitiatorprocessid) (kmdf 1.21 に追加)
    -   [**Wdffileobjectgetfmri Fileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetrelatedfileobject)
    -   [**WdfRequestGetEffectiveIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgeteffectiveiotype)
    -   [**WdfRequestGetRequestorProcessId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetrequestorprocessid) (kmdf 1.21 に追加)
    -   [**WdfRequestGetUserModeInitiatedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetusermodedriverinitiatedio)
    -   [**WdfRequestImpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)
    -   [**WdfRequestIsFromUserModeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisfromusermodedriver)
    -   [**WdfRequestRetrieveActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)
    -   [**WdfRequestSetActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)
    -   [**WdfRequestSetUserModeDriverInitiatedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetusermodedriverinitiatedio)
-   「[統合されたデバイスのプロパティモデルにアクセスする](accessing-the-unified-device-property-model.md)」で説明されている、次の kmdf/UMDF メソッド。

    -   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
    -   [**Wdfdevice割り当てプロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
    -   [**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)
    -   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)
    -   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
    -   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

    詳細については、「[統合デバイスプロパティモデルへのアクセス](accessing-the-unified-device-property-model.md)」を参照してください。

-   [**WdfUsbTargetDeviceSelectConfigType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype)での次の USB 構成の種類のサポート:
    -   **WdfUsbTargetDeviceSelectConfigTypeSingleInterface**
    -   **WdfUsbTargetDeviceSelectConfigTypeMultiInterface**
    -   **WdfUsbTargetDeviceSelectConfigTypeInterfacesPairs**
-   [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)での次の機能の種類のクエリのサポート:
    -   **GUID\_USB\_機能\_デバイス\_接続\_高い\_速度\_互換性**
    -   **GUID\_USB\_機能\_デバイス\_接続\_非常\_速度\_互換性があります**
-   [WDF レジスタ/ポートアクセス関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfhwaccess/)を追加しました

## <a name="umdf-version-111"></a>UMDF バージョン1.11


バージョン1.11 では、ドライバーによって提供される次のコールバックインターフェイスとイベントコールバック関数が追加されています。

-   [**IPnpCallbackHardware2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware2)

-   [**IPnpCallbackHardwareInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardwareinterrupt)

バージョン1.11 では、次のフレームワークによって提供されるインターフェイスが追加されます。

-   [**IWDFCmResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfcmresourcelist)

-   [**IWDFDevice3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice3)

-   [**IWDFFile3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile3)

-   [**IWDFInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfinterrupt)

-   [**IWDFIoRequest3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest3)

-   [**IWDFUnifiedPropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfunifiedpropertystore)

-   [**IWDFUnifiedPropertyStoreFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfunifiedpropertystorefactory)

-   [**IWDFWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfworkitem)

バージョン1.11 では、次の機能が UMDF ベースのドライバーに追加されます。

-   [ハードウェアへのアクセスと割り込みの処理](accessing-hardware-and-handling-interrupts.md)

-   [UMDF ドライバーでのデバイスプールの使用](using-device-pooling-in-umdf-drivers.md)

-   「INF で WDF ディレクティブを指定する」で説明されているように、 **Umdfhostprocesssharing**、 **UmdfDirectHardwareAccess**、 **umdfhostprocesssharing**、 **Umdfhostprocesssharing**、および**UmdfFsContextUsePolicy**ディレクティブを追加しました。 [ファイル](specifying-wdf-directives-in-inf-files.md)

-   [UMDF ドライバーの既知のセキュリティ識別子 (SID)](controlling-device-access.md)

-   統合プロパティストアのサポート。「 [UMDF ベースのドライバーでのレジストリの使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)」で説明しています。

-   [**Iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)は、UMDF と連動するように統合されています。 以前のバージョンでは、このルーチンはデバイスのハンドルに参照を取得した後、デバイスオブジェクトへのハンドルを閉じます。 この動作は、すべての i/o が完了するまで、デバイスオブジェクトでのクリーンアップ要求が発生しないという、UMDF の想定と互換性がありませんでした。

-   [UMDF ベースの HID ミニドライバーの作成](creating-umdf-hid-minidrivers.md)

-   [UMDF ベースのドライバーでのアイドル状態の電源をサポート](supporting-idle-power-down-in-umdf-drivers.md)するためのサポートの強化。 これで、フレームワークはアイドルタイムアウト期間が経過したときに、デバイスを D3cold 電源状態にすることができるようになりました。 また、システムが動作中 (S0) 状態に戻ったときに、デバイスが動作中 (D0) 状態に戻るようにすることもできます。

-   次のサンプルは、UMDF 1.11: [WudfVhidmini](https://go.microsoft.com/fwlink/p/?linkid=256226)、 [netare pprovider](https://go.microsoft.com/fwlink/p/?linkid=256147)の新しいものです。

## <a name="umdf-version-19"></a>UMDF バージョン1.9


バージョン1.9 では、ドライバーによって提供される次のコールバックインターフェイスが追加されています。

-   [IPnpCallbackRemoteInterfaceNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackremoteinterfacenotification)

-   [IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)

-   [IPowerPolicyCallbackWakeFromSx](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)

-   [IQueueCallbackIoCanceledOnQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackiocanceledonqueue)

-   [IRemoteInterfaceCallbackEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremoteinterfacecallbackevent)

-   [IRemoteInterfaceCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremoteinterfacecallbackremoval)

-   [Iremotetargetの削除](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremotetargetcallbackremoval)

-   [IWDFRemoteInterfaceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremoteinterfaceinitialize)

バージョン1.9 では、次のフレームワークによって提供されるインターフェイスが追加されます。

-   [IWDFDevice2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice2)

-   [IWDFDeviceInitialize2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize2)

-   [IWDFFile2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile2)

-   [IWDFIoRequest2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest2)

-   [IWDFIoTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget2)

-   [IWDFNamedPropertyStore2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore2)

-   [IWDFPropertyStoreFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfpropertystorefactory)

-   [IWDFRemoteTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremotetarget)

-   [IWDFUsbTargetPipe2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe2)

これらのインターフェイスによって、次の機能が UMDF ベースのドライバーに追加されます。

-   [リモート i/o ターゲット](general-i-o-targets-in-umdf.md)

-   [電源ポリシーの所有権](power-policy-ownership-in-umdf.md)

-   [ダイレクト i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)バッファーアクセス方法

-   USB デバイスの[継続的なリーダー](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-pipes-in-umdf-1-x-drivers)

-   [デバイスインターフェイス](using-device-interfaces-in-umdf-drivers.md)のサポートの強化

-   [I/o 要求をキャンセル](canceling-i-o-requests.md)する機能の強化

-   [レジストリ](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)へのアクセスの強化

 

 





