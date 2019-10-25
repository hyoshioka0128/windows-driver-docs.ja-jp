---
title: オフホスト VLD ビットストリームのデコード操作
description: オフホスト VLD ビットストリームのデコード操作
ms.assetid: fd339d5f-2d63-4b2f-a5dc-7ab7a6799a6d
keywords:
- オフ-ホスト VLD ビットストリーム処理 WDK DirectX VA
- ビットストリーム VLD 処理 WDK DirectX VA
- 逆量子化行列バッファー WDK DirectX VA
- スライスコントロールバッファーの WDK DirectX VA
- ビットストリームバッファー WDK DirectX VA
- 圧縮された画像で WDK DirectX VA をデコードし、マクロブロック指向の画像デコード
- 画像デコード WDK DirectX VA、圧縮
- ビデオデコード WDK DirectX VA、圧縮された画像
- ビデオをデコードする WDK DirectX VA、圧縮された画像
- ビデオデコード WDK DirectX VA、非ホスト VLD ビットストリーム処理
- ビデオをデコードしています。 WDK DirectX VA、非ホスト VLD ビットストリーム処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac233f1dd5561d0a686f517dd3a8dfdb664897ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840503"
---
# <a name="off-host-vld-bitstream-decoding-operation"></a>オフホスト VLD ビットストリームのデコード操作


## <span id="ddk_off_host_vld_bitstream_decoding_operation_gg"></span><span id="DDK_OFF_HOST_VLD_BITSTREAM_DECODING_OPERATION_GG"></span>


生のビットストリームデータの可変長デコードがアクセラレータで実行される場合、画像をデコードするためにホストによって送信されるデータは、次のバッファーの種類に分割されます。

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
<td align="left"><p>逆量子化行列</p></td>
<td align="left"><p>ビットストリームデータの逆量子化を実行する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>スライスコントロール</p></td>
<td align="left"><p>対応するビットストリームデータバッファー内の開始コードとデータの場所に関する情報を提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ビットストリーム</p></td>
<td align="left"><p>特定のビデオコーディング仕様に従ってエンコードされた未加工のデータストリームを格納します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinverse-quantization_matrix_buffersspanspan-idinverse-quantization_matrix_buffersspanspan-idinverse-quantization_matrix_buffersspaninverse-quantization-matrix-buffers"></a><span id="Inverse-Quantization_Matrix_Buffers"></span><span id="inverse-quantization_matrix_buffers"></span><span id="INVERSE-QUANTIZATION_MATRIX_BUFFERS"></span>逆量子化行列バッファー

逆量子化行列バッファーは、オフホストのビットストリームデコードの逆量子化マトリックスを初期化するために送信されます。 逆量子行列バッファーは、新しい逆量子化行列バッファーが指定されるまで、ビットストリーム内の現在および後続のすべてのビデオをデコードする方法に関する情報を提供します。 (したがって、逆量子化行列は永続的です)。ホストから一度に1つ以上の逆量子化行列バッファーをホストからアクセラレータに送信することはできません。 [**DXVA\_QmatrixData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_qmatrixdata)構造体は、圧縮されたビデオ画像デコード用の量子化マトリックスデータを読み込みます。

### <a name="span-idslice-control_buffersspanspan-idslice-control_buffersspanspan-idslice-control_buffersspanslice-control-buffers"></a><span id="Slice-Control_Buffers"></span><span id="slice-control_buffers"></span><span id="SLICE-CONTROL_BUFFERS"></span>スライスコントロールバッファー

スライスコントロールバッファーは、非ホスト VLD ビットストリーム処理の操作をガイドします。 ホストソフトウェアデコーダーは、ビットストリーム内のスライスレベルの再同期ポイントの場所を決定します。 スライスは、ビットストリームデータの再同期ポイントを含む multiマクロブロックレイヤーとして定義されます。 この場合、"-261" ブロック (GOB) はスライスと見なされます。 263 bitstreams では、GOB 開始コードから始まり、追加の GOB 開始コードを含まない1つ以上の263のシーケンスがスライスと見なされます。 スライスコントロールバッファーには、対応するビットストリームデータバッファーの内容に適用される[**DXVA\_スライス Einfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_sliceinfo)スライス制御構造体の配列が含まれています。

### <a name="span-idbitstream_buffersspanspan-idbitstream_buffersspanspan-idbitstream_buffersspanbitstream-buffers"></a><span id="Bitstream_Buffers"></span><span id="bitstream_buffers"></span><span id="BITSTREAM_BUFFERS"></span>ビットストリームバッファー

ビットストリームバッファーが使用されている場合、バッファーには単にビデオビットストリームからの生バイトが含まれます。 この種類のバッファーは、可変長デコードを使用した低レベルのビットストリーム解析を含む、ホストを使用しないデコードに使用されます。

ビットストリームバッファーの内容には特定の制限が適用されます。これは、アクセラレータによって受信されるデータが認識可能で効率的な形式であることを目的としています。

1.  MPEG-1 と MPEG 2 を除き、各画像の最初のビットストリームバッファーは、ビットストリーム内の現在の画像の最初のスライスの前にあるすべてのデータ (シーケンスヘッダーなど) の最後に続くすべてのデータから開始する必要があります。画像ヘッダー)。

2.  MPEG-1 と MPEG-2 の場合、各画像の最初のビットストリームバッファーは、画像の最初のスライスのスライス開始コード (たとえば、シーケンスヘッダーや画像ヘッダーがない) で開始する必要があります。これは、関連するすべてのデータが他のパラメーターで提供されるためです。

3.  ビットストリームデータのスライスの開始が特定のビットストリームバッファー内にある場合、スライスの開始を含むバッファーが割り当てられたサイズに達していない限り、そのスライスの末尾は同じバッファー内に配置する必要があります。

デコーダーは、1つのスライスのデータが複数のバッファーに配置されないように、ビットストリームバッファーの入力を管理する必要があります。

 

 





