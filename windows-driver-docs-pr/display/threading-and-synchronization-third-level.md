---
title: スレッド処理と 3 番目のレベルの同期
description: スレッド処理と 3 番目のレベルの同期
ms.assetid: 780d37d9-40c6-4737-9042-473810868227
keywords:
- WDK 表示スレッド処理、第 3 レベルします。
- 同期の WDK の表示、3 番目のレベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 647c5fd9bae10c25aa7f6dedcef25d2e3a0214ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559871"
---
# <a name="threading-and-synchronization-third-level"></a>スレッド処理と 3 番目のレベルの同期


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

 

 





