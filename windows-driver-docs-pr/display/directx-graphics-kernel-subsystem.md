---
title: DirectX グラフィックス カーネル サブシステム
description: Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) は、ディスプレイのミニポート ドライバーによって呼び出される関数を実装します。
ms.assetid: 7601c761-bdab-4d18-8a84-7d69a71ec41c
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: bca6196b5e14d5138e4bbb81e2a55a8756c49075
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327942"
---
# <a name="directx-graphics-kernel-subsystem-dxgkrnlsys"></a>DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys)

このトピックでは、Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) を通じて、Windows オペレーティング システムを実装するカーネル モード インターフェイスについて説明します。

ポートのディスプレイ ドライバーは、DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) の 1 つの部分です。 ディスプレイのミニポート ドライバーは、ディスプレイ アダプターの製造元によって実装されます。 DirectX グラフィックスのカーネル サブシステムによって実装されるその他の関数の説明については、次のトピックを参照してください。

[VidPN オブジェクトとインターフェイス](vidpn-objects-and-interfaces.md)

[パスに依存しない回転をサポートしています。](supporting-path-independent-rotation.md)

[追加のモニター ターゲット モードを取得します。](obtaining-additional-monitor-target-modes.md)

ディスプレイのミニポート ドライバーによって実装される関数の説明については、カーネル モード インターフェイスを実装して、表示ミニポート ドライバーを参照してください。

## <a name="dxgkrnl-interface"></a>Dxgkrnl インターフェイス

DirectX グラフィックスのカーネル サブシステム (*Dxgkrnl.sys*) で、次の表の関数へのポインターを渡すことによって、ディスプレイのミニポート ドライバーを提供します、 [DXGKRNL_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgkrnl_interface)構造体をディスプレイ ミニポート ドライバーの[DxgkDdiStartDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)関数。 DXGKRNL_INTERFACE 構造体には、特定のディスプレイ アダプター (ポートのディスプレイ ドライバーによって生成された) ハンドルも含まれます。 ディスプレイのミニポート ドライバーは、DXGKRNL_INTERFACE で任意の関数を呼び出すたびに、引数としてそのハンドルを渡します。



|Dxgkrnl.sys||
|:---|:---|
|DxgkInitialize|(カーネル モードの表示専用ドライバーによってのみ呼び出されます) DxgkInitializeDisplayOnlyDriver (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|
|DxgkCbAcquirePostDisplayOwnership (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbCompleteFStateTransition (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|
|DxgkCbCreateContextAllocation (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbDestroyContextAllocation (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|
|DxgkCbEnumHandleChildren|DxgkCbEvalAcpiMethod|
|DxgkCbExcludeAdapterAccess|DxgkCbGetCaptureAddress|
|DxgkCbGetDeviceInformation|DxgkCbGetHandleData|
|DxgkCbGetHandleParent|DxgkCbIndicateChildStatus|
|DxgkCbIsDevicePresent|DxgkCbLogEtwEvent|
|DxgkCbMapMemory|DxgkCbNotifyDpc|
|DxgkCbNotifyInterrupt|DxgkCbPowerRuntimeControlRequest (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|
|(カーネル モードの表示専用ドライバーによってのみ呼び出されます) DxgkCbPresentDisplayOnlyProgress (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbQueryMonitorInterface|
|DxgkCbQueryServices|DxgkCbQueryVidPnInterface|
|DxgkCbQueueDpc|DxgkCbReadDeviceSpace|
|DxgkCbSetPowerComponentActive (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbSetPowerComponentIdle (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|
|DxgkCbSetPowerComponentLatency (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbSetPowerComponentResidency (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|
|DxgkCbSynchronizeExecution|DxgkCbUnmapMemory|
|DxgkCbWriteDeviceSpace|DxgkCbIsDevicePresent|
|DxgkCbGetHandleData|DxgkCbGetHandleParent|
|DxgkCbEnumHandleChildren|DxgkCbNotifyInterrupt|
|DxgkCbNotifyDpc|DxgkCbQueryVidPnInterface|
|DxgkCbQueryMonitorInterface|DxgkCbGetCaptureAddress|
|DxgkCbLogEtwEvent|DxgkCbExcludeAdapterAccess|
|DxgkCbCreateContextAllocation|DxgkCbDestroyContextAllocation|
|DxgkCbSetPowerComponentActive|DxgkCbSetPowerComponentIdle|
|DxgkCbPowerRuntimeControlRequest||

## <a name="agp-interface"></a>AGP インターフェイス

次の関数は、オペレーティング システムによって実装され、AGP (高速のグラフィックス ポート) をサポートするためにディスプレイのミニポート ドライバーによって呼び出されます。 ディスプレイのミニポート ドライバーでは、これらの関数へのポインターを取得 DXGK_SERVICES 列挙型から DxgkServicesAgp 値を渡すことで、 *ServicesType*のパラメーター、 [DxgkCbQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_query_services)関数。

|AGP 関数|
|:---|
|[AgpAllocatePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_agp_allocate_pool)|
|[AgpFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_agp_free_pool)|
|[AgpSetCommand](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_agp_set_command)|


## <a name="debug-report-interface"></a>レポート インターフェイスをデバッグします。


ディスプレイのミニポート ドライバーを渡すことによって、次の関数へのポインターを取得する、 *DxgkServicesDebugReport* 、DXGK_SERVICES 列挙型の値、 *ServicesType*のパラメーター、[DxgkCbQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_query_services)関数。 これらの関数を使用してアクセスされる、 [_DXGK_DEBUG_REPORT_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_debug_report_interface)構造体。

|デバッグ レポート関数|
|:---|
|DbgReportComplete|
|DbgReportCreate|
|DbgReportSecondaryData|

## <a name="timed-operation-interface"></a>インターフェイスの操作がタイムアウトしました

ディスプレイのミニポート ドライバーを渡すことによって、次の関数へのポインターを取得する、 *DxgkServicesTimedOperation* 、DXGK_SERVICES 列挙型の値、 *ServicesType*のパラメーター[DxgkCbQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_query_services)関数。 DxgkCbQueryServices のメンバーでは、上記の関数へのポインターを返します、 [DXGK_TIMED_OPERATION_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_timed_operation_interface)構造;、display ミニポート ドライバーに DXGK_TIMED_OPERATION_INTERFACE へのポインターを提供する、*インターフェイス*DxgkCbQueryServices のパラメーター。

|時間操作関数|
|:---|
|TimedOperationStart|
|TimedOperationDelay|
|TimedOperationWaitForSingleObject|

## <a name="see-also"></a>関連項目

[Windows Display Driver Model (WDDM) アーキテクチャ](windows-vista-and-later-display-driver-model-architecture.md)

[表示のミニポート ドライバーの初期化](initializing-the-display-miniport-driver.md)

