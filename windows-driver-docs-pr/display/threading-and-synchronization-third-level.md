---
title: スレッドおよび同期の第 3 レベル
description: スレッドおよび同期の第 3 レベル
ms.assetid: 780d37d9-40c6-4737-9042-473810868227
keywords:
- スレッド WDK 表示、第3レベル
- 同期 WDK 表示、第3レベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54eddac923f5bab1972a2977e9608bfcb7e5461a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829322"
---
# <a name="threading-and-synchronization-third-level"></a>スレッドおよび同期の第 3 レベル


Windows Display Driver Model (WDDM) では、表示ミニポートドライバーへの次の呼び出しが、スレッド処理と同期の3番目のレベルで行われることが保証されています。 これにより、1つのスレッド (つまり、呼び出し元のスレッド) だけがドライバー内にあることが保証されます。 さらに、グラフィックスハードウェアがアイドル状態であり、ダイレクトメモリアクセス (DMA) バッファーが現在ドライバーによって処理されていないか、GPU スケジューラを通過しており、ビデオメモリがホストの CPU メモリに完全に削除されています。

-   [*DxgkDdiAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device)

-   [*DxgkDdiQueryChildRelations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)

-   [*DxgkDdiRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_remove_device)

-   [*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)

-   [*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)

-   [*DxgkDdiSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state)

-   [*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)

-   [*DxgkDdiStopDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)

-   [*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_unload)

 

 





