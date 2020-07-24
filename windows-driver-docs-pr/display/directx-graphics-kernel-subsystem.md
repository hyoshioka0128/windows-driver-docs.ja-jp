---
title: DirectX グラフィックス カーネル サブシステム
description: Microsoft DirectX グラフィックスカーネルサブシステム (Dxgkrnl.sys) は、ディスプレイミニポートドライバーによって呼び出される関数を実装します。
ms.assetid: 7601c761-bdab-4d18-8a84-7d69a71ec41c
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2ef293a0b13c242bc701794113fa38171b06b307
ms.sourcegitcommit: df50dc10210c124f2c7fb173d6e4fb796f56e5bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949694"
---
# <a name="directx-graphics-kernel-subsystem-dxgkrnlsys"></a>DirectX グラフィックスカーネルサブシステム (Dxgkrnl.sys)

このトピックでは、Windows オペレーティングシステムが Microsoft DirectX graphics カーネルサブシステム (Dxgkrnl.sys) を介して実装するカーネルモードインターフェイスを示します。

ディスプレイポートドライバーは、DirectX グラフィックスのカーネルサブシステム (Dxgkrnl.sys) の1つの部分です。 ディスプレイミニポートドライバーは、ディスプレイアダプターのベンダによって実装されます。 DirectX グラフィックスカーネルサブシステムによって実装される他の関数の説明については、次のトピックを参照してください。

[VidPN オブジェクトおよびインターフェイス](vidpn-objects-and-interfaces.md)

[パスに依存しない回転のサポート](supporting-path-independent-rotation.md)

[追加のモニター ターゲット モードの取得](obtaining-additional-monitor-target-modes.md)

ディスプレイミニポートドライバーによって実装される関数の説明については、「ディスプレイミニポートドライバーによって実装されるカーネルモードインターフェイス」を参照してください。

## <a name="dxgkrnl-interface"></a>Dxgkrnl インターフェイス

DirectX グラフィックスカーネルサブシステム (*Dxgkrnl.sys*) では、ディスプレイミニポートドライバーの[DxgkDdiStartDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)関数に[DXGKRNL_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgkrnl_interface)構造体を渡すことによって、次の表に示す関数へのポインターが表示されます。 DXGKRNL_INTERFACE 構造体には、特定のディスプレイアダプターに対して (ディスプレイポートドライバーによって生成される) ハンドルも含まれます。 表示ミニポートドライバーは、DXGKRNL_INTERFACE 内の関数のいずれかを呼び出すたびに、そのハンドルを引数として渡します。

* DxgkInitialize
* DxgkInitializeDisplayOnlyDriver (カーネルモードの表示専用ドライバーによってのみ呼び出されます) (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbAcquirePostDisplayOwnership (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbCompleteFStateTransition (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbCreateContextAllocation (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbDestroyContextAllocation (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbEnumHandleChildren
* DxgkCbEvalAcpiMethod
* DxgkCbExcludeAdapterAccess
* DxgkCbGetCaptureAddress
* DxgkCbGetDeviceInformation
* DxgkCbGetHandleData
* DxgkCbGetHandleParent
* DxgkCbIndicateChildStatus
* DxgkCbIsDevicePresent
* DxgkCbLogEtwEvent
* DxgkCbMapMemory
* DxgkCbNotifyDpc
* DxgkCbNotifyInterrupt
* DxgkCbPowerRuntimeControlRequest (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* Dxgkcbdisplayonlyprogress (カーネルモードの表示専用ドライバーによってのみ呼び出されます) (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbQueryMonitorInterface
* DxgkCbQueryServices
* DxgkCbQueryVidPnInterface
* DxgkCbQueueDpc
* DxgkCbReadDeviceSpace
* DxgkCbSetPowerComponentActive (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbSetPowerComponentIdle (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbSetPowerComponentLatency (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbSetPowerComponentResidency (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)
* DxgkCbSynchronizeExecution
* DxgkCbUnmapMemory
* DxgkCbWriteDeviceSpace
* DxgkCbIsDevicePresent
* DxgkCbGetHandleData
* DxgkCbGetHandleParent
* DxgkCbEnumHandleChildren
* DxgkCbNotifyInterrupt
* DxgkCbNotifyDpc
* DxgkCbQueryVidPnInterface
* DxgkCbQueryMonitorInterface
* DxgkCbGetCaptureAddress
* DxgkCbLogEtwEvent
* DxgkCbExcludeAdapterAccess
* DxgkCbCreateContextAllocation
* DxgkCbDestroyContextAllocation
* DxgkCbSetPowerComponentActive
* DxgkCbSetPowerComponentIdle
* DxgkCbPowerRuntimeControlRequest

## <a name="agp-interface"></a>AGP インターフェイス

次の関数はオペレーティングシステムによって実装され、AGP (Accelerated Graphics Port) をサポートするためにディスプレイミニポートドライバーによって呼び出されます。 表示ミニポートドライバーは、Dxgkサービスの値を DXGK_SERVICES 列挙型から[Dxgkcbqueryservices](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_query_services)関数の*servicestype*パラメーターに渡すことによって、これらの関数へのポインターを取得します。

* [AgpAllocatePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_agp_allocate_pool)
* [AgpFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_agp_free_pool)
* [AgpSetCommand](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_agp_set_command)


## <a name="debug-report-interface"></a>デバッグレポートインターフェイス


表示ミニポートドライバーは、 *Dxgkサービス*の値を DXGK_SERVICES 列挙型から[Dxgkservicesdebugreport](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_query_services)関数の*servicestype*パラメーターに渡すことによって、次の関数へのポインターを取得します。 これらの関数には、 [_DXGK_DEBUG_REPORT_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_debug_report_interface)構造体を使用してアクセスします。

* DbgReportComplete
* DbgReportCreate
* DbgReportSecondaryData

## <a name="timed-operation-interface"></a>時間指定操作インターフェイス

表示ミニポートドライバーは、DXGK_SERVICES 列挙型の*DxgkServicesTimedOperation*値を[Dxgkcbqueryservices](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_query_services)関数の*servicestype*パラメーターに渡すことによって、次の関数へのポインターを取得します。 DxgkCbQueryServices は、前のリストの関数へのポインターを[DXGK_TIMED_OPERATION_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_timed_operation_interface)構造体のメンバーに返します。表示ミニポートドライバーは、DxgkCbQueryServices の*INTERFACE*パラメーターに DXGK_TIMED_OPERATION_INTERFACE へのポインターを提供します。

* TimedOperationStart
* TimedOperationDelay
* TimedOperationWaitForSingleObject

## <a name="see-also"></a>関連項目

[Windows Display Driver Model (WDDM) のアーキテクチャ](windows-vista-and-later-display-driver-model-architecture.md)

[ディスプレイ ミニポート ドライバーの初期化](initializing-the-display-miniport-driver.md)

