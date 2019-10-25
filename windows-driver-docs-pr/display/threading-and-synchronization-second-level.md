---
title: スレッドおよび同期の第 2 レベル
description: スレッドおよび同期の第 2 レベル
ms.assetid: 2b7c1eae-6527-469e-a2fa-74d2a1246bd3
keywords:
- スレッド WDK 表示、第2レベル
- 同期 WDK 表示、第2レベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fbf1260d74e23b66fc624b225153c87630b34eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829324"
---
# <a name="threading-and-synchronization-second-level"></a>スレッドおよび同期の第 2 レベル


2番目のレベルのスレッド処理と同期は[3 番目](threading-and-synchronization-third-level.md)のレベルと同じですが、ビデオメモリがホストの CPU メモリに対して削除されない点が異なります。 つまり、Windows Display Driver Model (WDDM) は、1つのスレッド (つまり、呼び出し元のスレッド) がディスプレイミニポートドライバー内にあり、グラフィックスハードウェアがアイドル状態であり、ダイレクトメモリアクセス (DMA) バッファーが現在処理されていないことを保証します。ドライバーまたは GPU スケジューラによって渡された。 ディスプレイミニポートドライバーの次の呼び出しは、第2レベルで行われます。

**注**   2 番目のレベルでいくつかの呼び出しを行うには、 **Dxgkarg\_ESCAPE**のメンバーである**D3DDDI\_ESCAPEFLAGS**構造体内で、**ハードウェアアクセス**フラグが設定されている必要があります。 このフラグが設定されていない場合、呼び出しは失敗します。

 

-   [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)

-   [*DxgkDdiControlInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)

-   [*DxgkDdiDispatchIoRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dispatch_io_request)

-   [*DxgkDdiEscape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)

-   [*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)

-   [*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)

-   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)

-   [*DxgkDdiRecommendMonitorModes*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendmonitormodes)

-   [*DxgkDdiSetPalette*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpalette)

-   [*DxgkDdiSetTimingsFromVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settimingsfromvidpn)

-   [*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))

-   [*DxgkDdiSetVidPnSourceVisibility*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourcevisibility)

-   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)

 

 





