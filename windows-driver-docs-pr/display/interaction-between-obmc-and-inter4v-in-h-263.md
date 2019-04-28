---
title: H.263 での OBMC と INTER4V の相互作用
description: H.263 での OBMC と INTER4V の相互作用
ms.assetid: 096c723d-ec16-49f7-acaa-62ed228338c3
keywords:
- マクロ ブロック WDK DirectX va なので、汎用的なコマンド構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40cf3a96a51a07948e032c63f4c00448f6232acc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381871"
---
# <a name="interaction-between-obmc-and-inter4v-in-h263"></a>H.263 での OBMC と INTER4V の相互作用


## <span id="ddk_interaction_between_obmc_and_inter4v_in_h_263_gg"></span><span id="DDK_INTERACTION_BETWEEN_OBMC_AND_INTER4V_IN_H_263_GG"></span>


H. 263 の間の相互作用についての詳細*OBMC*、 *INTER4V*、 *B*、 *EP*、B PB フレームにも役立ちます。

-   H.263 標準の現在の構成がケースにも実行しない**bPicOBMC**が 1、 *Motion4MV*が 1、および*MotionBackward*は 1 に等しい。

-   OBMC は H.263 B または EP 画像では使用できません。

-   OBMC は、H.263 PB 図の B 部分で使用できません。

-   INTER4V は H.263 B または EP 画像では使用できません。

-   INTER4V が H.263 P 画像のマクロ ブロックで使用され、このマクロ ブロックは、後で予測に使用の参照をマクロ ブロックとして「直接」H.263 B 画像の場合は、OBMC は直接の予測では使用されません。 これは、モーションの 4 つのベクトルは、OBMC は適用されませんを H.263 Annex G などのようにこれらを使って H.263 Annex M、に従って使用されます。 H.263 では、OBMC と同時に、旧バージョンと予測の両方は必要ありませんし、逆方向に決して INTER4V を使用します。

### <a name="span-iddwmbsnlspanspan-iddwmbsnlspanspan-iddwmbsnlspandwmbsnl"></a><span id="dwMB_SNL"></span><span id="dwmb_snl"></span><span id="DWMB_SNL"></span>dwMB\_SNL

**DwMB\_SNL**構造体のメンバーの現在のマクロ ブロックでは、次の生成をスキップしたマクロ ブロックの数を指定し、データは、現在のブロックの残存の相違の場所を示しますマクロ ブロックします。 このメンバーには、2 つの変数が含まれています。*MBskipsFollowing*最上位の 8 ビットでと*MBdataLocation*最下位 24 ビットにします。 *MBskipsFollowing*次の現在のマクロ ブロックされるようにスキップされたマクロ ブロックの数を示します。 *MBdataLocation*残存違いブロックのデータ バッファーへのインデックスします。 このインデックスでは、32 ビットの倍数として表される、現在のマクロ ブロックのブロックの違いの残存データの場所を示します。

によって示されるスキップされた各マクロ ブロック*MBskipsFollowing*の値をインクリメントする数学的に同等の方法で生成する必要があります**wMBaddress**とし、同じマクロ ブロックを繰り返しコマンドを制御します。

0 以外の値でマクロ ブロック コントロール コマンド*MBskipsFollowing*を指定します、スキップするマクロ ブロックごとの予測の動き補正が実行される方法と同じです (の値を除く*MBskipsFollowing*) の最初の生成の結果の明示的な仕様をスキップしたマクロ ブロックに対して使用する一連の。 したがって、たびに*MBskipsFollowing*が 0、次の構造体のメンバーと、変数する必要がありますすべて 0 を指定します。*Motion4MV IntraMacroblock* **wPatternCode** *と* **wPCOverflow**します。

*MBdataLocation*変数は、マクロ ブロック コントロール コマンド バッファー内の最初のマクロ ブロックに 0 である必要があります。 *MBdataLocation*場合は、任意の値を含めることができます**wPatternCode**は 0 です。 ときに**wPatternCode** 0 の場合は、デコーダーはお勧めしますが、0 または次のマクロ ブロック コントロール コマンドのように同じ値のいずれかに、この値を設定する必要がありません。

スキップされたマクロ ブロックを生成する詳細については、次を参照してください。[スキップ マクロ ブロックの生成](generating-skipped-macroblocks.md)します。

### <a name="span-idwpatterncodespanspan-idwpatterncodespanspan-idwpatterncodespanwpatterncode"></a><span id="wPatternCode"></span><span id="wpatterncode"></span><span id="WPATTERNCODE"></span>wPatternCode

**WPatternCode**構造体のメンバーでは、残存の違いのデータをマクロ ブロック内の各ブロックに送信するかどうかを示します。

ビット (11 -*は*) の**wPatternCode**残存の違いのデータをブロックに送信するかどうかを示します (ビット 0 が最下位ビット)*は*ここで、*しました* mpeg-2 ビデオの数値で指定されているマクロ ブロック内のブロックのインデックスは、6 ~ 10、6 ~ 11、および 6 ~ 12 (ラスター スキャンのため、Y が続く 4: Cb ラスター スキャンの順序での 2:0 ブロックが続く 4:4 の後に、Cr のブロックを 2:0: Cb のブロックを 2:2後に 4:4 の後に、Cr のブロックを 2:2:4: 4 ブロックの後に 4 Cb: Cr のブロックを 4:4)。 コード化されたブロックのデータ (11 - ビットがそれらのブロック*は*を 1 に等しい) がインデックス作成と同じ順序でバッファーをコーディング残余で見つかった (増加*は*)。 4:2:0 mpeg-2 データの値は、 **wPatternCode** 6 つのビット位置を左にシフト CBP (コード化されたブロックのパターン) のデコードされた値に対応 (4 用に使用されているビットの位置を下げるもの: 2:2 と 4:4:4 つの値の彩度形式)。

場合、 **bConfigSpatialResidInterleaved**のメンバー [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)は 1 ですホスト ベースの残存相違点はで送信される、。使用中の YUV ピクセル形式に一致する値の彩度インターリーブ フォームです。 この場合、各 Cb およびブロックの空間的に対応する Cr のペアは残存違いの 1 つの構造の単位として扱われます。 値またはの意味は変わりませんこの**wPatternCode**、送信ブロック Cb、Cr のデータの各ペアの両方のメンバーたびにこれらのデータ ブロックのいずれかが対応するビット (ビット 7 またはビット 6) 設定こと意味しますが、 **wPatternCode**します。 場合にビット**wPatternCode** Cb、Cr のブロックの組で残存の違いのデータ ブロックを送信が求められるたびに、0 として残存の違いの対応するデータ値を送信する必要が特定のデータ ブロックが 0 には、ブロックに関する、 **wPatternCode**ビットが 0 に等しい。

 

 





