---
title: メモリの構成
description: メモリの構成
ms.assetid: e3341854-13ce-4028-ad75-49e8189ac0f7
keywords:
- stride WDK DirectDraw
- ピッチを WDK DirectDraw
- WDK DirectDraw のオフセット
- ヒープ メモリ WDK DirectDraw を描画するには、
- DirectDraw メモリ ヒープ、WDK の Windows 2000 の表示
- WDK DirectDraw、ヒープ メモリ
- ヒープ メモリ WDK の DirectDraw を表示します。
- ヒープ WDK DirectDraw
- ヒープのメモリを割り当てる
- グラフィックスアクセラレータ
- サーフェスの WDK DirectDraw、メモリ ヒープの割り当て
- 描画メモリ WDK DirectDraw、構成オプション
- DirectDraw メモリ WDK Windows 2000 の表示、構成オプション
- メモリ WDK DirectDraw、構成オプション
- メモリ WDK DirectDraw、構成オプションを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d4392c1003927e679d97225da16c1c92a8d250
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558016"
---
# <a name="memory-configurations"></a>メモリの構成


## <span id="ddk_memory_configurations_gg"></span><span id="DDK_MEMORY_CONFIGURATIONS_GG"></span>


次のセクションでには、3 つのメモリ構成の種類が含まれて:[線形](linear-memory-allocation.md)、[四角形](rectangular-memory-allocation.md)、および[混合](mixed-memory-allocation.md)メモリの割り当てを表示します。 各セクションには、サンプル コード、カードの物理的な特性に合わせて変更可能なおよび割り当てる HAL を追加することが含まれています。 ヒープにメモリを表示します。

アラインメント要件」の説明に従って、[メモリ ヒープ割り当て](memory-heap-allocation.md)トピックでは、メモリの構成の 3 種類のいずれかに適用できます。 一般に、線形のメモリは行が順番に格納されているために四角形のメモリよりもアプリケーションでより効率的に使用します。 任意の場所は、この線形範囲に沿ってまたは前方に移動することによって簡単にアクセスできます。

 

 





