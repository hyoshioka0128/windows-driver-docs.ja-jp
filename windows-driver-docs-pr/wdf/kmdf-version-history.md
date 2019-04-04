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
ms.openlocfilehash: 297fa37b477f2ef82ff53b7d6b6849add6cfcddb
ms.sourcegitcommit: 5cbc8ac1db572e92abeefebb39f5e72834785bc3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2019
ms.locfileid: "56754462"
---
# <a name="kmdf-version-history"></a>KMDF のバージョンの履歴


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) の Windows オペレーティング システム、および各リリースで行われた変更の対応するバージョンのバージョンを使用します。

次の表は、KMDF ライブラリのリリース履歴。

|KMDF バージョン|Release メソッド|このバージョンの Windows に含まれる|これを使用してドライバーを実行します。|
|--- |--- |--- |--- |
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

コールバックの完全な一覧とメソッド、およびどのフレームワークとバージョンに適用される、[WDF のコールバックの概要とメソッド](https://msdn.microsoft.com/library/windows/hardware/dn265591)を参照してください。

KMDF ドライバーを Windows 10 の新機能については、[WDF ドライバーの新](index.md)を参照してください。

## <a name="kmdf-version-127"></a>KMDF バージョン 1.27

版 1.25 から変更されていません。

## <a name="kmdf-version-125"></a>KMDF 版 1.25

* [複数のバージョンの Windows の WDF ドライバーをビルドする](building-a-wdf-driver-for-multiple-versions-of-windows.md)

## <a name="kmdf-version-123"></a>KMDF バージョン 1.23

* コンパニオンの機能は内部使用のみを追加します。  新しい Ddi を参照してください。 [WDF のコールバックの概要とメソッド](https://msdn.microsoft.com/library/windows/hardware/dn265591)します。

## <a name="kmdf-version-121"></a>KMDF バージョン 1.21

* [**WdfFileObjectGetInitiatorProcessId** ](https://msdn.microsoft.com/library/windows/hardware/dn265614) UMDF 専用以前、KMDF で利用可能にします。
* [**WdfRequestGetRequestorProcessId** ](https://msdn.microsoft.com/library/windows/hardware/dn265617) UMDF 専用以前、KMDF で利用可能にします。
* [**WdfObjectDereferenceActual**](https://msdn.microsoft.com/library/windows/hardware/ff548743):入力*ファイル*PCCH から PCHAR パラメーターに変更します。
* [**WdfObjectReferenceActual**](https://msdn.microsoft.com/library/windows/hardware/ff548760):入力*ファイル*PCCH から PCHAR パラメーターに変更します。

## <a name="kmdf-version-119"></a>KMDF バージョン 1.19

* 追加[ **WdfDmaTransactionSetSingleTransferRequirement**](https://msdn.microsoft.com/library/windows/hardware/988c7e70-3b2a-4a0f-91cf-dfab3ea07f05)
* 追加**WDF_DMA_ENABLER_CONFIG_REQUIRE_SINGLE_TRANSFER**フラグ[ **WDF_DMA_ENABLER_CONFIG_FLAGS**](https://msdn.microsoft.com/library/windows/hardware/hh439491)
* 追加**STATUS_WDF_TOO_MANY_TRANSFERS**の値を返す[ **WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)と[ **WdfDmaTransactionDmaCompleted**](https://msdn.microsoft.com/library/windows/hardware/ff547039)
* 1 つの転送に出力するための出力メッセージを追加[ **! wdfkd.wdfdmatransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff565721)と[ **! wdfkd.wdfdmaenabler**](https://msdn.microsoft.com/library/windows/hardware/ff565717)
* 1 つの転送 DMA に関する詳細については、[転送 DMA の 1 つを使用して](using-single-transfer-dma.md)を参照してください。

## <a name="kmdf-version-115"></a>KMDF バージョン 1.15

-   新しい[ **WdfDeviceOpenDevicemapKey** ](https://msdn.microsoft.com/library/windows/hardware/dn932458)メソッドは、サブキーをアクセスするためのドライバーを使用し、下に値**HKEY\_ローカル\_マシン\\ハードウェア\\DEVICEMAP**します。

## <a name="kmdf-version-113"></a>KMDF バージョン 1.13


KMDF バージョン 1.13 は、次の機能を追加します。

-   追加**CanWakeDevice**メンバー [ **WDF\_INTERRUPT\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552347)からデバイスを使用できる割り込みをサポートする構造体、低電力 Dx 状態は、完全に D0 状態に戻ります。 詳細については、[、割り込みを使用して、デバイスのスリープを解除する](using-an-interrupt-to-wake-a-device.md)を参照してください。
-   高解像度のタイマーをサポートします。 詳細については、[を使用してタイマー](using-timers.md)を参照してください。
-   システムが低電力状態の場合有効期限が切れる場合、システムがウェイクしないタイマーをサポートします。 詳細については、[を使用してタイマー](using-timers.md)を参照してください。
-   説明した次の KMDF/UMDF メソッド[デバイス プロパティの統合モデルにアクセスする](accessing-the-unified-device-property-model.md):
    -   [**WdfDeviceAllocAndQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265599)
    -   [**WdfDeviceAssignProperty**](https://msdn.microsoft.com/library/windows/hardware/dn265601)
    -   [**WdfDeviceInitSetIoTypeEx**](https://msdn.microsoft.com/library/windows/hardware/dn265604)
    -   [**WdfDeviceQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265608)
    -   [**WdfFdoInitAllocAndQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265612)
    -   [**WdfFdoInitQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265613)

UMDF バージョンについては、[UMDF バージョン履歴](umdf-version-history.md)を参照してください。

## <a name="kmdf-version-111"></a>KMDF Version 1.11


Version 1.11 は、次の機能を追加します。

-   [システム モードの DMA](supporting-system-mode-dma.md)

-   サポート[パッシブ レベルの割り込み](supporting-passive-level-interrupts.md)

-   [機能の電力状態](supporting-functional-power-states.md)1 台のデバイス内の複数のコンポーネント

-   [Irp の I/O キューへのディスパッチ](dispatching-irps-to-i-o-queues.md)
-   次のメソッド。
    -   [**WdfDeviceConfigureWdmIrpDispatchCallback**](https://msdn.microsoft.com/library/windows/hardware/hh451093)
    -   [**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://msdn.microsoft.com/library/windows/hardware/hh706196)
    -   [**WdfDeviceInitSetRemoveLockOptions**](https://msdn.microsoft.com/library/windows/hardware/hh451095)
    -   [**WdfDeviceWdmDispatchIrp**](https://msdn.microsoft.com/library/windows/hardware/hh451100)
    -   [**WdfDmaEnablerConfigureSystemProfile**](https://msdn.microsoft.com/library/windows/hardware/hh451108)
    -   [**WdfDmaTransactionAllocateResources**](https://msdn.microsoft.com/library/windows/hardware/hh451123)
    -   [**WdfDmaTransactionCancel**](https://msdn.microsoft.com/library/windows/hardware/hh451127)
    -   [**WdfDmaTransactionFreeResources**](https://msdn.microsoft.com/library/windows/hardware/hh451177)
    -   [**WdfDmaTransactionGetTransferInfo**](https://msdn.microsoft.com/library/windows/hardware/hh451179)
    -   [**WdfDmaTransactionInitializeUsingOffset**](https://msdn.microsoft.com/library/windows/hardware/hh451182)
    -   [**WdfDmaTransactionSetChannelConfigurationCallback**](https://msdn.microsoft.com/library/windows/hardware/hh451184)
    -   [**WdfDmaTransactionSetDeviceAddressOffset**](https://msdn.microsoft.com/library/windows/hardware/hh451188)
    -   [**WdfDmaTransactionSetImmediateExecution**](https://msdn.microsoft.com/library/windows/hardware/hh451190)
    -   [**WdfDmaTransactionSetTransferCompleteCallback**](https://msdn.microsoft.com/library/windows/hardware/hh439261)
    -   [**WdfDmaTransactionWdmGetTransferContext**](https://msdn.microsoft.com/library/windows/hardware/hh439267)
    -   [**WdfInterruptQueueWorkItemForIsr**](https://msdn.microsoft.com/library/windows/hardware/hh439270)
    -   [**WdfInterruptReportActive**](https://msdn.microsoft.com/library/windows/hardware/hh439273)
    -   [**WdfInterruptReportInactive**](https://msdn.microsoft.com/library/windows/hardware/hh439277)
    -   [**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)
    -   [**WdfIoQueueStopAndPurge**](https://msdn.microsoft.com/library/windows/hardware/hh439289)
    -   [**WdfIoQueueStopAndPurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/hh439293)
    -   [**WdfIoTargetPurge**](https://msdn.microsoft.com/library/windows/hardware/hh439338)
    -   [**WdfUsbTargetDeviceCreateIsochUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439420)
    -   [**WdfUsbTargetDeviceCreateUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439423)
    -   [**WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)
    -   [**WdfUsbTargetDeviceQueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh439434)
-   追加[ *EvtDeviceUsageNotificationEx*](https://msdn.microsoft.com/library/windows/hardware/hh406365)します。

-   追加**IdleTimeoutType**と**ExcludeD3Cold**メンバー [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff551270)します。

-   追加**ReportInactiveOnPowerDown**メンバー [ **WDF\_INTERRUPT\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff552347)します。

-   追加**WdfIoTargetPurged**値を[ **WDF\_IO\_ターゲット\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff552390)します。

-   追加**WdfSpecialFileBoot**値を[ **WDF\_特殊\_ファイル\_型**](https://msdn.microsoft.com/library/windows/hardware/ff552509)します。

-   追加**DbgWaitForSignalTimeoutInSec**に[Framework ベースのドライバーをデバッグするためのレジストリ値](registry-values-for-debugging-kmdf-drivers.md)します。

-   追加[InstallWdf](https://go.microsoft.com/fwlink/p/?linkid=256122)、 [MultiComp](https://go.microsoft.com/fwlink/p/?linkid=256158)、および[SingleComp](https://go.microsoft.com/fwlink/p/?linkid=256158)サンプル。

## <a name="kmdf-version-19"></a>KMDF バージョン 1.9


バージョン 1.9 には、次の機能が追加されます。

-   [進行を保証](guaranteeing-forward-progress-of-i-o-operations.md)の I/O キュー

-   サポート[requeuing の I/O 要求](requeuing-i-o-requests.md)親デバイスの I/O キューに子デバイスの I/O キューから

-   指定する機能[キュー レベルの同期](https://msdn.microsoft.com/library/windows/hardware/ff552518)の個々 のキュー オブジェクト。

-   次のメソッド。
    -   [**WdfDeviceGetSystemPowerAction**](https://msdn.microsoft.com/library/windows/hardware/ff546022)
    -   [**WdfDeviceRemoveDependentUsageDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff546829)
    -   [**WdfInterruptSetExtendedPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff547381)
    -   [**WdfPdoInitAllowForwardingRequestToParent**](https://msdn.microsoft.com/library/windows/hardware/ff548789)
    -   [**WdfPdoInitAssignContainerID**](https://msdn.microsoft.com/library/windows/hardware/ff548792)
    -   [**WdfPreDeviceInstallEx**](https://msdn.microsoft.com/library/windows/hardware/ff548839)
    -   [**WdfRequestForwardToParentDeviceIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549959)
    -   [**WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)
-   追加、 **NumberOfPresentedRequests**メンバーを[ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)ドライバーを絞り込むためにの構造体並列 I/O キューからドライバーにフレームワークを提供する要求の I/O の数。

-   追加、 **WdfFileObjectCanBeOptional**フラグを[ **WDF\_FILEOBJECT\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff551315)構造体。

-   追加、 **TolerableDelay**メンバーを[ **WDF\_タイマー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552519)構造体。

-   追加[WdfDefaultIdleInWorkingState と WdfDefaultWakeFromSleepState](user-control-of-device-idle-and-wake-behavior.md)レジストリの値。

## <a name="kmdf-version-17"></a>KMDF バージョン 1.7


-   [ **WdfDeviceEnqueueRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff545945) IRQL でメソッドを呼び出すことが&lt;= ディスパッチ\_レベル。

-   [ **WdfWorkItemEnqueue** ](https://msdn.microsoft.com/library/windows/hardware/ff551203)指定された作業項目が作業項目のキューが既にある場合、メソッドを呼び出すことができます。

-   追加、 [ *EvtDeviceArmWakeFromSxWithReason* ](https://msdn.microsoft.com/library/windows/hardware/ff540846)イベント コールバック関数。

-   追加**ArmForWakeIfChildrenAreArmedForWake**と**IndicateChildWakeOnParentWake**メンバーを[ **WDF\_デバイス\_POWER\_ポリシー\_WAKE\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff551277)構造体。

## <a name="kmdf-version-15"></a>KMDF バージョン 1.5


-   [**WdfUsbInterfaceGetNumSettings**](https://msdn.microsoft.com/library/windows/hardware/ff550070)

-   追加、 **DriverPoolTag**メンバー [ **WDF\_ドライバー\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551300)します。

## <a name="kmdf-version-11"></a>KMDF バージョン 1.1


-   次のメソッド。
    -   [**WdfCommonBufferCreateWithConfig**](https://msdn.microsoft.com/library/windows/hardware/ff545805)
    -   [**WdfDmaEnablerGetFragmentLength**](https://msdn.microsoft.com/library/windows/hardware/ff546986)
    -   [**WdfDmaEnablerWdmGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff547020)

## <a name="kmdf-version-10"></a>KMDF バージョン 1.0


最初のリリース。

 

 





