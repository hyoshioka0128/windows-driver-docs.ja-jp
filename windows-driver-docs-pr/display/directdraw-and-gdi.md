---
title: DirectDraw と GDI
description: DirectDraw と GDI
ms.assetid: 22106821-dac1-4c99-bf2c-c051b5a8893a
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、DirectDraw
- DirectDraw WDK Windows 2000 の表示、GDI
- GDI DirectDraw サポート WDK Windows 2000 の表示
- ディスプレイ ドライバー WDK Windows 2000 では、グラフィック
- グラフィックス WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92ba5c5892518408d40fde42e834f6d939e60fb1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384851"
---
# <a name="directdraw-and-gdi"></a>DirectDraw と GDI


## <span id="ddk_directdraw_and_gdi_gg"></span><span id="DDK_DIRECTDRAW_AND_GDI_GG"></span>


GDI は、ディスプレイ ドライバーが初期化されるときに、DirectDraw を自動的に有効にします。 DirectDraw とドライバーのグラフィックス DDI 部分の間の操作性が向上を提供するには、も DirectDraw DDI をサポートするドライバーを実装または次の関数を呼び出します。

<span id="DrvDeriveSurface"></span><span id="drvderivesurface"></span><span id="DRVDERIVESURFACE"></span>[**DrvDeriveSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvderivesurface)  
DirectDraw ドライバーの画面の周りの GDI ドライバー サーフェスをラップするドライバー実装関数を許可するハードウェアの任意の GDI DirectDraw ビデオ メモリまたは AGP 表面に描画 accelerated (を使用してソフトウェアで描画されているのではなく、 *DIB*エンジン)。 通常、ドライバーが既にデバイスがオフスクリーン ビットマップをサポートする場合この関数はのみコードのいくつかの追加行を必要とする必要があります。

[**DrvDeriveSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvderivesurface)ことも、GDI を使用しも排除カーソルちらつき DirectDraw または Direct3D アプリケーションとソフトウェアのカーソルを使用する場合、DirectDraw アプリケーションのパフォーマンスが向上します。

<span id="HeapVidMemAllocAligned_and_VidMemFree"></span><span id="heapvidmemallocaligned_and_vidmemfree"></span><span id="HEAPVIDMEMALLOCALIGNED_AND_VIDMEMFREE"></span>[**HeapVidMemAllocAligned** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)と[ **VidMemFree**](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-vidmemfree)  

DirectDraw を使用するドライバーと呼ばれる関数*ヒープ マネージャー*すべて[*オフスクリーン メモリ*](video-present-network-terminology.md#off_screen_memory)管理します。 [**DrvCreateDeviceBitmap** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap)呼び出す必要があります[ **HeapVidMemAllocAligned** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned) GDI ビットマップ; の容量を割り当てる DirectDraw を要求するには[ **DrvDeleteDeviceBitmap** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdeletedevicebitmap)呼び出す必要があります[ **VidMemFree** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-vidmemfree)この割り当てを解放します。

DirectDraw では、画面外のメモリ割り当て用のドライバーのグラフィックス DDI 部分に優先されます。 ドライバーは、DirectDraw をフックする必要があります[ *DdFreeDriverMemory* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_freedrivermemory)コールバックより高い優先度の DirectDraw surface のためオフスクリーン メモリから GDI サーフェスを削除するドライバーは、割り当て。

両方[ **HeapVidMemAllocAligned** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)と[ **VidMemFree** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-vidmemfree)で宣言された*dmemmgr.h*をWindows Driver Kit (WDK) に用意されています。 ドライバーは、定義する必要があります\_ \_NTDDKCOMP\_ \_このヘッダー ファイルをインクルードする前にします。

 

 





