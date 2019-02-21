---
title: オフホスト VLD ビット ストリームのデコード操作
description: オフホスト VLD ビット ストリームのデコード操作
ms.assetid: fd339d5f-2d63-4b2f-a5dc-7ab7a6799a6d
keywords:
- オフホスト VLD ビット ストリームの WDK DirectX VA の処理
- ビット ストリーム VLD WDK DirectX VA の処理
- 量子化の逆行列の行列が WDK DirectX VA をバッファー処理します。
- スライス コントロール WDK DirectX VA をバッファー処理します。
- ビット ストリーム バッファーの WDK DirectX VA
- 圧縮された画像をデコード WDK DirectX va なので、画像のマクロ ブロック指向のデコード
- デコード WDK DirectX va なので、圧縮の画像します。
- ビデオのデコード WDK DirectX va なので、画像の圧縮
- 画像を圧縮されたビデオの WDK DirectX VA をデコードするには、
- ビデオのデコード WDK DirectX va なので、オフホスト VLD ビット ストリーム処理
- ビデオの WDK DirectX VA をデコードするには、オフホスト VLD ビット ストリーム処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41ff18f2480c2d3f2750973edc4c8b9ae077f567
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538661"
---
# <a name="off-host-vld-bitstream-decoding-operation"></a>オフホスト VLD ビット ストリームのデコード操作


## <span id="ddk_off_host_vld_bitstream_decoding_operation_gg"></span><span id="DDK_OFF_HOST_VLD_BITSTREAM_DECODING_OPERATION_GG"></span>


可変長の生のビット ストリーム データのデコードをアクセラレータ上で実行するとき、画像のデコードをホストによって送信されるデータは、次のバッファーの種類に分かれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">バッファーの種類</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>量子化の逆行列のマトリックス</p></td>
<td align="left"><p>ビット ストリーム データの量子化の逆関数を実行する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>スライスのコントロール</p></td>
<td align="left"><p>スタート コードと対応するビット ストリーム データ バッファー内のデータの場所に関する情報を提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ビット ストリーム</p></td>
<td align="left"><p>特定のビデオ コーディング仕様に従ってエンコードされたデータの生のストリームが含まれています。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinverse-quantizationmatrixbuffersspanspan-idinverse-quantizationmatrixbuffersspanspan-idinverse-quantizationmatrixbuffersspaninverse-quantization-matrix-buffers"></a><span id="Inverse-Quantization_Matrix_Buffers"></span><span id="inverse-quantization_matrix_buffers"></span><span id="INVERSE-QUANTIZATION_MATRIX_BUFFERS"></span>量子化の逆行列のマトリックス バッファー

オフホスト ビット ストリームのデコードのマトリックスを逆量子化を初期化するために、行列の逆行列量子化のバッファーが送信されます。 量子化の逆行列の行列のバッファーでは、新しい行列の逆行列量子化バッファーが提供されるまで、ビット ストリームで、すべての現在およびそれ以降のビデオをデコードする方法についてを説明します。 (そのため、行列の逆行列量子化は永続的な) です。1 つの逆量子化マトリックス バッファーは、一度にアクセラレータにホストから送信できます。 [ **DXVA\_QmatrixData** ](https://msdn.microsoft.com/library/windows/hardware/ff564034)構造体は、圧縮されたビデオ画像のデコードの量子化マトリックスのデータを読み込みます。

### <a name="span-idslice-controlbuffersspanspan-idslice-controlbuffersspanspan-idslice-controlbuffersspanslice-control-buffers"></a><span id="Slice-Control_Buffers"></span><span id="slice-control_buffers"></span><span id="SLICE-CONTROL_BUFFERS"></span>スライス コントロール バッファー

スライス コントロール バッファー オフホスト VLD ビット ストリーム処理の操作を説明します。 ホスト ソフトウェア デコーダーは、ビット ストリームでスライスのレベルの再同期ポイントの場所を決定します。 スライスは、ビット ストリーム データで再同期ポイントを含む multimacroblock レイヤーに定義されます。 H.261 ビット ストリームで、H.261 グループのブロック (GOB) は、スライスと見なされます。 H.263 では、ビットを 1 つまたは複数の H.263 豊富な GOB 以降のシーケンスは、コードを起動し、追加 GOB 開始のコードが含まれていないと、スライスと見なされます。 スライス コントロール バッファーの配列を格納する[ **DXVA\_SliceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff564049)スライス コントロールの構造は、対応するビット ストリーム データ バッファーの内容に適用されます。

### <a name="span-idbitstreambuffersspanspan-idbitstreambuffersspanspan-idbitstreambuffersspanbitstream-buffers"></a><span id="Bitstream_Buffers"></span><span id="bitstream_buffers"></span><span id="BITSTREAM_BUFFERS"></span>ビット ストリーム バッファー

ビット ストリーム バッファーを使用する場合、バッファーにビデオ ビット ストリームからの生のバイトが含まれます。 この種類のバッファーは、可変長のデコードの解析中、低レベル ビット ストリームを含むオフホスト デコードに使用されます。

特定の制限は、アクセラレータで受信したデータが認識できる、効率的な形で順序で、ビット ストリーム バッファーの内容に課されます。

1.  Mpeg-1 や mpeg-2 を除く最初のビット ストリームをバッファーの各画像は、ビット ストリームで、現在の画像の最初のスライスの前にある前の図のすべてのデータの最後の存在する場合、すべてのデータを開始する必要があります (シーケンス ヘッダー、または画像のヘッダーの場合)。

2.  Mpeg-1 や mpeg-2 の各図の最初のビット ストリーム バッファーは、すべての関連データが他のパラメーターで提供されるためです (たとえば、いないシーケンス ヘッダーまたは画像ヘッダー)、画像の最初のスライスのスライスの開始コードで始まらなければなりません。

3.  ビット ストリーム データのスライスの開始が特定のビット ストリーム バッファー内にある場合は、そのスライスの末尾もあります同じバッファー内にあるスライスの開始を格納しているバッファー、割り当てられたサイズに達していない場合。

デコーダーには、1 つ以上のバッファーに 1 つのスライスのデータを配置することを回避するためにビット ストリーム バッファーの入力を管理する必要があります。

 

 





