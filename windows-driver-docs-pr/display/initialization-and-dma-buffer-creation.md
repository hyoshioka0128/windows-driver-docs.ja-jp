---
title: 初期化と DMA バッファーの作成
description: 初期化と DMA バッファーの作成
ms.assetid: d84aed8a-9e22-4172-89c2-807b4e06108f
keywords:
- DMA バッファー WDK 表示、GDI ハードウェアアクセラレーション用に作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 237d527943639e96aba271635a7e2085b99944a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840379"
---
# <a name="initialization-and-dma-buffer-creation"></a>初期化と DMA バッファーの作成


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


GPU が GDI ハードウェアアクセラレーションをサポートしていることを示すために、ディスプレイミニポートドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)関数の実装は、[**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)の**DxgkDdiRenderKm**メンバーに入力する必要があります。ドライバーによって実装された[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数へのポインターを持つ構造体。

DirectX graphics カーネルサブシステムは、 *DxgkDdiRenderKm*関数を呼び出して、オペレーティングシステムによって提供されるカーネルモードの正規表示ドライバー (cdd) によって渡されたコマンドバッファーから DMA バッファーを生成します。

DirectX グラフィックスカーネルサブシステム (*Dxgkrnl*) のディスプレイポートドライバーが[**DxgkDdiCreateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)関数を呼び出すと、 [**pCreateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createcontext)-&gt;[**フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_createcontextflags)-&gt;gdicontext に設定されます。GDI ハードウェアの高速化に使用されるコンテキストを示すメンバー。

同様に、ディスプレイポートドライバーが[**DxgkDdiCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)関数を呼び出すと、 [**PCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createdevice)-&gt;[**フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_createdeviceflags)-&gt;**GdiDevice**メンバーによって、GDI に使用されるデバイスを示すように設定されます。ハードウェアの高速化。

 

 





