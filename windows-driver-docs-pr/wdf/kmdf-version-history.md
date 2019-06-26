---
title: KMDF のバージョンの履歴
description: このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) の Windows オペレーティング システム、および各リリースで行われた変更の対応するバージョンのバージョンを使用します。
ms.assetid: b920937c-2e5d-48cc-81b5-1462f5d03d75
keywords:
- カーネル モード ドライバー WDK KMDF、リビジョン履歴
- KMDF WDK、リビジョン履歴
- カーネル モード ドライバー フレームワーク WDK のリビジョン履歴
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c1dd1ac2fcf1979a6153e12a825c6bc2e7715fd0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371742"
---
# <a name="kmdf-version-history"></a>KMDF のバージョンの履歴


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) の Windows オペレーティング システム、および各リリースで行われた変更の対応するバージョンのバージョンを使用します。

次の表は、KMDF ライブラリのリリース履歴。

|KMDF バージョン|Release メソッド|このバージョンの Windows に含まれる|これを使用してドライバーを実行します。|
|--- |--- |--- |--- |
|1.29|WDK リリースされません。|Windows 10 バージョン 1903 (2019年の更新プログラム、19 H 1 年 3 月)|Windows 10、バージョンが 1903 以降|
|1.27|Windows 10、バージョンは 1809 WDK|Windows 10、バージョンは 1809 (2018 の年 10 月の更新、レッドス トーン 5)|Windows 10、1809 およびそれ以降のバージョン|
|1.25|Windows 10、バージョン 1803 WDK|Windows 10、バージョン 1803 (2018 年 4 月の更新、Redstone 4)|Windows 10、バージョン 1803 以降|
|1.23|Windows 10 バージョン 1709 WDK|Windows 10 バージョン 1709 (Fall Creators Update, レッドス トーン 3)|Windows 10 バージョン 1709 以降|
|1.21|Windows 10 バージョン 1703 WDK|Windows 10 バージョン 1703 (Creators Update, レッドス トーン 2)|Windows 10 バージョン 1703 以降|
|1.19|Windows 10 バージョン 1607 WDK|Windows 10 バージョン 1607 (Anniversary Update、Redstone 1)|Windows 10 バージョン 1607 を Windows Server 2016 以降|
|1.17|Windows 10 バージョン 1511 WDK|Windows 10 バージョン 1511 (11 月の更新、しきい値 2)|Windows 10 バージョン 1511 では、Windows Server 2016 以降|
|1.15|Windows 10 WDK|Windows 10 バージョン 1507 (しきい値 1)|Windows 10 バージョン 1507、Windows Server 2016 以降|
|1.13|Windows 8.1 WDK|Windows 8.1|Windows 8.1 以降|
|1.11|Windows 8 WDK|Windows 8|Windows Vista 以降|
|1.9|Windows 7 WDK|Windows 7|Windows XP 以降|
|1.7|Windows Server 2008 の WDK|Windows Vista Service Pack 1 (SP1)、Windows Server 2008|Windows 2000 以降|
|1.5|Windows Vista WDK|Windows Vista|Windows 2000 以降|
|1.1|ダウンロードのみ|なし|Windows 2000 以降|
|1.0|ダウンロードのみ|なし|Windows XP 以降|

Microsoft Visual Studio 2017 で、Windows Driver Kit (WDK) を使用すると、Windows 7 以降を実行しているドライバーをビルドします。

WDF を使用するのには、どのようなバージョンの決定については、次を参照してください。[フレームワーク バージョンを使用する必要がありますか?](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)します。

コールバックの完全な一覧とメソッド、およびどのフレームワークとバージョンに適用される、次を参照してください。 [WDF のコールバックの概要とメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)します。

KMDF ドライバーを Windows 10 の新機能については、次を参照してください。 [WDF ドライバーの新](index.md)します。

## <a name="kmdf-version-129"></a>KMDF バージョン 1.29

版 1.25 から変更されていません。

## <a name="kmdf-version-127"></a>KMDF バージョン 1.27

版 1.25 から変更されていません。

## <a name="kmdf-version-125"></a>KMDF 版 1.25

* [複数のバージョンの Windows の WDF ドライバーをビルドする](building-a-wdf-driver-for-multiple-versions-of-windows.md)

## <a name="kmdf-version-123"></a>KMDF バージョン 1.23

* コンパニオンの機能は内部使用のみを追加します。  新しい Ddi を参照してください。 [WDF のコールバックの概要とメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)します。

## <a name="kmdf-version-121"></a>KMDF バージョン 1.21

* [**WdfFileObjectGetInitiatorProcessId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/nf-wdffileobject-wdffileobjectgetinitiatorprocessid) UMDF 専用以前、KMDF で利用可能にします。
* [**WdfRequestGetRequestorProcessId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetrequestorprocessid) UMDF 専用以前、KMDF で利用可能にします。
* [**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdereferenceactual):入力*ファイル*PCCH から PCHAR パラメーターに変更します。
* [**WdfObjectReferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectreferenceactual):入力*ファイル*PCCH から PCHAR パラメーターに変更します。

## <a name="kmdf-version-119"></a>KMDF バージョン 1.19

* 追加[ **WdfDmaTransactionSetSingleTransferRequirement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetsingletransferrequirement)
* 追加**WDF_DMA_ENABLER_CONFIG_REQUIRE_SINGLE_TRANSFER**フラグ[ **WDF_DMA_ENABLER_CONFIG_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/ne-wdfdmaenabler-_wdf_dma_enabler_config_flags)
* 追加**STATUS_WDF_TOO_MANY_TRANSFERS**の値を返す[ **WdfDmaTransactionInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)と[ **WdfDmaTransactionDmaCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)
* 1 つの転送に出力するための出力メッセージを追加[ **! wdfkd.wdfdmatransaction** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction)と[ **! wdfkd.wdfdmaenabler**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler)
* 1 つの転送 DMA に関する詳細については、次を参照してください。[転送 DMA の 1 つを使用して](using-single-transfer-dma.md)します。

## <a name="kmdf-version-115"></a>KMDF バージョン 1.15

-   新しい[ **WdfDeviceOpenDevicemapKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceopendevicemapkey)メソッドは、サブキーをアクセスするためのドライバーを使用し、下に値**HKEY\_ローカル\_マシン\\ハードウェア\\DEVICEMAP**します。

## <a name="kmdf-version-113"></a>KMDF バージョン 1.13


KMDF バージョン 1.13 は、次の機能を追加します。

-   追加**CanWakeDevice**メンバー [ **WDF\_INTERRUPT\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)からデバイスを使用できる割り込みをサポートする構造体、低電力 Dx 状態は、完全に D0 状態に戻ります。 詳細については、次を参照してください。 [、割り込みを使用して、デバイスのスリープを解除する](using-an-interrupt-to-wake-a-device.md)します。
-   高解像度のタイマーをサポートします。 詳細については、次を参照してください。[を使用してタイマー](using-timers.md)します。
-   システムが低電力状態の場合有効期限が切れる場合、システムがウェイクしないタイマーをサポートします。 詳細については、次を参照してください。[を使用してタイマー](using-timers.md)します。
-   説明した次の KMDF/UMDF メソッド[デバイス プロパティの統合モデルにアクセスする](accessing-the-unified-device-property-model.md):
    -   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
    -   [**WdfDeviceAssignProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
    -   [**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)
    -   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)
    -   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
    -   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

UMDF バージョンについては、次を参照してください。 [UMDF バージョン履歴](umdf-version-history.md)します。

## <a name="kmdf-version-111"></a>KMDF Version 1.11


Version 1.11 は、次の機能を追加します。

-   [システム モードの DMA](supporting-system-mode-dma.md)

-   サポート[パッシブ レベルの割り込み](supporting-passive-level-interrupts.md)

-   [機能の電力状態](supporting-functional-power-states.md)1 台のデバイス内の複数のコンポーネント

-   [Irp の I/O キューへのディスパッチ](dispatching-irps-to-i-o-queues.md)
-   次のメソッド。
    -   [**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)
    -   [**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)
    -   [**WdfDeviceInitSetRemoveLockOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetremovelockoptions)
    -   [**WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)
    -   [**WdfDmaEnablerConfigureSystemProfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile)
    -   [**WdfDmaTransactionAllocateResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)
    -   [**WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)
    -   [**WdfDmaTransactionFreeResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionfreeresources)
    -   [**WdfDmaTransactionGetTransferInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongettransferinfo)
    -   [**WdfDmaTransactionInitializeUsingOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingoffset)
    -   [**WdfDmaTransactionSetChannelConfigurationCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetchannelconfigurationcallback)
    -   [**WdfDmaTransactionSetDeviceAddressOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetdeviceaddressoffset)
    -   [**WdfDmaTransactionSetImmediateExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetimmediateexecution)
    -   [**WdfDmaTransactionSetTransferCompleteCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsettransfercompletecallback)
    -   [**WdfDmaTransactionWdmGetTransferContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionwdmgettransfercontext)
    -   [**WdfInterruptQueueWorkItemForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)
    -   [**WdfInterruptReportActive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportactive)
    -   [**WdfInterruptReportInactive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)
    -   [**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)
    -   [**WdfIoQueueStopAndPurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurge)
    -   [**WdfIoQueueStopAndPurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)
    -   [**WdfIoTargetPurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge)
    -   [**WdfUsbTargetDeviceCreateIsochUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)
    -   [**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)
    -   [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)
    -   [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)
-   追加[ *EvtDeviceUsageNotificationEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification_ex)します。

-   追加**IdleTimeoutType**と**ExcludeD3Cold**メンバー [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)します。

-   追加**ReportInactiveOnPowerDown**メンバー [ **WDF\_INTERRUPT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)します。

-   追加**WdfIoTargetPurged**値を[ **WDF\_IO\_ターゲット\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)します。

-   追加**WdfSpecialFileBoot**値を[ **WDF\_特殊\_ファイル\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ne-wdfdevice-_wdf_special_file_type)します。

-   追加**DbgWaitForSignalTimeoutInSec**に[Framework ベースのドライバーをデバッグするためのレジストリ値](registry-values-for-debugging-kmdf-drivers.md)します。

-   追加[InstallWdf](https://go.microsoft.com/fwlink/p/?linkid=256122)、 [MultiComp](https://go.microsoft.com/fwlink/p/?linkid=256158)、および[SingleComp](https://go.microsoft.com/fwlink/p/?linkid=256158)サンプル。

## <a name="kmdf-version-19"></a>KMDF バージョン 1.9


バージョン 1.9 には、次の機能が追加されます。

-   [進行を保証](guaranteeing-forward-progress-of-i-o-operations.md)の I/O キュー

-   サポート[requeuing の I/O 要求](requeuing-i-o-requests.md)親デバイスの I/O キューに子デバイスの I/O キューから

-   指定する機能[キュー レベルの同期](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ne-wdfobject-_wdf_synchronization_scope)の個々 のキュー オブジェクト。

-   次のメソッド。
    -   [**WdfDeviceGetSystemPowerAction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetsystempoweraction)
    -   [**WdfDeviceRemoveDependentUsageDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceremovedependentusagedeviceobject)
    -   [**WdfInterruptSetExtendedPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsetextendedpolicy)
    -   [**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent)
    -   [**WdfPdoInitAssignContainerID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigncontainerid)
    -   [**WdfPreDeviceInstallEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstallex)
    -   [**WdfRequestForwardToParentDeviceIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)
    -   [**WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)
-   追加、 **NumberOfPresentedRequests**メンバーを[ **WDF\_IO\_キュー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_config)ドライバーを絞り込むためにの構造体並列 I/O キューからドライバーにフレームワークを提供する要求の I/O の数。

-   追加、 **WdfFileObjectCanBeOptional**フラグを[ **WDF\_FILEOBJECT\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ne-wdfdevice-_wdf_fileobject_class)構造体。

-   追加、 **TolerableDelay**メンバーを[ **WDF\_タイマー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/ns-wdftimer-_wdf_timer_config)構造体。

-   追加[WdfDefaultIdleInWorkingState と WdfDefaultWakeFromSleepState](user-control-of-device-idle-and-wake-behavior.md)レジストリの値。

## <a name="kmdf-version-17"></a>KMDF バージョン 1.7


-   [ **WdfDeviceEnqueueRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest) IRQL でメソッドを呼び出すことが&lt;= ディスパッチ\_レベル。

-   [ **WdfWorkItemEnqueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)指定された作業項目が作業項目のキューが既にある場合、メソッドを呼び出すことができます。

-   追加、 [ *EvtDeviceArmWakeFromSxWithReason* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason)イベント コールバック関数。

-   追加**ArmForWakeIfChildrenAreArmedForWake**と**IndicateChildWakeOnParentWake**メンバーを[ **WDF\_デバイス\_POWER\_ポリシー\_WAKE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)構造体。

## <a name="kmdf-version-15"></a>KMDF バージョン 1.5


-   [**WdfUsbInterfaceGetNumSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetnumsettings)

-   追加、 **DriverPoolTag**メンバー [ **WDF\_ドライバー\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)します。

## <a name="kmdf-version-11"></a>KMDF バージョン 1.1


-   次のメソッド。
    -   [**WdfCommonBufferCreateWithConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig)
    -   [**WdfDmaEnablerGetFragmentLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablergetfragmentlength)
    -   [**WdfDmaEnablerWdmGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter)

## <a name="kmdf-version-10"></a>KMDF バージョン 1.0


最初のリリース。

 

 





