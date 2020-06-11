---
title: システム DMA の使用
description: システム DMA の使用
ms.assetid: 8d478365-a6c8-4488-9f75-53a822d1daa2
keywords:
- AdapterControl ルーチン、システム DMA
- システム DMA WDK カーネル
- アダプタオブジェクト WDK カーネル、システム DMA
- DMA 転送 WDK カーネル、システム DMA
- 下位デバイス WDK DMA
- システム dma WDK カーネル、システム DMA について
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4aad36f6266e25db69b5cac5e849293c3d1e94a
ms.sourcegitcommit: bd120d96651f9e338956388c618acec7d215b0d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681672"
---
# <a name="using-system-dma"></a>システム DMA の使用





下位 DMA デバイスのドライバーは、次の種類のシステム指定の DMA サポートのいずれかを使用します。

-   パケットベースの DMA。ドライバーがシステム DMA コントローラーの自動初期化モードを使用する必要がない場合。 「[パケットベースのシステム DMA の使用」を](using-packet-based-system-dma.md)参照してください。

-   ドライバーが自動初期化モードを使用する場合は、共通バッファー DMA。 「[コモンバッファーシステム DMA の使用」を](using-common-buffer-system-dma.md)参照してください。

さらに、パケットベースの DMA を使用するドライバーでは、デバイスが組み込みのスキャッター/ギャザーサポートを備えているかどうかに関係なく、スキャッター/ギャザー DMA を効率化するためのサポートルーチンを使用できます。 詳細については、「[スキャッター/GATHER DMA の使用](using-scatter-gather-dma.md)」を参照してください。

 

 




