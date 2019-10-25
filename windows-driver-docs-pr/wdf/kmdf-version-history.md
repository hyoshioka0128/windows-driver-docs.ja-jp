---
title: KMDF のバージョンの履歴
description: このトピックでは、カーネルモードドライバーフレームワーク (KMDF) のバージョン、対応する Windows オペレーティングシステムのバージョン、および各リリースで行われた変更について説明します。
ms.assetid: b920937c-2e5d-48cc-81b5-1462f5d03d75
keywords:
- カーネルモードドライバー WDK KMDF、リビジョン履歴
- KMDF WDK、リビジョン履歴
- カーネルモードドライバーフレームワーク WDK、リビジョン履歴
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6fccda5aa4af89d1ec1ad81c48175d5ef5c1197d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843156"
---
# <a name="kmdf-version-history"></a>KMDF のバージョンの履歴


このトピックでは、カーネルモードドライバーフレームワーク (KMDF) のバージョン、対応する Windows オペレーティングシステムのバージョン、および各リリースで行われた変更について説明します。

次の表は、KMDF ライブラリのリリース履歴を示しています。

|KMDF バージョン|Release メソッド|このバージョンの Windows に含まれています|使用しているドライバーを実行する|
|--- |--- |--- |--- |
|1.29|WDK でリリースされていません|Windows 10、バージョン 1903 (2019 年3月更新、19H1)|Windows 10 バージョン1903以降|
|1.27|Windows 10 バージョン 1809 WDK|Windows 10、バージョン 1809 (2018 年10月の更新プログラム、Redstone 5)|Windows 10 バージョン1809以降|
|1.25|Windows 10 バージョン 1803 WDK|Windows 10、バージョン 1803 (2018 年4月更新、Redstone 4)|Windows 10 バージョン1803以降|
|1.23|Windows 10 バージョン 1709 WDK|Windows 10、バージョン 1709 (作成者の更新プログラム、Redstone 3)|Windows 10 バージョン1709以降|
|1.21|Windows 10 バージョン 1703 WDK|Windows 10、バージョン 1703 (作成者の更新、Redstone 2)|Windows 10 バージョン1703以降|
|1.19|Windows 10 バージョン 1607 WDK|Windows 10、バージョン 1607 (記念日更新、Redstone 1)|Windows 10 バージョン1607、Windows Server 2016 以降|
|1.17|Windows 10 バージョン 1511 WDK|Windows 10 バージョン 1511 (11 月の更新プログラム、しきい値 2)|Windows 10 バージョン1511、Windows Server 2016 以降|
|1.15|Windows 10 WDK|Windows 10 バージョン 1507 (しきい値 1)|Windows 10 バージョン1507、Windows Server 2016 以降|
|1.13|WDK Windows 8.1|Windows 8.1|Windows 8.1 以降|
|1.11|Windows 8 WDK|Windows 8|Windows Vista 以降|
|1.9|Windows 7 WDK|Windows 7|Windows XP 以降|
|1.7|Windows Server 2008 WDK|Windows Vista Service Pack 1 (SP1)、Windows Server 2008|Windows 2000 以降|
|1.5|Windows Vista WDK|Windows Vista|Windows 2000 以降|
|1.1|ダウンロードのみ|なし|Windows 2000 以降|
|1.0|ダウンロードのみ|なし|Windows XP 以降|

Windows Driver Kit (WDK) と Microsoft Visual Studio 2017 を使用して、Windows 7 以降で実行されるドライバーを構築できます。

使用する WDF のバージョンを確認する方法については、「[使用する必要があるフレームワークのバージョン](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)」を参照してください。

コールバックとメソッド、およびそれらが適用されるフレームワークとバージョンの完全な一覧については、「 [WDF のコールバックとメソッドの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)」を参照してください。

Windows 10 での KMDF ドライバーの新機能の詳細については、「 [WDF drivers の新](index.md)機能」を参照してください。

## <a name="kmdf-version-129"></a>KMDF バージョン1.29

バージョン1.25 から変更されていません。

## <a name="kmdf-version-127"></a>KMDF バージョン1.27

バージョン1.25 から変更されていません。

## <a name="kmdf-version-125"></a>KMDF バージョン1.25

* [複数のバージョンの Windows の WDF ドライバーをビルドする](building-a-wdf-driver-for-multiple-versions-of-windows.md)

## <a name="kmdf-version-123"></a>KMDF バージョン1.23

* 内部使用のためだけに追加されたコンパニオン機能。  新しい DDIs については、「 [WDF のコールバックとメソッドの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)」を参照してください。

## <a name="kmdf-version-121"></a>KMDF バージョン1.21

* [**WdfFileObjectGetInitiatorProcessId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetinitiatorprocessid)は以前は UMDF のみで、kmdf で使用できるようになりました。
* [**WdfRequestGetRequestorProcessId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetrequestorprocessid)は以前は UMDF のみで、kmdf で使用できるようになりました。
* [**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual):*ファイル*パラメーターの型が PCHAR から pcch に変更されました。
* [**Wdfobjectreferenceactual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual):*ファイル*パラメーターの型が PCHAR から pcch に変更されました。

## <a name="kmdf-version-119"></a>KMDF バージョン1.19

* [ **Wdfdmatransactionsetsingletransferrequirement 要件**を追加しました](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetsingletransferrequirement)
* [**WDF_DMA_ENABLER_CONFIG_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/ne-wdfdmaenabler-_wdf_dma_enabler_config_flags)に**WDF_DMA_ENABLER_CONFIG_REQUIRE_SINGLE_TRANSFER**フラグを追加しました
* [**Wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)および[**WdfdmatransactiondmacomSTATUS_WDF_TOO_MANY_TRANSFERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)の戻り値が追加されました
* 1回の転送出力の出力メッセージを[ **! wdfkd. wdfdmatransaction**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction)と[ **! wdfdmaenabler**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler)に追加しました
* シングル転送 DMA の詳細については、「[シングル転送 dma の使用](using-single-transfer-dma.md)」を参照してください。

## <a name="kmdf-version-115"></a>KMDF バージョン1.15

-   新しい[**WdfDeviceOpenDevicemapKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopendevicemapkey)メソッドを使用すると、ドライバーは**HKEY\_ローカル\_マシン\\ハードウェア\\DEVICEMAP**のサブキーと値にアクセスできます。

## <a name="kmdf-version-113"></a>KMDF バージョン1.13


KMDF バージョン1.13 では、次の機能が追加されています。

-   **CanWakeDevice**メンバーを[**WDF\_INTERRUPT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体に追加して、デバイスを低電力の Dx 状態から完全な D0 状態に戻すために使用できる割り込みをサポートするようになりました。 詳細については、「[割り込みを使用したデバイスのスリープ解除](using-an-interrupt-to-wake-a-device.md)」を参照してください。
-   高解像度タイマーのサポート。 詳細については、「[タイマーの使用](using-timers.md)」を参照してください。
-   システムが低電力状態のときにシステムをスリープ解除しない場合のタイマーのサポート。 詳細については、「[タイマーの使用](using-timers.md)」を参照してください。
-   「[統合されたデバイスのプロパティモデルにアクセスする](accessing-the-unified-device-property-model.md)」で説明されている、次の kmdf/UMDF メソッド。
    -   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
    -   [**Wdfdevice割り当てプロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
    -   [**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)
    -   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)
    -   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
    -   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

UMDF バージョンの詳細については、「 [Umdf Version History](umdf-version-history.md)」を参照してください。

## <a name="kmdf-version-111"></a>KMDF バージョン1.11


バージョン1.11 では、次の機能が追加されています。

-   [システムモードの DMA](supporting-system-mode-dma.md)

-   [パッシブレベルの割り込み](supporting-passive-level-interrupts.md)のサポート

-   1つのデバイス内の複数のコンポーネントの[機能力状態](supporting-functional-power-states.md)

-   [Irp を i/o キューにディスパッチする](dispatching-irps-to-i-o-queues.md)
-   次のメソッドがあります。
    -   [**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)
    -   [**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)
    -   [**WdfDeviceInitSetRemoveLockOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetremovelockoptions)
    -   [**WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)
    -   [**WdfDmaEnablerConfigureSystemProfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile)
    -   [**WdfDmaTransactionAllocateResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)
    -   [**WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)
    -   [**WdfDmaTransactionFreeResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionfreeresources)
    -   [**WdfDmaTransactionGetTransferInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongettransferinfo)
    -   [**Wdfdmatransactioninitializeenabled オフセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingoffset)
    -   [**WdfDmaTransactionSetChannelConfigurationCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetchannelconfigurationcallback)
    -   [**WdfDmaTransactionSetDeviceAddressOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetdeviceaddressoffset)
    -   [**WdfDmaTransactionSetImmediateExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetimmediateexecution)
    -   [**WdfDmaTransactionSetTransferCompleteCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsettransfercompletecallback)
    -   [**WdfDmaTransactionWdmGetTransferContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionwdmgettransfercontext)
    -   [**WdfInterruptQueueWorkItemForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)
    -   [**WdfInterruptReportActive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportactive)
    -   [**WdfInterruptReportInactive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)
    -   [**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)
    -   [**WdfIoQueueStopAndPurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurge)
    -   [**WdfIoQueueStopAndPurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)
    -   [**WdfIoTargetPurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge)
    -   [**WdfUsbTargetDeviceCreateIsochUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)
    -   [**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)
    -   [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)
    -   [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)
-   [*EvtDeviceUsageNotificationEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification_ex)を追加しました。

-   **IdleTimeoutType**および**ExcludeD3Cold**メンバーが[**WDF\_デバイス\_電源\_ポリシー\_アイドル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)に追加されました。

-   **ReportInactiveOnPowerDown**メンバーを[**WDF\_INTERRUPT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)に追加しました。

-   [**WDF\_IO\_ターゲット\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)に、 **Wdfiotargetpurged**値が追加されました。

-   WDF に**Wdfspecial Fileboot**値が追加されました。[**特別な\_ファイル\_の種類\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_special_file_type)ます。

-   [フレームワークベースのドライバーをデバッグするためのレジストリ値](registry-values-for-debugging-kmdf-drivers.md)に**DbgWaitForSignalTimeoutInSec**を追加しました。

-   [InstallWdf](https://go.microsoft.com/fwlink/p/?linkid=256122)、 [MultiComp](https://go.microsoft.com/fwlink/p/?linkid=256158)、 [SingleComp](https://go.microsoft.com/fwlink/p/?linkid=256158)の各サンプルを追加しました。

## <a name="kmdf-version-19"></a>KMDF バージョン1.9


バージョン1.9 では、次の機能が追加されています。

-   I/o キューの[事前処理が保証](guaranteeing-forward-progress-of-i-o-operations.md)されます

-   子デバイスの i/o キューから親デバイスの i/o キューへの[キュー i/o 要求](requeuing-i-o-requests.md)がサポートされるようになりました。

-   個々のキューオブジェクトに対して[キューレベルの同期](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_synchronization_scope)を指定する機能。

-   次のメソッドがあります。
    -   [**WdfDeviceGetSystemPowerAction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetsystempoweraction)
    -   [**WdfDeviceRemoveDependentUsageDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceremovedependentusagedeviceobject)
    -   [**WdfInterruptSetExtendedPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsetextendedpolicy)
    -   [**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent)
    -   [**Wdfpdoinit割り当ての Containerid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigncontainerid)
    -   [**WdfPreDeviceInstallEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstallex)
    -   [**WdfRequestForwardToParentDeviceIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)
    -   [**WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)
-   **Numberofpresentedrequests**メンバーが[**WDF\_IO\_QUEUE\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構造体に追加されたため、ドライバーが並列 i/o キューからドライバーに提供する i/o 要求の数を制限できるようになりました。

-   **Wdffileobjectcanbeoptional**フラグを[**WDF\_FILEOBJECT\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_fileobject_class)構造体に追加しました。

-   **TolerableDelay**メンバーを[**WDF\_TIMER\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config)構造体に追加しました。

-   [WdfDefaultIdleInWorkingState および WdfDefaultWakeFromSleepState](user-control-of-device-idle-and-wake-behavior.md)レジストリ値が追加されました。

## <a name="kmdf-version-17"></a>KMDF バージョン1.7


-   [**Wdfdeviceenqueuerequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)メソッドは、IRQL&lt;= ディスパッチ\_レベルで呼び出すことができます。

-   指定された作業項目が既に作業項目キューにある場合は、 [**Wdfworkitemenqueue キュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)メソッドを呼び出すことができます。

-   [*EvtDeviceArmWakeFromSxWithReason*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason)イベントコールバック関数が追加されました。

-   [**WDF\_デバイス\_電源\_ポリシー\_WAKE\_SETTINGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)構造体に**ArmForWakeIfChildrenAreArmedForWake**メンバーと**IndicateChildWakeOnParentWake**メンバーを追加しました。

## <a name="kmdf-version-15"></a>KMDF バージョン1.5


-   [**WdfUsbInterfaceGetNumSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumsettings)

-   **Driverpooltag**メンバーを[**WDF\_DRIVER\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)に追加しました。

## <a name="kmdf-version-11"></a>KMDF バージョン1.1


-   次のメソッドがあります。
    -   [**WdfCommonBufferCreateWithConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig)
    -   [**WdfDmaEnablerGetFragmentLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablergetfragmentlength)
    -   [**WdfDmaEnablerWdmGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter)

## <a name="kmdf-version-10"></a>KMDF バージョン1.0


最初のリリース。

 

 





