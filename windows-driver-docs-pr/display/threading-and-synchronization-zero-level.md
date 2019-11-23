---
title: スレッドおよび同期の 0 レベル
description: スレッドおよび同期の 0 レベル
ms.assetid: 2baf91e8-fafb-40e2-a24c-cbf04fe45274
keywords:
- スレッド WDK 表示、ゼロレベル
- 同期 WDK 表示、ゼロレベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abd1eaece8bad4107c4d2125228e91b56065d7e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825490"
---
# <a name="threading-and-synchronization-zero-level"></a>スレッドおよび同期の 0 レベル


Windows Display Driver Model (WDDM) を使用すると、ディスプレイミニポートドライバーへの次の呼び出しを再入可能な方法で行うことができます。 つまり、次の関数を呼び出すことによって、複数のスレッドが同時にドライバーに入ることができます。

**注**   同時に複数のスレッドをドライバーで実行することはできますが、1つのプロセスに属することができるスレッドは2つありません。

 

-   [*DxgkDdiCloseAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_closeallocation)

-   [*DxgkDdiCollectDbgInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)
    **Note**  [*DxgkDdiCollectDbgInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)は、さまざまなエラーのデバッグ情報を収集する必要があります。また、いつでも高い irql で呼び出すことができます (つまり、 *DxgkDdiCollectDbgInfo*がで実行される irql は一般に未定義です)。 いずれの場合も、 *DxgkDdiCollectDbgInfo*は、必要なデバッグ情報と適切な同期が使用可能かどうかを確認する必要があります。 ただし、 [TDR\_TIMEOUT\_検出さ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)れた、または[ビデオ\_エンジン\_タイムアウト\_検出](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)された場合に、DxgkDdiCollectDbgInfo の*pcollectdbginfo*パラメーターによって指定されたの[**Collectdbginfo 構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_collectdbginfo)の**Reason**メンバーが\_VIDEO に設定されていると、ドライバーは*DxgkDdiCollectDbgInfo*がページング可能であること、および同期**のゼロレベル**をサポートする必要があり\_

     

-   [*DxgkDdiControlEtwLogging*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_control_etw_logging)

-   [*DxgkDdiCreateAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)

-   [*DxgkDdiCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)

-   [*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)

-   [*DxgkDdiDescribeAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_describeallocation)

-   [*DxgkDdiDestroyAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyallocation)

-   [*DxgkDdiDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroycontext)

-   [*DxgkDdiDestroyDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroydevice)

-   [*DxgkDdiDpcRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dpc_routine)

-   [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)

-   [*DxgkDdiGetScanLine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)

-   [*DxgkDdiGetStandardAllocationDriverData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)

-   [*DxgkDdiInterruptRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)

-   [*DxgkDdiIsSupportedVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)

-   [*DxgkDdiMiracastCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)

-   [*DxgkDdiMiracastDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)

-   [*DxgkDdiMiracastIoControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)

-   [*DxgkDdiMiracastQueryCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps)

-   [*DxgkDdiOpenAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_openallocationinfo)

-   [*DxgkDdiPresent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)

-   [*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)

-   [*DxgkDdiQueryCurrentFence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querycurrentfence)

-   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)

-   [*DxgkDdiRecommendVidPnTopology*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology)

-   [*DxgkDdiRender*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)

-   [*DxgkDdiRenderKm*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)

-   [*DxgkDdiResetDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_reset_device)

 

 





