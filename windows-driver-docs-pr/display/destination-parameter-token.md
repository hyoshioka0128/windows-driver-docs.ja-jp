---
title: 宛先パラメーター トークン
description: 宛先パラメーター トークン
ms.assetid: 1a9842c5-0ea9-47ee-a341-77e705ab5e25
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: dc28ec9d6278727879b16ea290a366eb08d4d34e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348882"
---
# <a name="destination-parameter-token"></a>宛先パラメーター トークン


## <span id="ddk_destination_parameter_token_gg"></span><span id="DDK_DESTINATION_PARAMETER_TOKEN_GG"></span>


変換先のパラメーター トークンは、宛先レジスタのプロパティについて説明しは次のビットで構成されます。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_10_00_"></span>**\[10時 00分\]** 0 ~ 10 のビットがレジスタ番号 (登録ファイル内のオフセット) を示します。

<span id="_12_11_"></span>**\[12時 11分\]** ビット 11 と 12 は、4 番目と 5 番目のビット\[3, 4\]を示すため、[の種類を登録](https://msdn.microsoft.com/library/windows/hardware/ff569707)します。

<span id="_13_"></span>**\[13\]** 頂点シェーダー (VS) のバージョン 3 の\_13 のビットが 0 以降では、相対アドレス指定モードが使用されるかどうかを示します。 場合 1 に設定されて[相対アドレス指定](shader-relative-addressing.md)適用されます。

すべてのピクセル シェーダー (PS) バージョンと頂点シェーダーのバージョン 3 よりも前の\_0、13 ビットは予約されている、0x0 に設定します。

<span id="_15_14_"></span>**\[15時 14分\]** 予約します。 この値は、「0x0」に設定されます。

<span id="_19_16_"></span>**\[19時 16分\]** 書き込みマスク。 このマスクのビットは、次のコンポーネントをです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット</th>
<th align="left">コンポーネント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>コンポーネント (X; 0赤)</p></td>
</tr>
<tr class="even">
<td align="left"><p>17</p></td>
<td align="left"><p>コンポーネント 1 (Y です。緑)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>コンポーネント 2 (Z。青)</p></td>
</tr>
<tr class="even">
<td align="left"><p>19</p></td>
<td align="left"><p>コンポーネント 3 (W です。アルファ)</p></td>
</tr>
</tbody>
</table>

 

<span id="_23_20_"></span>**\[23時 20分\]** 23 ビット 20 は、結果の修飾子を示します。 複数の結果の修飾子を使用できます。 結果のうち修飾子はこの 4 ビット値でまとめて or 演算を指定できます。

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
<td align="left"><p>(頂点シェーダー) が飽和状態します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>部分的な有効桁数 (ピクセル シェーダー)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>重心 (ピクセル シェーダー)</p></td>
</tr>
</tbody>
</table>

 

<span id="_27_24_"></span>**\[27:24\]**  PS のバージョン 2 よりも前\_0、24 ~ 27 ビット結果 shift スケール (符号付きのシフト) を指定します。
PS バージョン 2 の\_0 以降と、これらのビットは予約済みに設定して 0x0 とします。
<span id="_30_28_"></span>**\[30:28\]**  30 からビット 28 は最初の 3 つのビット\[0,1,2\]を示すため、[の種類を登録](https://msdn.microsoft.com/library/windows/hardware/ff569707)します。

<span id="_31_"></span>**\[31\]** ビット 31 は 0x1 です。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

ビット 28、29、30、11、および 12 フォーム register 型を示す 5 ビット値です。 登録の種類については、次を参照してください。[シェーダー登録型](https://msdn.microsoft.com/library/windows/hardware/ff569707)します。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





