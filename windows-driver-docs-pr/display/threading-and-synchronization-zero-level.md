---
title: スレッドおよび同期の 0 レベル
description: スレッドおよび同期の 0 レベル
ms.assetid: 2baf91e8-fafb-40e2-a24c-cbf04fe45274
keywords:
- WDK の表示、レベル 0 個のスレッド処理
- WDK の表示、0 レベルの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df93ebad8394a9587edc3d07f2bb751cbe7e921a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385563"
---
# <a name="threading-and-synchronization-zero-level"></a>スレッドおよび同期の 0 レベル


Windows 表示 Driver Model (WDDM) は、再入可能な方法で作成する、ディスプレイのミニポート ドライバーを次の呼び出しを許可します。 複数のスレッドでは、次の関数を呼び出すことによって、ドライバーは入力できます同時に。

**注**   2 つのスレッドが 1 つのプロセスに属することができますが、2 つまたは複数のスレッドは、ドライバーで同時に実行できます、します。

 

-   [*DxgkDdiCloseAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_closeallocation)

-   [*DxgkDdiCollectDbgInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)
    **注**  [*DxgkDdiCollectDbgInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)のさまざまなデバッグ情報を収集する必要がありますエラーと高の IRQL でいつでも呼び出すことができます (は、IRQL を*DxgkDdiCollectDbgInfo*で実行されますが一般に未定義)。 いずれの場合も、 *DxgkDdiCollectDbgInfo*適切な同期の必要なデバッグ情報の可用性を確認する必要があります。 ただし場合、**理由**のメンバー、 [ **DXGKARG\_COLLECTDBGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_collectdbginfo)構造体、 *pCollectDbgInfo*パラメーターの*DxgkDdiCollectDbgInfo*へのポインターに設定されている[ビデオ\_TDR\_タイムアウト\_検出](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)または[ビデオ\_エンジン\_タイムアウト\_検出](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)、ドライバーを確認する必要がありますを*DxgkDdiCollectDbgInfo*ページング可能なは、IRQL で実行 =**パッシブ\_レベル**同期 0 レベルをサポートしています。

     

-   [*DxgkDdiControlEtwLogging*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_control_etw_logging)

-   [*DxgkDdiCreateAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)

-   [*DxgkDdiCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)

-   [*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)

-   [*DxgkDdiDescribeAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_describeallocation)

-   [*DxgkDdiDestroyAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyallocation)

-   [*DxgkDdiDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_destroycontext)

-   [*DxgkDdiDestroyDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_destroydevice)

-   [*DxgkDdiDpcRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_dpc_routine)

-   [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)

-   [*DxgkDdiGetScanLine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)

-   [*DxgkDdiGetStandardAllocationDriverData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)

-   [*DxgkDdiInterruptRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)

-   [*DxgkDdiIsSupportedVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)

-   [*DxgkDdiMiracastCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)

-   [*DxgkDdiMiracastDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)

-   [*DxgkDdiMiracastIoControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)

-   [*DxgkDdiMiracastQueryCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps)

-   [*DxgkDdiOpenAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_openallocationinfo)

-   [*DxgkDdiPresent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_present)

-   [*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)

-   [*DxgkDdiQueryCurrentFence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_querycurrentfence)

-   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)

-   [*DxgkDdiRecommendVidPnTopology*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology)

-   [*DxgkDdiRender*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_render)

-   [*DxgkDdiRenderKm*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)

-   [*DxgkDdiResetDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_reset_device)

 

 





