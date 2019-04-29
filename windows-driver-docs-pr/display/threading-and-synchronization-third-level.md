---
title: スレッドおよび同期の第 3 レベル
description: スレッドおよび同期の第 3 レベル
ms.assetid: 780d37d9-40c6-4737-9042-473810868227
keywords:
- WDK 表示スレッド処理、第 3 レベルします。
- 同期の WDK の表示、3 番目のレベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 647c5fd9bae10c25aa7f6dedcef25d2e3a0214ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389841"
---
# <a name="threading-and-synchronization-third-level"></a>スレッドおよび同期の第 3 レベル


Windows 表示 Driver Model (WDDM) は、スレッドと同期の第 3 レベルの下で、ディスプレイのミニポート ドライバーを次の呼び出しが行われることを保証します。 これにより、1 つのスレッド (つまり、呼び出し元のスレッド) のみが、ドライバー内にあります。 さらに、グラフィックス ハードウェアがアイドル状態、いいえダイレクト メモリ アクセス (DMA) バッファーを現在されているドライバーで処理する場合や、GPU のスケジューラを通過し、ビデオ メモリが CPU メモリをホストする完全に削除されます。

-   [*DxgkDdiAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559586)

-   [*DxgkDdiQueryChildRelations*](https://msdn.microsoft.com/library/windows/hardware/ff559750)

-   [*DxgkDdiRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559789)

-   [*DxgkDdiResetFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559815)

-   [*DxgkDdiRestartFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559820)

-   [*DxgkDdiSetPowerState*](https://msdn.microsoft.com/library/windows/hardware/ff560764)

-   [*DxgkDdiStartDevice*](https://msdn.microsoft.com/library/windows/hardware/ff560775)

-   [*DxgkDdiStopDevice*](https://msdn.microsoft.com/library/windows/hardware/ff560781)

-   [*DxgkDdiUnload*](https://msdn.microsoft.com/library/windows/hardware/ff560801)

 

 





