---
title: ソース パラメーター トークン
description: ソース パラメーター トークン
ms.assetid: 280b9fb2-9b5c-4830-9ba5-cfb6201960e0
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e635dff01fe1e6ef554ee152ba14c314c251d382
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829448"
---
# <a name="source-parameter-token"></a>ソース パラメーター トークン


## <span id="ddk_source_parameter_token_gg"></span><span id="DDK_SOURCE_PARAMETER_TOKEN_GG"></span>


ソースパラメータートークンは、ソースレジスタのプロパティを記述し、次のビットで構成されます。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>列

<span id="_10_00_"></span> **\[10:00\]** ビット 0 ~ 10 はレジスタ番号 (レジスタファイル内のオフセット) を示します。

<span id="_12_11_"></span> **\[12:11\]** ビット11と12は、4番目と5番目の \[3, 4\][レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を示すために使用します。

<span id="_13_"></span> **\[13\]** 3\_0 より前のピクセルシェーダー (PS) バージョンでは、ビット13が予約され、0x0 に設定されます。

ピクセルシェーダー (PS) バージョン 3\_0 以降で、すべてのバージョンの頂点シェーダー (VS) では、ビット13は、相対アドレス指定モードが使用されているかどうかを示します。 1に設定すると、[相対アドレス指定](shader-relative-addressing.md)が適用されます。

<span id="_15_14_"></span> **\[15:14\]** すべてのバージョンの PS および VS 用に予約されています。 この値は0x0 に設定されます。

<span id="_23_16_"></span> **\[23:16\]** ビット 16 ~ 23 はチャネル*swizzle*を示します。 すべての算術演算は、4つ (X、Y、Z、W) の並列チャネルで実行されます。 Swizzle は、操作のチャネルに参加するソースコンポーネントを指定します。 Swizzle の詳細については、最新の DirectX SDK のドキュメントを参照してください。 このフィールドのビットは、次のチャネルに対して swizzle を指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット</th>
<th align="left">Channel</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>17:16</p></td>
<td align="left"><p>Channel X swizzle</p></td>
</tr>
<tr class="even">
<td align="left"><p>19:18</p></td>
<td align="left"><p>Channel Y swizzle</p></td>
</tr>
<tr class="odd">
<td align="left"><p>21:20</p></td>
<td align="left"><p>Channel Z swizzle</p></td>
</tr>
<tr class="even">
<td align="left"><p>23:22</p></td>
<td align="left"><p>チャネル W swizzle</p></td>
</tr>
</tbody>
</table>

 

前のビットのセットに含まれる次の値は、操作のチャネルで使用される変換元コンポーネントを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">Component</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>コンポーネント X が使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>コンポーネント Y が使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>コンポーネント Z が使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>コンポーネント W が使用されます。</p></td>
</tr>
</tbody>
</table>

 

たとえば、19:18 ビットが0x2 に設定されている場合、コンポーネント Z はチャネル Y 操作のソースとして使用されます。

<span id="_27_24_"></span> **\[27:24\]** ビット 24 ~ 27 は、ソース修飾子を示します。 この4ビット値は、次のソース修飾子の種類を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">ソース修飾子の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>バイアス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>バイアスと反転</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>Sign (bx2)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>Sign (bx2) と否定</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>網</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>x2 (PS 1_4)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>x2 と否定 (PS 1_4)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>dz (-Z コンポーネント-PS 1_4)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xa</p></td>
<td align="left"><p>dw (W コンポーネントによる除算-ˆ ' PS 1_4)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xb</p></td>
<td align="left"><p>abs (x) compute absolute 値</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xc</p></td>
<td align="left"><p>-abs (x) 絶対値を計算し、符号を反転します</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xd</p></td>
<td align="left"><p>じゃない。 Predication register (BOOL) にのみ適用されます。 したがって、これは論理的なものではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xe-0xf です</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<span id="_30_28_"></span> **\[30:28\]** ビット 28 ~ 30 は、[レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を示すために0、1、2\] \[最初の3ビットです。

<span id="_31_"></span> **\[31\]** ビット31は0x1 です。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

ビット28、29、30、11、および12は、レジスタの種類を示す5ビットの値です。 レジスタ型の詳細については、「[シェーダーレジスタ型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)」を参照してください。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

 

 





