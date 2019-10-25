---
title: ターゲットパラメータートークン
description: ターゲットパラメータートークン
ms.assetid: 1a9842c5-0ea9-47ee-a341-77e705ab5e25
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: abd2b827c3c0c5433a40809c1d6d62b5d891a432
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839016"
---
# <a name="destination-parameter-token"></a>ターゲットパラメータートークン


## <span id="ddk_destination_parameter_token_gg"></span><span id="DDK_DESTINATION_PARAMETER_TOKEN_GG"></span>


Destination パラメータートークンは、変換先レジスタのプロパティを記述し、次のビットで構成されます。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>列

<span id="_10_00_"></span> **\[10:00\]** ビット 0 ~ 10 はレジスタ番号 (レジスタファイル内のオフセット) を示します。

<span id="_12_11_"></span> **\[12:11\]** ビット11と12は、4番目と5番目の \[3, 4\][レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を示すために使用します。

<span id="_13_"></span> **\[13\]** 頂点シェーダー (VS) バージョン 3\_0 以降では、ビット13は、相対アドレス指定モードが使用されているかどうかを示します。 1に設定すると、[相対アドレス指定](shader-relative-addressing.md)が適用されます。

3\_0 より前のすべてのピクセルシェーダー (PS) バージョンと頂点シェーダーバージョンでは、ビット13が予約され、0x0 に設定されます。

<span id="_15_14_"></span> **\[15:14\]** 確保. この値は0x0 に設定されます。

<span id="_19_16_"></span> **\[19:16\]** 書き込みマスク。 このマスクのビットには、次のコンポーネントがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Bit</th>
<th align="left">コンポーネント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>コンポーネント 0 (X;Red</p></td>
</tr>
<tr class="even">
<td align="left"><p>17</p></td>
<td align="left"><p>コンポーネント 1 (Y)配慮</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>コンポーネント 2 (Z;書体</p></td>
</tr>
<tr class="even">
<td align="left"><p>19</p></td>
<td align="left"><p>コンポーネント 3 (W;英数</p></td>
</tr>
</tbody>
</table>

 

<span id="_23_20_"></span> **\[23:20\]** ビット 20 ~ 23 は、結果の修飾子を示します。 複数の結果修飾子を使用できます。 次の結果の修飾子の型は、この4ビット値で連結できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">結果の修飾子の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>飽和 (頂点シェーダー)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>部分的な精度 (ピクセルシェーダー)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>重心 (ピクセルシェーダー)</p></td>
</tr>
</tbody>
</table>

 

<span id="_27_24_"></span> **\[27:24\]** 2\_0 より前の PS バージョンでは、ビット 24 ~ 27 は、結果のシフトスケール (符号付きシフト) を指定します。
PS バージョン 2\_0 以降および VS では、これらのビットは予約され、0x0 に設定されます。
<span id="_30_28_"></span> **\[30:28\]** ビット 28 ~ 30 は、[レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を示すために0、1、2\] \[最初の3ビットです。

<span id="_31_"></span> **\[31\]** ビット31は0x1 です。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

ビット28、29、30、11、および12は、レジスタの種類を示す5ビットの値です。 レジスタ型の詳細については、「[シェーダーレジスタ型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)」を参照してください。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>必要性


Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

 

 





