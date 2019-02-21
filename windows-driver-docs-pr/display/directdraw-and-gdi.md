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
ms.openlocfilehash: c358d551fc7f383bb7e0d3676a1ff956c913364f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538384"
---
# <a name="directdraw-and-gdi"></a>DirectDraw と GDI


## <span id="ddk_directdraw_and_gdi_gg"></span><span id="DDK_DIRECTDRAW_AND_GDI_GG"></span>


GDI は、ディスプレイ ドライバーが初期化されるときに、DirectDraw を自動的に有効にします。 DirectDraw とドライバーのグラフィックス DDI 部分の間の操作性が向上を提供するには、も DirectDraw DDI をサポートするドライバーを実装または次の関数を呼び出します。

<span id="DrvDeriveSurface"></span><span id="drvderivesurface"></span><span id="DRVDERIVESURFACE"></span>[**DrvDeriveSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556188)  
DirectDraw ドライバーの画面の周りの GDI ドライバー サーフェスをラップするドライバー実装関数を許可するハードウェアの任意の GDI DirectDraw ビデオ メモリまたは AGP 表面に描画 accelerated (を使用してソフトウェアで描画されているのではなく、 *DIB*エンジン)。 通常、ドライバーが既にデバイスがオフスクリーン ビットマップをサポートする場合この関数はのみコードのいくつかの追加行を必要とする必要があります。

[**DrvDeriveSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556188)ことも、GDI を使用しも排除カーソルちらつき DirectDraw または Direct3D アプリケーションとソフトウェアのカーソルを使用する場合、DirectDraw アプリケーションのパフォーマンスが向上します。

<span id="HeapVidMemAllocAligned_and_VidMemFree"></span><span id="heapvidmemallocaligned_and_vidmemfree"></span><span id="HEAPVIDMEMALLOCALIGNED_AND_VIDMEMFREE"></span>[**HeapVidMemAllocAligned** ](https://msdn.microsoft.com/library/windows/hardware/ff567267)と[ **VidMemFree**](https://msdn.microsoft.com/library/windows/hardware/ff570554)  

DirectDraw を使用するドライバーと呼ばれる関数*ヒープ マネージャー*すべて[*オフスクリーン メモリ*](video-present-network-terminology.md#off_screen_memory)管理します。 [**DrvCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556185)呼び出す必要があります[ **HeapVidMemAllocAligned** ](https://msdn.microsoft.com/library/windows/hardware/ff567267) GDI ビットマップ; の容量を割り当てる DirectDraw を要求するには[ **DrvDeleteDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556187)呼び出す必要があります[ **VidMemFree** ](https://msdn.microsoft.com/library/windows/hardware/ff570554)この割り当てを解放します。

DirectDraw では、画面外のメモリ割り当て用のドライバーのグラフィックス DDI 部分に優先されます。 ドライバーは、DirectDraw をフックする必要があります[ *DdFreeDriverMemory* ](https://msdn.microsoft.com/library/windows/hardware/ff549360)コールバックより高い優先度の DirectDraw surface のためオフスクリーン メモリから GDI サーフェスを削除するドライバーは、割り当て。

両方[ **HeapVidMemAllocAligned** ](https://msdn.microsoft.com/library/windows/hardware/ff567267)と[ **VidMemFree** ](https://msdn.microsoft.com/library/windows/hardware/ff570554)で宣言された*dmemmgr.h*をWindows Driver Kit (WDK) に用意されています。 ドライバーは、定義する必要があります\_ \_NTDDKCOMP\_ \_このヘッダー ファイルをインクルードする前にします。

 

 





