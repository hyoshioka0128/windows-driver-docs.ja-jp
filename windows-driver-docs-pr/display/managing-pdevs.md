---
title: PDEV の管理
description: PDEV の管理
ms.assetid: f7badbe8-b24f-438a-8937-95bb98de6310
keywords:
- PDEV WDK DirectDraw
- WDK DirectDraw、PDEV の描画
- DirectDraw WDK Windows 2000 display、PDEV
- 無効な PDEV WDK DirectDraw
- PDEV WDK DirectDraw の有効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82547f90b6dff1199cde6ee2d616b5fcc3f73257
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840582"
---
# <a name="managing-pdevs"></a>PDEV の管理


## <span id="ddk_managing_pdevs_gg"></span><span id="DDK_MANAGING_PDEVS_GG"></span>


**このトピックは、Windows 2000 以降にのみ適用されます。**

ディスプレイドライバーを呼び出すスレッドの数は、デバイス上の既存の PDEVs の数によって異なります。 各デバイスには、アダプターごとの最大有効の PDEV 出力と、無制限の数の無効な PDEVs があります。 PDEV が無効になっているか、ドライバーの[**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)関数を呼び出して有効になっています。 ディスプレイドライバーで無効になっている PDEVs が混在している場合、オペレーティングシステムは、1つのスレッドが有効な PDEV でドライバー関数を呼び出すことができます。同時に、複数のスレッドに対して、無効な PDEVs を持つドライバー関数の呼び出しを同時に許可します。 たとえば、有効な PDEV で[**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)が実行されていて、別の無効になっている pdev が[**DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)によって破棄されている可能性があります。 1つのディスプレイドライバーが複数の有効な PDEVs を管理している場合でも (たとえば、マルチモニターのシナリオで)、オペレーティングシステムでは、有効な PDEVs のいずれかを使用して、1つのスレッドだけがドライバーコードを呼び出すことができます。

ディスプレイドライバーが、PDEVs 間で共有されるグローバルリソースとハードウェアの状態を管理する必要がある場合は、表示ドライバーも必要な同期を処理する必要があります。 ディスプレイドライバーはセッション領域にマップされるので、各セッションには独自のグローバル変数セットがあります。 したがって、ミューテックスなどの同期オブジェクトを保持するために、display driver グローバル変数を使用することはできません。 代わりに、ビデオミニポートドライバーのデバイス拡張機能にミューテックスを格納します。これは、セッション領域ではなくグローバル空間にマップされます。 ビデオミニポートドライバーの[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)関数でミューテックスを初期化できます。 次に、ディスプレイドライバーの[**Drの Ablepdev**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)関数は、ビデオミニポートドライバーにカスタム IOCTL を送信することによって、ミューテックスへのポインターを取得できます。 別のセッションに属する表示ドライバースレッドには、ポインターの個別のコピーが含まれますが、これらのすべてのコピーは同じ mutex オブジェクトを指します。

ディスプレイドライバーは、ミューテックスを取得して解放するカーネルルーチンを直接呼び出すことは許可されていないため、ディスプレイドライバーはビデオミニポートドライバーを使用してこれらのタスクを実行する必要があります。 ビデオミニポートドライバーは、ミューテックスを取得して解放する関数を実装できます。また、表示ドライバーは、ミューテックス自体へのポインターを取得するために使用するのと同じカスタム IOCTL 内のその関数へのポインターを取得できます。

無効な PDEV を使用して呼び出すことができるのは、次の制限された数のドライバー関数だけです。

-   [*Ddmapmemory*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory) (メモリのマップ解除用)

-   [**DrvDisableDirectDraw**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledirectdraw)

-   [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) (システムメモリのみ)

-   [**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)

-   [**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)

-   [**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)

-   [*DdDestroySurface*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)

-   [*DdLock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)

-   [*DdUnlock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)

-   [*DestroyD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552754(v=vs.85))

-   [*LockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))

-   [*UnlockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570106(v=vs.85))

-   [**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)

-   [**DrvDisablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)

-   [**DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)

-   [**DrvResetPDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)

 

 





