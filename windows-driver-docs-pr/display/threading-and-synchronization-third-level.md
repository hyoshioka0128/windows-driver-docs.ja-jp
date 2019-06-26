---
title: スレッドおよび同期の第 3 レベル
description: スレッドおよび同期の第 3 レベル
ms.assetid: 780d37d9-40c6-4737-9042-473810868227
keywords:
- WDK 表示スレッド処理、第 3 レベルします。
- 同期の WDK の表示、3 番目のレベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a5c71dcc40e28daa3dcee3db284f16beb506309
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354692"
---
# <a name="threading-and-synchronization-third-level"></a>スレッドおよび同期の第 3 レベル


Windows 表示 Driver Model (WDDM) は、スレッドと同期の第 3 レベルの下で、ディスプレイのミニポート ドライバーを次の呼び出しが行われることを保証します。 これにより、1 つのスレッド (つまり、呼び出し元のスレッド) のみが、ドライバー内にあります。 さらに、グラフィックス ハードウェアがアイドル状態、いいえダイレクト メモリ アクセス (DMA) バッファーを現在されているドライバーで処理する場合や、GPU のスケジューラを通過し、ビデオ メモリが CPU メモリをホストする完全に削除されます。

-   [*DxgkDdiAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_add_device)

-   [*DxgkDdiQueryChildRelations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)

-   [*DxgkDdiRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_remove_device)

-   [*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)

-   [*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)

-   [*DxgkDdiSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_set_power_state)

-   [*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)

-   [*DxgkDdiStopDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_stop_device)

-   [*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_unload)

 

 





