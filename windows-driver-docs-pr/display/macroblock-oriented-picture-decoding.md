---
title: 画像のマクロ ブロック指向のデコード
description: 画像のマクロ ブロック指向のデコード
ms.assetid: 7a416992-04d3-4307-83b3-9fb94c17d60e
keywords:
- WDK DirectX VA マクロ ブロック
- 圧縮された画像をデコード WDK DirectX va なので、画像のマクロ ブロック指向のデコード
- デコード WDK DirectX va なので、圧縮の画像します。
- マクロ ブロック WDK DirectX va なので、画像のマクロ ブロック指向デコードについての詳細
- ビデオのデコード WDK DirectX va なので、画像の圧縮
- 画像を圧縮されたビデオの WDK DirectX VA をデコードするには、
- ビデオのデコード WDK DirectX マクロ ブロック指向 va なので、図のデコード
- ビデオの WDK DirectX va なので、デコード マクロ ブロック指向の画像のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c01270f84d0068459cfa792f20aa33ab3623c04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560984"
---
# <a name="macroblock-oriented-picture-decoding"></a>画像のマクロ ブロック指向のデコード


## <span id="ddk_macroblock_oriented_picture_decoding_gg"></span><span id="DDK_MACROBLOCK_ORIENTED_PICTURE_DECODING_GG"></span>


マクロ ブロックは、ビデオのデコード処理の基本的な単位です。 マクロ ブロックは、四角形の配列 (Y) の輝度サンプルと、彩度 (Cb および Cr) サンプルの対応する 2 つの配列で構成されます。 確立されたビデオ コーディング標準ではのマクロ ブロックは、輝度サンプルの次元内の 16 x 16 ブロックです。 ビデオが 4 でコード化された場合: 2:0 形式、2 つ、彩度の配列各は高さの半分と、マクロ ブロックの輝度および配列の半分の幅があります。 ビデオが 4 でコード化された場合: 同じの高さと幅は、マクロ ブロックの輝度配列の半分にある各 2:2 形式、2 つのクロミナンス配列。 ビデオが 4 ではコード化された場合: 4:4 形式、2 つクロミナンスの配列ごと、マクロ ブロックの輝度配列と同じサイズである場合します。

マクロ ブロックは動き補正を使用して、1 つまたは複数の動きベクトルで予測可能性があります。 または、このような予測せず内としてコーディングする可能性があります。 かどうか、マクロ ブロックを予測するかどうかを決定した後、残りの信号洗練存在する場合が追加されます残存違いデータ ブロックの形式で。 確立されたビデオ コーディング標準では、これらの違いの残存データ ブロックは、16 x 16 の輝度マクロ ブロックをカバーする 4 つの違いの残存データ ブロックが必要なようにに 8 x 8 をされます。

 

 





