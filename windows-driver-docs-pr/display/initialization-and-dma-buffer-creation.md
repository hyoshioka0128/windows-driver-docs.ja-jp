---
title: 初期化と DMA バッファーの作成
description: 初期化と DMA バッファーの作成
ms.assetid: d84aed8a-9e22-4172-89c2-807b4e06108f
keywords:
- DMA バッファー WDK 表示は、GDI ハードウェア アクセラレータを作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6783098afb47a38f8ee517a47c27cc4347a7844
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385198"
---
# <a name="initialization-and-dma-buffer-creation"></a>初期化と DMA バッファーの作成


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


GPU が GDI ハードウェア アクセラレータの表示のミニポート ドライバーの実装をサポートしていることを示すために、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)関数を入力する必要があります、 **DxgkDdiRenderKm**のメンバー、 [**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data)ドライバー実装へのポインターを使用した構造[ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数。

DirectX グラフィックスのカーネル サブシステムの呼び出し、 *DxgkDdiRenderKm*によって、カーネル モード正規ディスプレイ ドライバー (CDD) オペレーティング システムによって提供されるを渡されたコマンド バッファーから DMA バッファーを生成する関数。

表示が DirectX グラフィックスのカーネル サブシステムのドライバーを移植するときに (*Dxgkrnl.sys*) 呼び出し、 [ **DxgkDdiCreateContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)関数の場合、設定、 [**pCreateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_createcontext)-&gt;[**フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_createcontextflags) - &gt; **GdiContext** GDI ハードウェア高速化に使用されるコンテキストを示すことです。

同様に、ポートのディスプレイ ドライバーを呼び出すと、 [ **DxgkDdiCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)関数の場合、設定、 [ **pCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_createdevice) - &gt; [**フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_createdeviceflags)-&gt;**GdiDevice** GDI ハードウェアを使用するデバイスを示すメンバー高速化します。

 

 





