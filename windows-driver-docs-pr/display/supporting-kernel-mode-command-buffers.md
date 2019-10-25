---
title: カーネル モード コマンド バッファーのサポート
description: カーネル モード コマンド バッファーのサポート
ms.assetid: c61a39b3-6fd6-461f-a68f-450ccd705f6f
keywords:
- コマンドバッファーの WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb0bfd9ac620280c54475d1f0f4091996f3b8d78
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825611"
---
# <a name="supporting-kernel-mode-command-buffers"></a>カーネル モード コマンド バッファーのサポート


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


表示ミニポートドライバーは、「[コマンドバッファーを送信](submitting-a-command-buffer.md)する」で説明されているように、 [**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数の呼び出しに応答してコマンドバッファーを送信する必要があります。

ドライバーは、 [**Dxgkarg\_RENDER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)構造体の**multiパスワード**メンバーを使用して、入力コマンドバッファー処理の進行状況を追跡できます。 たとえば、表示ミニポートドライバーは、最後に処理されたコマンドへのオフセットとして上位16ビットを使用し、コマンドの処理を追跡するために下位16ビットを使用できます。

 

 





