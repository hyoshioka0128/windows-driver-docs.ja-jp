---
title: マクロ ブロック コントロール コマンドの構造体の第 2 部
description: マクロ ブロック コントロール コマンドの構造体の第 2 部
ms.assetid: 94ef61d1-cd7d-4e73-8be8-01f7d23bb91d
keywords:
- マクロ ブロック WDK DirectX va なので、汎用的なコマンド構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d47b5d40cff5527e79e1ab2812c3a10998688d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550673"
---
# <a name="second-part-of-macroblock-control-command-structure"></a>マクロ ブロック コントロール コマンドの構造体の第 2 部


## <span id="ddk_second_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_SECOND_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


ジェネリックのマクロ ブロック コントロール コマンド構造体の 2 番目の部分には、画像をデコード処理の構成に応じて、3 つのバリエーションが含まれています。

1.  場合*HostResidDiff* (11 ビット、 **wMBtype**メンバー) が 1 に等しいのマクロ ブロック コントロールのコマンドは、次の要素が**wPC\_Overflow**。 **WPC\_オーバーフロー**メンバーを使用する場合はマクロ ブロック使用オーバーフロー残存違いデータのブロックを指定します。 **wPC\_Overflow** 0 に等しい DWORD が続きます。

2.  場合*HostResidDiff* (11 ビット、 **wMBtype**メンバー) が 0 に等しいと**bChromaFormat**のメンバー [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)が 1 に等しいのマクロ ブロック コントロールのコマンドは、次の要素が**bNumCoef、** バイトの 6 要素配列。 **BNumCoef**メンバーは、マクロ ブロックの各ブロックの違いの残存データ バッファーの係数の数を示します。

3.  場合*HostResidDiff* (11 ビット、 **wMBtype**要素) が 0 に等しいと**bChromaFormat** DXVA のメンバー\_PictureParameters が 1 と等しく、マクロ ブロックの制御コマンドの次の要素が**wTotalNumCoef**します。 0 に等しい DWORD が続きます。

### <a name="span-idwpcoverflowspanspan-idwpcoverflowspanspan-idwpcoverflowspanwpcoverflow"></a><span id="wPC_Overflow"></span><span id="wpc_overflow"></span><span id="WPC_OVERFLOW"></span>wPC\_オーバーフロー

**WPC\_オーバーフロー**構造体のメンバーをマクロ ブロック使用オーバーフロー残存違いデータのブロックを指定します。

残存の違いのホスト ベースのデコードを使用する場合 (と*HostResidDiff*は 1 に等しい) で、 **bPicOverflowBlocks**のメンバー [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)を 1 に等しいと*IntraMacroblock* (8-8 オーバーフロー メソッド) を 0 に等しい**wPC\_オーバーフロー**がパターンを含むコードと同じ方法で指定された、オーバーフロー要素の**wPatternCode**します。 コード化されたオーバーフロー要素のデータ (マイナス 11 のビットがそれらのブロック*は*を 1 に等しい) が同じインデックス作成の順序でバッファーをコーディング残余で見つかった (増加*は*)。

### <a name="span-idbnumcoefspanspan-idbnumcoefspanspan-idbnumcoefspanbnumcoef"></a><span id="bNumCoef"></span><span id="bnumcoef"></span><span id="BNUMCOEF"></span>bNumCoef

**BNumCoef**構造体のメンバーが 6 つの要素の配列。 *は*番目の要素の**bNumCoef**配列には、ブロックごとに残存違いデータ バッファー内の係数の数が含まれています*は*、マクロ ブロックのどこ。*は*は指定の mpeg-2 ビデオ図 6 ~ 10、6 ~ 11、および 6 ~ 12 (Cb、Cr の後に続く Y のラスター スキャン order) としてマクロ ブロック内のブロックのインデックスです。 **bNumCoef**される場合にのみ*HostResidDiff*ゼロ、 **bChromaFormat**のメンバー [ **DXVA\_PictureParameters**](https://msdn.microsoft.com/library/windows/hardware/ff564012)は 1 (4:2:0)。 4 で使用する場合: 2:2 または 4:4:4 つの形式、サイズが増加マクロ ブロックの一般的なコントロールのコマンドの過去のブロックごとに係数の数を決定するため、重要なメモリの配置境界、EOB 変換係数構造内でのみです非-4:2:0 場合。 目的は、 **bNumCoef**をブロックごとに存在する係数の数で表した、残存違いデータ バッファーに存在するデータの量を示すことです。 ときに、 **bConfig4GroupedCoefs**のメンバー [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)は 1 です**bNumCoef**いずれかを含めることができます。ブロックの係数の実際の数が送信または 4 の倍数である値が最大に丸められます。 これらの係数のデータは、同じ順序で残存違いバッファーに検出されます。

### <a name="span-idwtotalnumcoefspanspan-idwtotalnumcoefspanspan-idwtotalnumcoefspanwtotalnumcoef"></a><span id="wTotalNumCoef"></span><span id="wtotalnumcoef"></span><span id="WTOTALNUMCOEF"></span>wTotalNumCoef

**WTotalNumCoef**構造体のメンバーは、全体のマクロ ブロックの違いの残存データ バッファーの係数の合計数を示します。 このメンバーが使用される場合にのみ*HostResidDiff*ゼロ、 **bChromaFormat**のメンバー [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)は 1 (4:2:0) と等しくありません。

 

 





