---
title: デコードに 5 つ以上の非圧縮サーフェスを使用する
description: デコードに 5 つ以上の非圧縮サーフェスを使用する
ms.assetid: 7cd09d7a-6700-4079-97bd-0b0151705b82
keywords:
- ビデオのデコード WDK DirectX va なので、シーケンスの要件
- ビデオの WDK DirectX va なので、シーケンスの要件をデコード
- WDK の DirectX va なので、シーケンスの要件をデコードする画像
- WDK DirectX VA の要件をシーケンス処理します。
- 連続して要件 WDK DirectX VA
- 複数の圧縮されていないサーフェスの WDK DirectX VA のデコード
- WDK DirectX VA をデコードの圧縮されていないサーフェスの例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad73a257be86b7802d5d8bc2ffa3ffe513ba695e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389077"
---
# <a name="using-five-or-more-uncompressed-surfaces-for-decoding"></a>デコードに 5 つ以上の非圧縮サーフェスを使用する


## <span id="ddk_using_five_or_more_uncompressed_surfaces_for_decoding_gg"></span><span id="DDK_USING_FIVE_OR_MORE_UNCOMPRESSED_SURFACES_FOR_DECODING_GG"></span>


圧縮されていないサーフェスの 4 つを超える使用できますデコード、バッファーの表示の開始位置と、そのバッファーに新しい書き込み操作間のタイム ラグを許可する 2 つ以上を 1 つの表示期間の最小値を増やす。 この手法は、ジッター デコードの処理のタイミングの許容値の詳細を提供できます。 この手法には、デコードされた出力処理が有効にできますも 3 つのフィールドを実行する画像インター レースを解除、表示プロセスの一環として操作します。 だけでなくは表示されるのに、前の画像が使用可能なもに、現在の画像を使用できるコンテキストを提供し、実際の表示プロセスで 1 つのフィールドの遅延を許可するためです。

最低でも 4 つのバッファーは DirectX VA B の画像を効果的に使用するために必要ですがの遅延を最小限に抑える必要としないシナリオで特に、5 つ以上のバッファーの使用が推奨します。 DirectX VA デコーダーは、B、および P 構造化ビデオ デコーディングはそのため、最小値を設定するが必要で、要求の最大圧縮されていないサーフェスの割り当て数は少なくとも 4 つと 5 つ、それぞれ、圧縮されていないサーフェスを割り当てるときにします。 1 つまたは複数の圧縮されていない余分なサーフェスを使用して信頼性の高い、終了処理のない操作を実現できます。

 

 





