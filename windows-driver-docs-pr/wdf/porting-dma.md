---
title: DMA の移植
description: DMA の移植
ms.assetid: 457B6459-EE02-4A2C-8D25-81CE1D9265DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a4a80036c48e6be4c073b5b70de2da4894ca226
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390100"
---
# <a name="porting-dma"></a>DMA の移植


\[KMDF にのみ適用されます。\]

KMDF ドライバーで DMA (Direct Memory Access) を実行すると、フレームワークは、ドライバーの代わりの詳細の多くを処理するため、WDM ドライバーよりも簡単ですが。

基本的に、フレームワーク ベースのドライバーは DMA イネーブラー オブジェクトを作成、デバイスの DMA の機能を指定し、転送を実行するためのハードウェアを操作するコールバック関数を提供します。

フレームワークは、転送に必要なマップのレジスタの数を決定、マップのレジスタを割り当て、スキャッター/ギャザー リスト (の場合、デバイスがサポート スキャッター/ギャザー DMA) をビルド、およびプロセッサのキャッシュと必要なときにバッファーをフラッシュを。

実装の詳細については、次を参照してください。 [KMDF ドライバーで DMA 操作を処理](handling-dma-operations-in-kmdf-drivers.md)します。

 

 





