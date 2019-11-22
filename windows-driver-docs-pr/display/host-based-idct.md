---
title: ホストベース IDCT
description: ホストベース IDCT
ms.assetid: 9f44e734-8cbc-4317-bd72-66d4ac7cd4de
keywords:
- マクロが WDK DirectX VA、IDCT をブロックする
- 低レベルの IDCT WDK DirectX VA
- ホストベースの IDCT WDK DirectX VA
- 逆余弦変換-WDK DirectX VA
- IDCT WDK DirectX VA
- 16ビットホストベースの IDCT WDK DirectX VA
- 8-8 オーバーフローホストベース IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d875951e373ed931631077bd0741e1771902751a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839651"
---
# <a name="host-based-idct"></a>ホストベース IDCT


## <span id="_host_based_idct"></span><span id="_HOST_BASED_IDCT"></span>


IDCT はホスト上で実行され、結果は空間ドメインの DirectX VA API を介して渡されます。 ホストからアクセラレータへの結果の送信には、16ビットと8-8 のオーバーフローの2つのメソッドがサポートされています。 [**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の**bConfigSpatialResid8**メンバーは、どのメソッドが使用されているかを示します。

### <a name="span-id16-bit_host-based_idct_processingspanspan-id16-bit_host-based_idct_processingspanspan-id16-bit_host-based_idct_processingspan16-bit-host-based-idct-processing"></a><span id="16-bit_Host-Based_IDCT_Processing"></span><span id="16-bit_host-based_idct_processing"></span><span id="16-BIT_HOST-BASED_IDCT_PROCESSING"></span>16ビットホストベースの IDCT 処理

16ビットホストベースの残差のデコードに使用されるマクロブロック制御構造は[**DXVA\_mbctrl\_I\_hostresiddiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1)および[**DXVA\_Mbctrl\_P\_hostresiddiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1).

16ビット方式を使用して空間ドメインの残留差データを送信する場合、16ビットデータのブロックは順番に送信されます。 空間ドメインデータの各ブロックは、64 16 ビットの整数で構成されます。

[**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体から派生した*BPP*が8より大きい場合、16ビットのメソッドのみを使用できます。 DXVA\_ピクチャパラメーター構造体の**b**のメンバーが1で、 *BPP*が8の場合、8-8 overflow メソッドが使用されます。 *IntraMacroblock*がゼロの場合、16ビットの残差のサンプルは、モーション補正予測値に追加される符号付きの数量として送信されます。 *IntraMacroblock*が1の場合、16ビットのサンプルは次のように送信されます。

-   [**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の**Bconfigに**よって署名されていないメンバーが1である場合、サンプルは定数参照値0から相対的に符号なしの数量として送信されます。 たとえば、中間レベルの灰色は、Y = 2<sup>(bpp-1)</sup>、Cb = 2<sup>(bpp-1)</sup>、Cr = 2<sup>(bpp-1)</sup>として表されます。

-   DXVA\_Configピクチャデコード構造体の**Bconfig**メンバーが0の場合、サンプルは、定数参照値 2<sup>(BPP-1)</sup>を基準として、符号付きの数量として送信されます。 たとえば、中間レベルの灰色は Y = 0、Cb = 0、Cr = 0 と表示されます。

データのブロックは、マクロブロックコントロール構造の**Wpattern コード**メンバーをスキャンすることによって指定された順序で順番に送信されます。これにより、最上位ビットから最下位ビットまでの値が1になるビットが返されます。

[**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の**bConfigSpatialHost8or9Clipping**メンバーが1の場合を除き、残存差の値のクリッピングはホストで実行されていると想定できます。 空間ドメインの相違データを適切に表現するために必要なのは、 *BPP*+ 1 ビット範囲のみですが、一部の[idct](low-level-idct-processing-elements.md)実装の出力では、クリッピングされない限り、この範囲を超えて数値が生成されます。

アクセラレータは、少なくとも15ビットの値の範囲で動作する必要がある   に**注意**してください。 通常、ビデオコーディング標準では、予測値に追加する前に差の値のクリッピングが指定されていますが (つまり、8ビットのサンプルビデオでは9ビットのクリッピング)、このクリッピングステージは、結果に影響を与えないため、実際には不要です。出力画像をデコードします。 DXVA\_Configピクチャデコード構造体の**bConfigSpatialHost8or9Clipping**メンバーによって示されているように、アクセラレータハードウェアに必要な場合を除き、このクリッピングが発生するとは見なされません。

 

### <a name="span-id8-8_overflow_host-based_idct_processing_spanspan-id8-8_overflow_host-based_idct_processing_spanspan-id8-8_overflow_host-based_idct_processing_span8-8-overflow-host-based-idct-processing"></a><span id="8-8_Overflow_Host-Based_IDCT_Processing_"></span><span id="8-8_overflow_host-based_idct_processing_"></span><span id="8-8_OVERFLOW_HOST-BASED_IDCT_PROCESSING_"></span>8-8 オーバーフローホストベースの IDCT 処理

8-8 で使用するマクロブロックコントロール構造体は、 [**DXVA\_mbctrl\_I\_hostresiddiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1)および[**DXVA\_Mbctrl\_P\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1).

[**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体から派生した*BPP*変数が8の場合は、8-8 のオーバーフロー空間ドメイン残留差法を使用できます。 この構造体の**B絵文字**のメンバーが1で、 *BPP*が8の場合は、使用する必要があります。 この場合、各空間ドメインの差の値は、8ビットのみを使用して表されます。 8-8 overflow メソッドを使用してデータを送信する場合、8ビットデータのブロックは順番に送信されます。 8ビットの空間ドメインの残留差データの各ブロックは、64バイトで構成されます。これには、従来のラスタースキャン順序 (最初の行の要素、2番目の行の要素など) のデータ値が含まれます。

マクロブロックコントロールコマンドの*IntraMacroblock*がゼロの場合、8ビットの空間ドメインの残余差のサンプルは、モーション補正予測値を基準にして、追加または削除する符号付きの相違 ( [**DXVA\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)の構造体の**bConfigResid8Subtraction**メンバーと、そのサンプルが最初のパスブロックまたはオーバーフローブロックにあるかどうか) を示します。

*IntraMacroblock* (マクロブロック構造体の**wmbtype**メンバーのビット 0) が0で、ブロック内の一部のピクセルに対して表される差が、8ビットのみを使用して表すには大きすぎる (8 ビット空間ドメインの2番目のオーバーフローブロック)残余差のサンプルが送信されます。

*IntraMacroblock* (マクロブロック構造の**wmbtype**メンバーのビット 0) が1の場合、8ビットの空間ドメインの残留差のサンプルは次のように設定されます。

-   DXVA\_Configピクチャデコード構造体の**Bconfigに**よって署名されていないメンバーが1である場合、8ビットのサンプルは、定数参照値0から相対的に符号なしの数量として送信されます。 たとえば、中間レベルの灰色は、Y = 2<sup>(bpp-1)</sup>、Cb = 2<sup>(bpp-1)</sup>、Cr = 2<sup>(bpp-1)</sup>として表されます。

-   [**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の**Bconfig の sidunsigned**メンバーがゼロの場合、8ビットのサンプルは、定数参照値 2<sup>(BPP-1)</sup>を基準とした符号付きの数量として送信されます。 たとえば、中間レベルの灰色は Y = 0、Cb = 0、Cr = 0 と表示されます。

IntraMacroblock が1の場合、8ビットのオーバーフローブロックは送信されません。

データのブロックは、マクロブロックコントロールコマンドの**Wpattern コード**メンバーをスキャンすることによって指定された順序で順番に送信されます。 その後、必要なすべての8ビットオーバーフローブロックが、 **Wpc\_overflow**メンバーによって指定されたとおりにマクロブロックコントロールコマンドによって送信されます。 このようなオーバーフローブロックは加算ではなく減算されます。これは、 [**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の**bConfigResid8Subtraction**メンバーが1である場合に加算されます。 マクロブロック以外の各ブロックについて、8ビットの相違点の最初のパスが追加されます。 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体の**bPicOverflowBlocks**メンバーがゼロの場合、またはマクロブロックコントロールコマンドの*IntraMacroblock*メンバーが1の場合、2番目のパスはありません。 **BPicOverflowBlocks**が1の場合、 *IntraMacroblock*が0で、 **bConfigResid8Subtraction**が1の場合は、非マクロブロックごとに8ビットの相違の2番目のパスが減算されます。 **BPicOverflowBlocks**が1、 *IntraMacroblock*が0、 **bConfigResid8Subtraction**がゼロの場合は、マクロブロック以外の各ブロックについて8ビットの相違点の2番目のパスが追加されます。

元の8ビットブロックと対応する8ビットオーバーフローブロックの両方で、いずれかのサンプルが0以外の場合は、次の規則が適用されます。

-   **BConfigResid8Subtraction**が0の場合、両方のブロックでサンプルの符号が同じである必要があります。

-   **BConfigResid8Subtraction**が1の場合、元の8ビットブロックのサンプルの符号は、対応するオーバーフローブロックのサンプルの値の負の1倍の符号と同じである必要があります。

これらの規則により、2つのパスのそれぞれの後に、結果の8ビットのクリッピングでサンプルを予測図に追加できます。

**BConfigResid8Subtraction**が0に等しいオーバーフローブロックと8ビットの違いを使用します (オーバーフローブロックごとに8ビットの違いが2つ追加されます)。  **ただし**、次の場合*は、+ 255 の残余差の値を表すことはできません。IntraMacroblock*は0です。 (この方法で表すことができる最大の差の値は、127 + 127 = 254 です)。これにより、 **bConfigResid8Subtraction**がゼロの場合、8-8 overflow のホストベースの idct メソッドがビデオコーディング標準に厳密に準拠していないようになります。 ただし、この形式は、既存のいくつかの実装で使用されているためサポートされています。これは、画像を表すために必要なデータ量の観点から16ビットのサンプルを使用するよりも効率的であり、通常はビデオ品質の意味のある劣化を招くことはありません。

 

 

 





