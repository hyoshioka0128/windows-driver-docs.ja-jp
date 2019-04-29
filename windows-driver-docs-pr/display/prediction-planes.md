---
title: 予測平面
description: 予測平面
ms.assetid: 967d52d1-c4e1-4a81-a1ad-40a09040c3a8
keywords:
- ビデオの WDK DirectX va なので、マクロ ブロック予測のデコード
- ビデオのデコード WDK DirectX va なので、マクロ ブロックの予測
- 予測平面を WDK DirectX VA
- WDK の DirectX va なので、予測をマクロ ブロック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 728888ef51078b37d0919e734de807dd11c5a6fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383990"
---
# <a name="prediction-planes"></a>予測平面


## <span id="ddk_prediction_planes_gg"></span><span id="DDK_PREDICTION_PLANES_GG"></span>


次の図では、最終的な予測を形成する前に存在する概念のマクロ ブロック予測平面は示しています。

![フィールドのマクロ ブロック予測平面の例を示す図](images/m2planes.png)

Mpeg-2 が 2 つの平面。 前方と後方の (双方向予測)、または同じパリティと反対パリティ (デュアル素数)。 前方参照平面から最も近いブロックから成る以前はまたは P 画像。 旧バージョンとの参照の平面は、I または P 画像最も近い将来からのブロックで構成されます。

Mpeg-1 や mpeg-2 の場合、予測の平面は、2 つの予測の平面の対応するブロックのピクセル値の間の平均を計算し、それぞれ、最も近い整数に丸め処理して結合されます。 詳細は、高度な予測スキーム、モーションのブロックが (OBMC) の予測を補正 H. 263 の重複など、3 つの平面があります。

 

 





