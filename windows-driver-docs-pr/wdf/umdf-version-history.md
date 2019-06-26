---
title: UMDF バージョン履歴
description: このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) の Windows オペレーティング システム、および各リリースで行われた変更の対応するバージョンのバージョンを使用します。
ms.assetid: f3e895c6-6801-4033-adaa-d7d04a46db0a
keywords:
- UMDF WDK、リビジョン履歴
- UMDF WDK、バージョン情報
- WDK UMDF のリビジョン履歴
- WDK UMDF のバージョン情報
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 17972b1697ef1991aac95b549c55261525352b28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372295"
---
# <a name="umdf-version-history"></a>UMDF バージョン履歴


このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) の Windows オペレーティング システム、および各リリースで行われた変更の対応するバージョンのバージョンを使用します。

次の表は、UMDF ライブラリのリリース履歴。

|UMDF バージョン|Release メソッド|このバージョンの Windows に含まれる|これを使用してドライバーを実行できます。|
|--- |--- |--- |--- |
|2.29|WDK リリースされません。|Windows 10 バージョン 1903 (2019年の更新プログラム、19 H 1 年 3 月)|Windows 10、バージョンが 1903 以降|
|2.27|Windows 10、バージョンは 1809 WDK|Windows 10、バージョンは 1809 (2018 の年 10 月の更新、レッドス トーン 5)|Windows 10、1809 およびそれ以降のバージョン|
|2.25|Windows 10、バージョン 1803 WDK|Windows 10、バージョン 1803 (2018 年 4 月の更新、Redstone 4)|Windows 10、バージョン 1803 以降|
|2.23|Windows 10 バージョン 1709 WDK|Windows 10 バージョン 1709 (Fall Creators Update, レッドス トーン 3)|Windows 10 バージョン 1709 以降|
|2.21|Windows 10 バージョン 1703 WDK|Windows 10 バージョン 1703 (Creators Update, レッドス トーン 2)|Windows 10 バージョン 1703 以降|
|2.19|Windows 10 バージョン 1607 WDK|Windows 10 バージョン 1607 (Anniversary Update、Redstone 1)|Windows 10、バージョン 1607 を Windows Server 2016 以降|
|2.17|Windows 10 バージョン 1511 WDK|Windows 10 バージョン 1511 (11 月の更新、しきい値 2)|Windows 10、バージョン 1511 では、Windows Server 2016 以降|
|2.15|Windows 10 WDK|Windows 10 バージョン 1507 (しきい値 1)|Windows 10 バージョン 1507、Windows Server 2016 以降|
|2.0|Windows Driver Kit (WDK) 8.1|Windows 8.1|Windows 8.1 以降|
|1.11|Windows Driver Kit (WDK) 8|Windows 8|Windows Vista 以降|
|1.9|Windows 7 WDK|Windows 7|Windows XP 以降|
|1.7|Windows Server 2008 の WDK|Windows Vista Service Pack 1 (SP1)、Windows Server 2008|Windows XP 以降|
|1.5|Windows Vista WDK|Windows Vista|Windows XP 以降|


Microsoft Visual Studio 2017 で、Windows Driver Kit (WDK) を使用すると、Windows 7 以降を実行しているドライバーをビルドします。

WDF を使用するのには、どのようなバージョンの決定については、次を参照してください。[フレームワーク バージョンを使用する必要がありますか?](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)します。

Windows 10 で UMDF ドライバーの新機能については、次を参照してください。 [WDF ドライバーの新](index.md)します。

## <a name="umdf-version-229"></a>UMDF バージョン 2.29

2\.27 のバージョンから変更されていません。

## <a name="umdf-version-227"></a>UMDF バージョン 2.27

* 新しい API [**WdfDriverRetrieveDriverDataDirectoryString**](/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverretrievedriverdatadirectorystring) が追加されました

## <a name="umdf-version-225"></a>UMDF バージョン 2.25

* [複数のバージョンの Windows の WDF ドライバーをビルドする](building-a-wdf-driver-for-multiple-versions-of-windows.md)
* [**WdfDeviceRetrieveDeviceDirectoryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceretrievedevicedirectorystring)

## <a name="umdf-version-223"></a>UMDF バージョン 2.23

* コンパニオンの機能は内部使用のみを追加します。  新しい Ddi を参照してください。 [WDF のコールバックの概要とメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)します。

## <a name="umdf-version-221"></a>UMDF バージョン 2.21

* [**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdereferenceactual):入力*ファイル*PCCH から PCHAR パラメーターに変更します。
* [**WdfObjectReferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectreferenceactual):入力*ファイル*PCCH から PCHAR パラメーターに変更します。

## <a name="umdf-version-219"></a>UMDF バージョン 2.19

変更または UMDF バージョン 2.19 の追加はありません。

## <a name="umdf-version-217"></a>UMDF バージョン 2.17

このバージョンは、次の既存のインターフェイスの UMDF サポートを追加します。

-   [**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)
-   [*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)
-   [**WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)
-   [**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)

詳細については、次を参照してください。 [I/O キューへのディスパッチ Irp](dispatching-irps-to-i-o-queues.md)します。

## <a name="umdf-version-215"></a>UMDF バージョン 2.15

更新された Ddi 2.15 バージョンの一覧を次に示します。

-   新しい[ **WdfDeviceOpenDevicemapKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceopendevicemapkey)メソッドは、サブキーをアクセスするためのドライバーを使用し、下に値**HKEY\_ローカル\_マシン\\ハードウェア\\DEVICEMAP**します。

-   UMDF ドライバーを呼び出すことができます[ **WdfIoTargetWdmGetTargetFileHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)そのスタックに次の下位のカーネル モード ドライバーのファイル ハンドルを取得します。 ドライバーは、データをローカル I/O ターゲットに I/O を送信するためのフレームワークの抽象化をバイパスして、そのハンドルを書き込むことができます。

-   UMDF ドライバーでは、基になるバス ドライバー再列挙することを要求できます。 参照してください[ **WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)します。

-   設定、 **UmdfDirectHardwareAccess**ディレクティブは常にリソースを接続するデバイスの必要なくなりました。 「[Specifying WDF Directives in INF Files](specifying-wdf-directives-in-inf-files.md)」 (INF ファイルに WDF ディレクティブを指定する) を参照してください。

## <a name="umdf-version-20"></a>UMDF Version 2.0


説明されている共有機能だけでなく[UMDF 入門](getting-started-with-umdf-version-2.md)、UMDF version 2.0 で追加します。

-   システムが低電力状態の場合有効期限が切れる場合、システムがウェイクしないタイマーをサポートします。 詳細については、次を参照してください。[を使用してタイマー](using-timers.md)します。
-   追加**CanWakeDevice**メンバー [ **WDF\_INTERRUPT\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)からデバイスを使用できる割り込みをサポートする構造体、低電力 Dx 状態は、完全に D0 状態に戻ります。 詳細については、次を参照してください。 [、割り込みを使用して、デバイスのスリープを解除する](using-an-interrupt-to-wake-a-device.md)します。
-   単一コンポーネントの 1 つの状態 (F0) の電源管理 UMDF ドライバー。 詳細については、次を参照してください。 [ **WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)します。

-   Wdfkd.dll でいくつかのデバッガー拡張機能のコマンドは、2.0 の UMDF ドライバーも今すぐに使用できます。 拡張機能ライブラリには、UMDF 2.0 ドライバーのデバッグ専用に設計された次の新しい拡張機能コマンドも含まれています。

    -   [ **!wdfkd.wdfumdevstack**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack)
    -   [ **!wdfkd.wdfumdevstacks**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks)
    -   [ **!wdfkd.wdfumdownirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdownirp)
    -   [ **!wdfkd.wdfumfile**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumfile)
    -   [ **!wdfkd.wdfumirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp)
    -   [ **!wdfkd.wdfumirps**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)
    -   [ **!wdfkd.wdfdeviceinterrupts**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdeviceinterrupts)

    拡張機能のコマンドとフレームワークの適用性の一覧は、次を参照してください。[デバッガー拡張機能](debugger-extensions-for-kmdf-drivers.md)します。

-   [フレームワークのイベント ロガー](using-the-framework-s-event-logger.md)、または*インフライト レコーダー* (IFR) が 2.0 の UMDF ドライバーの動作に更新されました。
-   2\.0 の UMDF ドライバーを使用するその他の WDF デバッガー拡張が更新されました。 情報についての フレームワークに適用されますを参照してくださいものなど、拡張機能のコマンドの完全な一覧については[デバッガーの拡張機能ドライバーを WDF](debugger-extensions-for-kmdf-drivers.md)します。
-   追加**WdfIoTargetOpenLocalTargetByFile**に[ **WDF\_IO\_ターゲット\_オープン\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_open_type) UMDF を許可するにはドライバー ファイルが関連付けられているオブジェクトを必要とするターゲットを削減するドライバーが作成した要求を送信します。 詳細については、の「解説」を参照してください。 **WDF\_IO\_ターゲット\_オープン\_型**します。
-   次の UMDF 専用であるルーチン:

    -   [*EvtRequestImpersonate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)
    -   [**WDF\_IO\_ターゲット\_オープン\_PARAMS\_INIT\_オープン\_BY\_ファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_open_by_file)
    -   [**WdfDeviceAllocAndQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryinterfaceproperty)
    -   [**WdfDeviceAssignInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigninterfaceproperty)
    -   [**WdfDeviceGetDeviceStackIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestackiotype)
    -   [**WdfDeviceGetHardwareRegisterMappedAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegethardwareregistermappedaddress)
    -   [**WdfDeviceMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicemapiospace)
    -   [**WdfDevicePostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicepostevent)
    -   [**WdfDeviceQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicequeryinterfaceproperty)
    -   [**WdfDeviceUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceunmapiospace)
    -   [**WdfFileObjectGetInitiatorProcessId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/nf-wdffileobject-wdffileobjectgetinitiatorprocessid) (KMDF 1.21 に追加)
    -   [**WdfFileObjectGetRelatedFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/nf-wdffileobject-wdffileobjectgetrelatedfileobject)
    -   [**WdfRequestGetEffectiveIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgeteffectiveiotype)
    -   [**WdfRequestGetRequestorProcessId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetrequestorprocessid) (KMDF 1.21 に追加)
    -   [**WdfRequestGetUserModeInitiatedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetusermodedriverinitiatedio)
    -   [**WdfRequestImpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)
    -   [**WdfRequestIsFromUserModeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestisfromusermodedriver)
    -   [**WdfRequestRetrieveActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)
    -   [**WdfRequestSetActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)
    -   [**WdfRequestSetUserModeDriverInitiatedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetusermodedriverinitiatedio)
-   説明した次の KMDF/UMDF メソッド[デバイス プロパティの統合モデルにアクセスする](accessing-the-unified-device-property-model.md):

    -   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
    -   [**WdfDeviceAssignProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
    -   [**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)
    -   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)
    -   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
    -   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

    詳細については、次を参照してください。[デバイス プロパティの統合モデルにアクセスする](accessing-the-unified-device-property-model.md)します。

-   次の USB 構成タイプのサポート[ **WdfUsbTargetDeviceSelectConfigType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype):
    -   **WdfUsbTargetDeviceSelectConfigTypeSingleInterface**
    -   **WdfUsbTargetDeviceSelectConfigTypeMultiInterface**
    -   **WdfUsbTargetDeviceSelectConfigTypeInterfacesPairs**
-   次の機能の種類のクエリでのサポート[ **WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability):
    -   **GUID\_USB\_機能\_デバイス\_接続\_高\_速度\_互換性**
    -   **GUID\_USB\_機能\_デバイス\_接続\_スーパー\_速度\_互換性**
-   追加[WDF 登録/ポート アクセス関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfhwaccess/)

## <a name="umdf-version-111"></a>UMDF Version 1.11


Version 1.11 は、次のドライバーが提供するコールバック インターフェイスとイベントのコールバック関数を追加します。

-   [**IPnpCallbackHardware2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware2)

-   [**IPnpCallbackHardwareInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardwareinterrupt)

Version 1.11 は、次のフレームワークが指定したインターフェイスを追加します。

-   [**IWDFCmResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfcmresourcelist)

-   [**IWDFDevice3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice3)

-   [**IWDFFile3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile3)

-   [**IWDFInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfinterrupt)

-   [**IWDFIoRequest3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest3)

-   [**IWDFUnifiedPropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfunifiedpropertystore)

-   [**IWDFUnifiedPropertyStoreFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfunifiedpropertystorefactory)

-   [**IWDFWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfworkitem)

Version 1.11 には、UMDF ベースのドライバーには次の機能が追加されます。

-   [ハードウェアにアクセスして、割り込み処理](accessing-hardware-and-handling-interrupts.md)

-   [UMDF ドライバーでデバイスのプールを使用します。](using-device-pooling-in-umdf-drivers.md)

-   追加**UmdfHostProcessSharing**、 **UmdfDirectHardwareAccess**、 **UmdfRegisterAccessMode**、 **UmdfFileObjectPolicy**と**UmdfFsContextUsePolicy**で示すディレクティブは、 [INF ファイルで WDF ディレクティブを指定します。](specifying-wdf-directives-in-inf-files.md)

-   [UMDF ドライバーの既知のセキュリティ識別子 (SID)](controlling-device-access.md)

-   プロパティ ストアのサポートで説明されているユニファイド[UMDF ベースのドライバーのレジストリを使用して](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)

-   [**IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer) UMDF を使用する統合されています。 以前のバージョンでは、このルーチンは、デバイスのハンドルの参照を考慮してデバイス オブジェクトを識別するハンドルを閉じます。 この動作は、すべての I/O が完了するまでデバイス オブジェクトのクリーンアップ要求は実行されません UMDF の期待と互換性がありません。

-   [UMDF ベース HID ミニドライバーを作成します。](creating-umdf-hid-minidrivers.md)

-   サポートの強化[をサポートしているアイドル状態の電源切断 UMDF ベースのドライバーで](supporting-idle-power-down-in-umdf-drivers.md)します。 フレームワーク挿入できるように、デバイス D3cold の電源状態でアイドル状態のタイムアウト期間が経過するとします。 フレームワークには、デバイスの作業 (S0) 状態に戻ると、システムの作業 (D0) 状態に戻るにこともあります。

-   次のサンプルは、UMDF 1.11 の新機能です。[WudfVhidmini](https://go.microsoft.com/fwlink/p/?linkid=256226)、 [NetNfpProvider](https://go.microsoft.com/fwlink/p/?linkid=256147)します。

## <a name="umdf-version-19"></a>UMDF バージョン 1.9


バージョン 1.9 には、次のドライバーが提供するコールバック インターフェイスが追加されます。

-   [IPnpCallbackRemoteInterfaceNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackremoteinterfacenotification)

-   [IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)

-   [IPowerPolicyCallbackWakeFromSx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)

-   [IQueueCallbackIoCanceledOnQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackiocanceledonqueue)

-   [IRemoteInterfaceCallbackEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremoteinterfacecallbackevent)

-   [IRemoteInterfaceCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremoteinterfacecallbackremoval)

-   [IRemoteTargetCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremotetargetcallbackremoval)

-   [IWDFRemoteInterfaceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfremoteinterfaceinitialize)

バージョン 1.9 には、次のフレームワークが指定したインターフェイスが追加されます。

-   [IWDFDevice2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice2)

-   [IWDFDeviceInitialize2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize2)

-   [IWDFFile2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile2)

-   [IWDFIoRequest2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest2)

-   [IWDFIoTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget2)

-   [IWDFNamedPropertyStore2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfnamedpropertystore2)

-   [IWDFPropertyStoreFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfpropertystorefactory)

-   [IWDFRemoteTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfremotetarget)

-   [IWDFUsbTargetPipe2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe2)

これらのインターフェイスは、UMDF ベースのドライバーには次の機能を追加します。

-   [リモートの I/O ターゲット](general-i-o-targets-in-umdf.md)

-   [電源ポリシーの所有権](power-policy-ownership-in-umdf.md)

-   [ダイレクト I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)バッファーへのアクセス メソッド

-   [継続的なリーダー](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-pipes-in-umdf-1-x-drivers)の USB デバイス

-   サポートの強化[デバイス インターフェイス](using-device-interfaces-in-umdf-drivers.md)

-   機能の強化[I/O 要求をキャンセル](canceling-i-o-requests.md)

-   アクセスの強化、[レジストリ](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)

 

 





