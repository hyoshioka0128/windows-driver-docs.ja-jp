---
title: ホストベース IDCT
description: ホストベース IDCT
ms.assetid: 9f44e734-8cbc-4317-bd72-66d4ac7cd4de
keywords:
- マクロ ブロック WDK DirectX va なので、IDCT
- 低レベルの IDCT WDK DirectX VA
- ホスト ベース IDCT WDK DirectX VA
- 逆コサイン不連続変換 WDK DirectX VA
- IDCT WDK DirectX VA
- 16 ビットのホスト ベース IDCT WDK DirectX VA
- 8-8 オーバーフロー ホストベース IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f8a865f8ad315b3b41efb27b2611389e0b8a83b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571733"
---
# <a name="host-based-idct"></a>ホストベース IDCT


## <span id="_host_based_idct"></span><span id="_HOST_BASED_IDCT"></span>


IDCT は空間ドメインでの DirectX VA API を介して渡された結果をホストで実行できます。 アクセラレータにホストから、結果を送信するための 2 つのサポートされている方法はあります。16 ビット版と 8-8 オーバーフローします。 **BConfigSpatialResid8**のメンバー、 [ **DXVA\_ConfigPictureDecode**](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体を使用する方法を示します。

### <a name="span-id16-bithost-basedidctprocessingspanspan-id16-bithost-basedidctprocessingspanspan-id16-bithost-basedidctprocessingspan16-bit-host-based-idct-processing"></a><span id="16-bit_Host-Based_IDCT_Processing"></span><span id="16-bit_host-based_idct_processing"></span><span id="16-BIT_HOST-BASED_IDCT_PROCESSING"></span>16 ビットのホスト ベース IDCT 処理

16 ビットのホスト ベース残存違いデコードで使用マクロ ブロックの制御構造は[ **DXVA\_MBctrl\_は\_HostResidDiff\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563983)と[ **DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)します。

ドメイン空間残存の違いを 16 ビット メソッドを使用してデータを送信する場合は、16 ビットのデータのブロックが順番に送信されます。 ドメイン空間データの各ブロックは、64 の 16 ビット整数で構成されます。

場合*BPP*から派生した、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造体を 8 よりも大きい 16 ビット メソッドのみを使用できます。 場合、 **bPicIntra**メンバーは、DXVA の\_PictureParameters 構造体が 1 と*BPP*が 8 の場合、8-8 オーバーフロー メソッドを使用します。 場合*IntraMacroblock*がゼロ、16 ビットの残存差サンプルは動き補償の予測値に追加する符号付きの数量として送信されます。 場合*IntraMacroblock*は 1 です。 16 ビットのサンプルを次のように送信されます。

-   場合、 **bConfigIntraResidUnsigned**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体が 1 のサンプルは、符号なし数量として送信されます場合、0 の定数参照の値を基準にします。 たとえば、中程度の灰色を Y = 2 として示されます<sup>(BPP 1)</sup>、Cb = 2<sup>(BPP 1)</sup>、Cr = 2<sup>(BPP 1)</sup>します。

-   場合、 **bConfigIntraResidUnsigned**メンバーは、DXVA の\_ConfigPictureDecode 構造が 0 で、サンプルが 2 の符号付きの数量の定数参照の値を基準として送信される<sup>(BPP 1)</sup>. たとえば、中程度の灰色を Y = 0、Cb として示されます 0、Cr の = = 0。

データのブロックがスキャンで指定された順序で順番に送信される、 **wPatternCode**の値の最上位ビットから最下位ビットの 1 ビットのマクロ ブロックのコントロール構造体のメンバー。

残存の相違点の値のクリッピングと想定できなし、ホストで実行された場合を除き、 **bConfigSpatialHost8or9Clipping**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体は 1 です。 だけですが、 *BPP*+1 のビットの範囲が、ドメイン空間データをいくつかの出力を十分に表すために必要な[IDCT](low-level-idct-processing-elements.md)実装でない限り、この範囲外の数値が生成されます切り取られます。

**注**  アクセラレータは、値の少なくとも 15 ビット範囲を使用する必要があります。 ビデオ コーディング標準は、通常、予測値 (サンプルあたり 8 ビットのビデオでは、9 ビット クリッピング) に追加する前に、difference 値のクリップを指定していますが、この段階でクリッピングは、その結果に影響があるないために、実際に必要なデコード済み出力の画像。 しない限り、このクリッピングが発生すること、想定されませんアクセラレータ ハードウェアで示されているために必要な**bConfigSpatialHost8or9Clipping**メンバーは、DXVA の\_ConfigPictureDecode 構造体が 1 に設定されています。

 

### <a name="span-id8-8overflowhost-basedidctprocessingspanspan-id8-8overflowhost-basedidctprocessingspanspan-id8-8overflowhost-basedidctprocessingspan8-8-overflow-host-based-idct-processing"></a><span id="8-8_Overflow_Host-Based_IDCT_Processing_"></span><span id="8-8_overflow_host-based_idct_processing_"></span><span id="8-8_OVERFLOW_HOST-BASED_IDCT_PROCESSING_"></span>8-8 オーバーフロー IDCT のホスト ベースの処理

8-8 オーバーフロー残存違いのホスト ベースのデコードで使用するマクロ ブロックの制御構造は[ **DXVA\_MBctrl\_は\_HostResidDiff\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563983)と[ **DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)します。

場合、 *BPP*から派生した変数、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造は、8、8-8 のオーバーフロー ドメイン空間残存違いメソッドがありますこのオプションを使用するとします。 場合、使用する必要が、 **bPicIntra**この構造体のメンバーが 1 と*BPP*は 8 です。 この場合、各ドメイン空間値は、8 ビットのみを使用して表されます。 8-8 のオーバーフロー メソッドを使用してデータを送信するときに、8 ビットのデータのブロックが順番に送信されます。 8 ビット ドメイン空間残存違いデータは、従来のラスター内のデータの値を含む 64 バイトの各ブロックは、(2 番目の行、およびなどの要素の後に、順序の最初の行の要素) の順序をスキャンします。

場合*IntraMacroblock*マクロ ブロック コントロールのコマンドは、0、8 ビット ドメイン空間残存差サンプルは、加算または減算する符号付きの相違点 (から決定される、 **bConfigResid8Subtraction**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造とサンプルは、最初に、かどうかがブロックまたはオーバーフロー ブロックを渡す)動き補正の予測値を基準にします。

場合*IntraMacroblock* (ビット 0 で、 **wMBtype**マクロ ブロック構造体のメンバー) は 0、ブロック内のいくつかのピクセルが大きすぎて表す 8 ビットのみを使用して表される差秒8 ビット ドメイン空間残存差サンプルのオーバーフロー ブロックが送信されます。

場合*IntraMacroblock* (ビット 0 で、 **wMBtype**マクロ ブロック構造体のメンバー) は 1、8 ビット ドメイン空間残存差サンプルを次のように設定されます。

-   場合、 **bConfigIntraResidUnsigned**メンバーは、DXVA の\_ConfigPictureDecode 構造体が 1 の場合のサンプルは、8 ビットが 0 の定数参照の値を基準とした符号なし数量として送信されます。 たとえば、中程度の灰色を Y = 2 として示されます<sup>(BPP 1)</sup>、Cb = 2<sup>(BPP 1)</sup>、Cr = 2<sup>(BPP 1)</sup>します。

-   場合、 **bConfigIntraResidUnsigned**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造が 0 で、8 ビットのサンプルは、符号付きの数量として送信されます2 の定数参照の値を基準<sup>(BPP 1)</sup>します。 たとえば、中程度の灰色を Y = 0、Cb として示されます 0、Cr の = = 0。

IntraMacroblock が 1 の場合は、8 ビット オーバーフロー ブロックは送信されません。

データのブロックがスキャンで指定された順序で順番に送信される、 **wPatternCode**から最下位に最上位の 1 の値を持つビットのマクロ ブロック コントロール コマンドのメンバー。 すべての必要な 8 ビット オーバーフロー ブロックが、送信で指定された、 **wPC\_オーバーフロー**マクロ ブロック コントロール コマンドのメンバー。 このようなオーバーフロー ブロックが追加された場合ではなく減算されて、 **bConfigResid8Subtraction**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造1。 各 nonintra マクロ ブロックの 8 ビットの相違点の最初のパスが追加されます。 場合、 **bPicOverflowBlocks**のメンバー、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造は、0 または*IntraMacroblock*マクロ ブロック コントロール コマンドのメンバーは 1、2 番目のパスはありません。 場合**bPicOverflowBlocks**は 1 です*IntraMacroblock*ゼロと**bConfigResid8Subtraction**各 nonintra マクロ ブロックは 1、2 番目のパスの 8 ビットの相違点は、。減算します。 場合**bPicOverflowBlocks**は 1 です*IntraMacroblock*ゼロと**bConfigResid8Subtraction**がゼロの場合は、各 nonintra マクロ ブロックは、8 ビットの相違点の 2 つ目のパス。追加されます。

すべてのサンプルは、および対応する 8 ビット オーバーフロー ブロックで、両方の元の 8 ビット ブロックで、0 以外の場合は、次の規則が適用されます。

-   場合**bConfigResid8Subtraction** 0 の場合は、サンプルの符号は両方のブロックで同じである必要があります。

-   場合**bConfigResid8Subtraction** 1 に設定されて、元の 8 ビット ブロックでサンプルの符号は、対応するオーバーフロー ブロックでサンプルの 1 回の値を負の符号と同じである必要があります。

これらの規則は、2 つの各経過した後、結果の 8 ビットのクリッピングと予測の画像に追加するサンプルを使用できます。

**注**  オーバーフローのブロックと相違点を使用して 8 ビット**bConfigResid8Subtraction**は残余を表すことはできません (オーバーフロー ブロックごとに 2 つの 8 ビットの相違点の追加の結果) を 0 に等しい場合 +255 の値の差。 *IntraMacroblock*は 0 です。 (この方法を表すことができますの差の最大値は、127 + 127 = 254)。これにより、8-8 オーバーフロー IDCT ホスト ベースのメソッドは、ビデオ コーディング標準に厳密に準拠していないときに**bConfigResid8Subtraction**は 0 です。 ただしは一部の既存の実装で使用、画像を表すために必要なデータの量の観点から 16 ビットのサンプルの使用よりも効率的ですし、意味のあるビデオ品質の低下に一般的にならないため、この形式がサポートされています。

 

 

 





