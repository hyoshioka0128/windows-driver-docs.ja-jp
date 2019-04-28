---
title: コマンドおよび DMA バッファーの概要
description: コマンドおよび DMA バッファーの概要
ms.assetid: e9fa38a2-3243-4578-83c3-4559ec3480a7
keywords:
- コマンド バッファー コマンド バッファーについての WDK の表示
- DMA バッファーについて、DMA バッファー WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b6eece19903448d2f59e43222c5fe3ee77359cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362146"
---
# <a name="introduction-to-command-and-dma-buffers"></a>コマンドおよび DMA バッファーの概要


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


密接にコマンドおよび DMA バッファーでは互いに似ています。 ただし、コマンド バッファーは、ユーザー モードのディスプレイ ドライバーによって使用され、DMA バッファーは、ディスプレイのミニポート ドライバーによって使用されます。

コマンド バッファーには、次の特徴があります。

-   GPU で直接アクセスします。

-   ハードウェア ベンダーは、書式を制御します。

-   ユーザー モードのディスプレイ ドライバー レンダリング アプリケーションのプライベート アドレス空間で正規のページング可能なメモリからを割り当てられます。

DMA バッファーには、次の特徴があります。

-   コマンド バッファーの検証済みのコンテンツに基づいています。

-   カーネルのページング可能なメモリからディスプレイ ミニポート ドライバーによって割り当てられます。

-   GPU は、DMA バッファーから読み取ることができます、前に、ディスプレイのミニポート ドライバーはページ DMA バッファーをロックする必要があり、aperture を通じて DMA バッファーをマップします。

 

 





