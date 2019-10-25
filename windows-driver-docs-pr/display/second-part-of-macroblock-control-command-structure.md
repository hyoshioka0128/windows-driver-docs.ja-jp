---
title: マクロブロック制御コマンド構造の 2 番目の部分
description: マクロブロック制御コマンド構造の 2 番目の部分
ms.assetid: 94ef61d1-cd7d-4e73-8be8-01f7d23bb91d
keywords:
- マクロは WDK DirectX VA、汎用コマンド構造をブロックします
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1bbf2baba7c230556dbd7927ff40460af4f439e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829510"
---
# <a name="second-part-of-macroblock-control-command-structure"></a>マクロブロック制御コマンド構造の 2 番目の部分


## <span id="ddk_second_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_SECOND_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


汎用マクロブロックコントロールの2番目の部分には、画像デコードプロセスの構成に応じて、3つのバリエーションが含まれています。

1.  *Hostresiddiff* ( **wmbtype**メンバーのビット 11) が1に等しい場合、マクロブロックコントロールコマンドの次の要素は**wpc\_Overflow**になります。 **Wpc\_overflow**メンバーが使用されている場合は、マクロブロックでオーバーフロー残差データを使用するかどうかを指定します。 **Wpc\_Overflow**の後に、0に等しい DWORD が続きます。

2.  *Hostresiddiff* ( **wmbtype**メンバーのビット 11) がゼロで、 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)の**bChromaFormat**メンバーが1に等しい場合、マクロブロックコントロールコマンドの次の要素は**bnumcoef,** aバイトの6要素配列。 **Bnumcoef**メンバーは、マクロブロックの各ブロックの残存差データバッファー内の係数の数を示します。

3.  *Hostresiddiff* ( **wmbtype**要素のビット 11) が0と等しく、DXVA\_ピクチャパラメーターの**bChromaFormat**メンバーが1ではない場合、マクロブロックコントロールコマンドの次の要素は**wtotalnumcoef**になります。 この後に、0に等しい DWORD が続きます。

### <a name="span-idwpc_overflowspanspan-idwpc_overflowspanspan-idwpc_overflowspanwpc_overflow"></a><span id="wPC_Overflow"></span><span id="wpc_overflow"></span><span id="WPC_OVERFLOW"></span>wPC\_オーバーフロー

**Wpc\_オーバーフロー**構造体のメンバーは、マクロブロックでオーバーフロー残差データを使用するブロックを指定します。

ホストベースの残余差のデコードを使用する場合 ( *Hostresiddiff*が 1)、 [ **\_DXVA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)の**bPicOverflowBlocks**メンバーが1に等しく、 *IntraMacroblock*が0に等しい (8-8 overflow)メソッド)、 **Wpc\_overflow**には、 **wpc コード**と同じ方法で指定されたオーバーフローブロックのパターンコードが含まれています。 コード化されたオーバーフローブロック (ビット11から*i*が1に等しいブロック) のデータは、同じインデックス作成順序 (増加する*i*) の残りのコードバッファーにあります。

### <a name="span-idbnumcoefspanspan-idbnumcoefspanspan-idbnumcoefspanbnumcoef"></a><span id="bNumCoef"></span><span id="bnumcoef"></span><span id="BNUMCOEF"></span>bNumCoef

**Bnumcoef**構造体のメンバーは、6つの要素の配列です。 **Bnumcoef**配列の*i*番目の要素には、マクロブロックの各ブロック*i*の残余差データバッファー内の係数の数が含まれます。ここで、 *i*は、MPEG-2 で指定されたマクロブロック内のブロックのインデックスです。ビデオでは、6-10、6-11、6-12 (Y の場合はラスタースキャンの順序、Cb の後には Cr) が使用されます。 **Bnumcoef**は、 *Hostresiddiff*が0で、 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)の**bChromaFormat**メンバーが 1 (4:2:0) の場合にのみ使用されます。 4:2:2 または4:4:4 形式で使用されている場合、一般的なマクロブロックの制御コマンドのサイズが重要なメモリアラインメントの境界を越えて増加するため、で各ブロックの係数の数を決定するために変換係数構造内の EOB のみが使用されます。4:2:0 以外のケース。 **Bnumcoef**の目的は、残存差データバッファー内の各ブロックに存在するデータの量を示します。これは、存在する係数の数として表されます。 **BConfig4GroupedCoefs**の[ **\_DXVA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)メンバーが1に設定されている場合、 **bnumcoef**には、ブロックに対して実際に送信された係数の数または4の倍数として切り上げられた値のいずれかが含まれている可能性があります。 これらの係数のデータは、残余差のバッファーに同じ順序で格納されます。

### <a name="span-idwtotalnumcoefspanspan-idwtotalnumcoefspanspan-idwtotalnumcoefspanwtotalnumcoef"></a><span id="wTotalNumCoef"></span><span id="wtotalnumcoef"></span><span id="WTOTALNUMCOEF"></span>wTotalNumCoef

**Wtotalnumcoef**構造体のメンバーは、マクロブロック全体の残存差データバッファー内の係数の合計数を示します。 このメンバーは、 *Hostresiddiff*が0で、 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)の**bChromaFormat**メンバーが 1 (4:2:0) と等しくない場合にのみ使用されます。

 

 





