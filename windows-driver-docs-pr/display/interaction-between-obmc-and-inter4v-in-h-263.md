---
title: INTER4V での OBMC と間の相互作用
description: INTER4V での OBMC と間の相互作用
ms.assetid: 096c723d-ec16-49f7-acaa-62ed228338c3
keywords:
- マクロは WDK DirectX VA、汎用コマンド構造をブロックします
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4c04708b17b2f4444d9c1bab9bfb6ef649c5d82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840356"
---
# <a name="interaction-between-obmc-and-inter4v-in-h263"></a>INTER4V での OBMC と間の相互作用


## <span id="ddk_interaction_between_obmc_and_inter4v_in_h_263_gg"></span><span id="DDK_INTERACTION_BETWEEN_OBMC_AND_INTER4V_IN_H_263_GG"></span>


PB*のフレーム*での、 *INTER4V*、 *B*、 *EP*、および b の間の相互作用に関する詳細は、次のような場合に役立ちます。

-   現在の構成では、 *Motion4MV*は、 **b obmc**が1に等しく、1が1に等しく、 *motionbackward*が1に等しい場合に実行されます。

-   OBMC は、263 B または EP の画像では使用できません。

-   OBMC は、263 PB 画像の B 部分では使用できません。

-   INTER4V は、263 B または EP の画像では使用できません。

-   INTER4V が、のマクロブロックで使用されている場合、このマクロブロックは、後で B 画像の "direct" 予測の参照マクロブロックとして使用されます。これは、直接予測では使用されません。 これは、4つのモーションベクターが使用されているためです。これは、(たとえば、-263 付属 G) のように使用します。これは、OBMC を適用しません。 INTER4V では、OBMC と後方予測の両方を同時に使用することはできません。逆方向にはを使用しません。

### <a name="span-iddwmb_snlspanspan-iddwmb_snlspanspan-iddwmb_snlspandwmb_snl"></a><span id="dwMB_SNL"></span><span id="dwmb_snl"></span><span id="DWMB_SNL"></span>dwMB\_SNL

**Dwmb\_SNL**構造体のメンバーは、現在のマクロブロックの後に生成されるスキップされるマクロブロックの数を指定し、現在のマクロブロックの残存差データの場所を示します。 このメンバーには、2つの変数が含まれています。 *Mbskipsfollowing*は、最も重要な8ビットであり、最も重要でない24ビットです。 *Mbskipsfollowing*は、現在のマクロブロックの後に生成される、スキップされたマクロブロックの数を示します。 *MBdataLocation*は、残留差ブロックデータバッファーのインデックスです。 このインデックスは、現在のマクロブロックの残存差データの場所を示します。これは、32ビットの倍数として表されます。

*Mbskipsfollowing*によって示されたスキップされた各マクロブロックは、 **wmbaddress**の値をインクリメントし、同じマクロブロックコントロールコマンドを繰り返すという数学的な方法で生成する必要があります。

*Mbskipsfollowing*に0以外の値が設定されたマクロブロックコントロールコマンドは、スキップする各マクロブロックに対してモーション補正予測を実行する方法を指定します。これは、( *Mbskipsfollowing*の値を除く) 同等のものになります。最初の一連のスキップされたマクロブロックの生成の非スキップ指定。 したがって、 *Mbskipsfollowing*の値が0ではない場合、次の構造体のメンバーと変数はすべてゼロに等しくなければなりません: *Motion4MV IntraMacroblock* **wpattern コード***と* **wpカバーフロー**。

*MBdataLocation*変数は、マクロブロックコントロールのコマンドバッファーの最初のマクロブロックに対して0にする必要があります。 **Wpattern コード**がゼロの場合、 *MBdataLocation*には任意の値を含めることができます。 **Wpattern コード**がゼロの場合、デコーダーが推奨されますが、この値を0に設定する必要はありません。また、次のマクロブロックコントロールコマンドの場合と同じ値に設定する必要もありません。

スキップされたマクロブロックの生成の詳細については、「スキップされた[マクロブロックの生成](generating-skipped-macroblocks.md)」を参照してください。

### <a name="span-idwpatterncodespanspan-idwpatterncodespanspan-idwpatterncodespanwpatterncode"></a><span id="wPatternCode"></span><span id="wpatterncode"></span><span id="WPATTERNCODE"></span>Wpattern コード

**Wpattern コード**構造体のメンバーは、マクロブロックの各ブロックに残差のデータが送信されるかどうかを示します。

**Wpattern コード**のビット (11- *i*) (ビット0は最も重要ではないビット) は、残存差データがブロック*i*に送信されるかどうかを示します。ここで、 *i*は mpeg-2 ビデオに指定されているマクロブロック内のブロックのインデックスです。図6-10、6-11、6-12 (Y の場合はラスタースキャンの順序、ラスタースキャンの順序では Cb の4:2:0 ブロックが、その後には4:2:0 ブロックのブロックが続き、その後には、4:2:2 の4:2:2 ブロックが続き、その後に、Cb の4:4:4 ブロックが続き、その後には、4:4:4 のブロックがあります。 コード化されたブロックのデータ (ビット 11-*i*が1に等しいブロック) は、同じインデックス作成順序 ( *i*を増やす) の残りのコードバッファーにあります。 4:2:0 MPEG-2 データの場合、 **Wpattern コード**の値は、Cbp (コード化されたブロックパターン) のデコードされた値を6ビット位置 (4:2:2 と4:4:4 クロマ形式で使用される下位ビット位置) にシフトすることに対応します。

[**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)の**bConfigSpatialResidInterleaved**メンバーが1の場合、ホストベースの残余差は、使用されている YUV ピクセル形式と一致するクロマインターリーブ形式で送信されます。 この場合、各 Cb と空間的に対応するブロックの Cr ペアは、1つの残余差集合単位として扱われます。 これにより、 **Wpattern コード**の値または意味は変更されませんが、これらのデータブロックのいずれかに対応するビット (ビット7またはビット 6) が**wpattern コード**で設定されている場合は常に、Cb と Cr の両方のデータブロックの両方のメンバーが送信されることを意味します。 特定のデータブロックの**Wpattern コード**内のビットが0の場合、Cb と Cr ブロックのペアリングで、ブロック**の残存差データブロックを送信する必要がある場合は常に、対応する残留差データ値を0として送信する必要があります。Wpattern コード**ビットが0に等しい。

 

 





