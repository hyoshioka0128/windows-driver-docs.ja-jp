---
title: カーネル モード コマンド バッファーのサポート
description: カーネル モード コマンド バッファーのサポート
ms.assetid: c61a39b3-6fd6-461f-a68f-450ccd705f6f
keywords:
- コマンド バッファー WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2c29abcb6910e02ac507bf8bc07b540a3b9d330
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377652"
---
# <a name="supporting-kernel-mode-command-buffers"></a>カーネル モード コマンド バッファーのサポート


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


ディスプレイのミニポート ドライバーをコマンド バッファーへの呼び出しに応答を送信する必要があります、 [ **DxgkDdiRenderKm** ](https://msdn.microsoft.com/library/windows/hardware/ff559800)で説明されているとおりに機能[コマンド バッファーを送信する](submitting-a-command-buffer.md)します。

ドライバーを使用して、 **MultipassOffset**のメンバー、 [ **DXGKARG\_レンダリング**](https://msdn.microsoft.com/library/windows/hardware/ff557648)コマンドを入力バッファーの処理の進行状況を追跡するために構造体。 たとえば、ディスプレイのミニポート ドライバーは、コマンドの処理を追跡するために、最後の処理コマンドと下位 16 ビットのオフセットとして上位 16 ビットを使用できます。

 

 





