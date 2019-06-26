---
title: カーネル モード コマンド バッファーのサポート
description: カーネル モード コマンド バッファーのサポート
ms.assetid: c61a39b3-6fd6-461f-a68f-450ccd705f6f
keywords:
- コマンド バッファー WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7f37252c5cfc51bd6d728f1858bc6f2a988f1a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375786"
---
# <a name="supporting-kernel-mode-command-buffers"></a>カーネル モード コマンド バッファーのサポート


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


ディスプレイのミニポート ドライバーをコマンド バッファーへの呼び出しに応答を送信する必要があります、 [ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)で説明されているとおりに機能[コマンド バッファーを送信する](submitting-a-command-buffer.md)します。

ドライバーを使用して、 **MultipassOffset**のメンバー、 [ **DXGKARG\_レンダリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)コマンドを入力バッファーの処理の進行状況を追跡するために構造体。 たとえば、ディスプレイのミニポート ドライバーは、コマンドの処理を追跡するために、最後の処理コマンドと下位 16 ビットのオフセットとして上位 16 ビットを使用できます。

 

 





