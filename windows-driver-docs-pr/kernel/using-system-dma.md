---
title: システム DMA の使用
description: システム DMA の使用
ms.assetid: 8d478365-a6c8-4488-9f75-53a822d1daa2
keywords:
- AdapterControl ルーチン、DMA システム
- システム DMA WDK カーネル
- アダプター オブジェクトの WDK カーネル、DMA システム
- DMA は、WDK カーネルでは、システム DMA を転送します。
- スレーブ デバイス WDK DMA
- システムに関するシステム DMA の DMA WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7984b4a9334648985cc8b3067545f21868b417a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379060"
---
# <a name="using-system-dma"></a>システム DMA の使用





下位の DMA デバイスのドライバーは、システム指定の DMA サポートの種類は次のいずれかを使用します。

-   パケットに基づく DMA、ドライバーはシステム DMA コント ローラーの自動初期化モードを使用しない必要がある場合。 参照してください[DMA パケットに基づくシステムを使用して](using-packet-based-system-dma.md)します。

-   一般的なバッファー DMA 場合は、ドライバーは、自動初期化モードを使用します。 参照してください[共通バッファー システム DMA を使用して](using-common-buffer-system-dma.md)します。

さらに、すべてのドライバーを使用してパケットに基づく DMA サポート ルーチンが効率化するためのものを使用できますスキャッター/ギャザー DMA に関係なくかどうか、デバイスがスキャッター/ギャザーの組み込みサポート。 参照してください[を使用してスキャッター/ギャザー DMA](using-scatter-gather-dma.md)詳細についてはします。

 

 




