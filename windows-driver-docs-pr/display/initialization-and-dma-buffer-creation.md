---
title: 初期化と DMA バッファーの作成
description: 初期化と DMA バッファーの作成
ms.assetid: d84aed8a-9e22-4172-89c2-807b4e06108f
keywords:
- DMA バッファー WDK 表示は、GDI ハードウェア アクセラレータを作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 501ff566b716ed266d8bc41c9ae01df0699e833e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325050"
---
# <a name="initialization-and-dma-buffer-creation"></a>初期化と DMA バッファーの作成


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


GPU が GDI ハードウェア アクセラレータの表示のミニポート ドライバーの実装をサポートしていることを示すために、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff556157)関数を入力する必要があります、 **DxgkDdiRenderKm**のメンバー、 [**ドライバー\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff556169)ドライバー実装へのポインターを使用した構造[ **DxgkDdiRenderKm** ](https://msdn.microsoft.com/library/windows/hardware/ff559800)関数。

DirectX グラフィックスのカーネル サブシステムの呼び出し、 *DxgkDdiRenderKm*によって、カーネル モード正規ディスプレイ ドライバー (CDD) オペレーティング システムによって提供されるを渡されたコマンド バッファーから DMA バッファーを生成する関数。

表示が DirectX グラフィックスのカーネル サブシステムのドライバーを移植するときに (*Dxgkrnl.sys*) 呼び出し、 [ **DxgkDdiCreateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff559612)関数の場合、設定、 [**pCreateContext**](https://msdn.microsoft.com/library/windows/hardware/ff557567)-&gt;[**フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff561037) - &gt; **GdiContext** GDI ハードウェア高速化に使用されるコンテキストを示すことです。

同様に、ポートのディスプレイ ドライバーを呼び出すと、 [ **DxgkDdiCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff559615)関数の場合、設定、 [ **pCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff557570) - &gt; [**フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff561039)-&gt;**GdiDevice** GDI ハードウェアを使用するデバイスを示すメンバー高速化します。

 

 





