---
title: ビット ブロックの転送
description: ビット ブロックの転送
ms.assetid: d9cbe939-957d-48e0-8427-d2c1ca0a9dd6
keywords:
- blt WDK DirectDraw
- blt の描画中の WDK DirectDraw
- 中について、DirectDraw 中 WDK Windows 2000 の表示します。
- 中 WDK の DirectDraw 中について
- サーフェス WDK DirectDraw、中
- 描画 blt WDK DirectDraw
- DirectDraw 中 WDK Windows 2000 の表示
- WDK DirectDraw 中
- blt 中は、WDK DirectDraw
- DdBlt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5975ff3329eeb296548c9a463e96128b7f66cf7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384619"
---
# <a name="blitting"></a>ビット ブロックの転送


## <span id="ddk_blitting_gg"></span><span id="DDK_BLITTING_GG"></span>


Blt が 1 つの画面内で発生しているソースと変換先の領域が重なっている場合は、適切な方向がコピーされる前に、ソースの一部が上書きされないように決定する必要があります。 これは、画面の反対側の角にある 2 つの潜在的な方法で開始にポイントを実現できます。 Blt エンジンが必要なすべてが、各イメージのサイズと場所です。

高速化する実際の blt も行う必要があります。 IF ステートメントを回避するためにコードのセクションを複製することをドライバーなどの速度を上げることがあります。 おそらく、この手法の最適な実装はマクロにコードを追加して、関数の呼び出しを行うのではなく、さまざまな場所で使用します。 詳細については、次を参照してください。 [ *DdBlt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)します。

 

 





