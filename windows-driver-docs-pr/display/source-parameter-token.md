---
title: ソース パラメーター トークン
description: ソース パラメーター トークン
ms.assetid: 280b9fb2-9b5c-4830-9ba5-cfb6201960e0
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5b68529bb18f761446865e58d85644f22b7d6b28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382329"
---
# <a name="source-parameter-token"></a>ソース パラメーター トークン


## <span id="ddk_source_parameter_token_gg"></span><span id="DDK_SOURCE_PARAMETER_TOKEN_GG"></span>


ソース パラメーターのトークンは、ソースの登録のプロパティについて説明しは次のビットで構成されます。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_10_00_"></span>**\[10時 00分\]** 0 ~ 10 のビットがレジスタ番号 (登録ファイル内のオフセット) を示します。

<span id="_12_11_"></span>**\[12時 11分\]** ビット 11 と 12 は、4 番目と 5 番目のビット\[3, 4\]を示すため、[の種類を登録](https://msdn.microsoft.com/library/windows/hardware/ff569707)します。

<span id="_13_"></span>**\[13\]** ピクセル シェーダー (PS) バージョンが 3 よりも前の\_0、13 ビットは予約されている、0x0 に設定します。

ピクセル シェーダー (PS) version 3 の\_0 以降相対アドレス指定モードを使用するかどうかを示します頂点シェーダー (VS) のすべてのバージョン、ビット 13 とします。 場合 1 に設定されて[相対アドレス指定](shader-relative-addressing.md)適用されます。

<span id="_15_14_"></span>**\[15時 14分\]** PS と VS のすべてのバージョン用に予約されています。 この値は、「0x0」に設定されます。

<span id="_23_16_"></span>**\[23時 16分\]** ビット 16 ~ 23 がチャネルを示す*スィズル*します。 4 つのすべての算術演算が実行されます (X、Y、Z, W) 並列チャネル。 スィズル ソースを指定する操作のチャネルに参加させます。 スィズルの詳細については、DirectX SDK の最新のドキュメントを参照してください。 このフィールドのビットは、以下のチャネルのスィズルを指定します。

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
<td align="left"><p>チャネル X スィズル</p></td>
</tr>
<tr class="even">
<td align="left"><p>19:18</p></td>
<td align="left"><p>チャネル Y スィズル</p></td>
</tr>
<tr class="odd">
<td align="left"><p>21:20</p></td>
<td align="left"><p>チャネル Z スィズル</p></td>
</tr>
<tr class="even">
<td align="left"><p>23:22</p></td>
<td align="left"><p>チャネル W スィズル</p></td>
</tr>
</tbody>
</table>

 

前のビットのセットは、次の値は、操作のチャネルで使用する変換元コンポーネントを指定します。

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
<td align="left"><p>X のコンポーネントが使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>Y のコンポーネントが使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>Z コンポーネントが使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>コンポーネントの W が使用されます。</p></td>
</tr>
</tbody>
</table>

 

たとえば、19:18 ビット 0x2、Z からのコンポーネントに設定されますが、チャネル Y 操作のソースとして使用する場合です。

<span id="_27_24_"></span>**\[27:24\]** ビット 24 27 ~ ソース修飾子を指定します。 この 4 ビット値では、次のソースの修飾子の種類を示します。

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
<td align="left"><p>負数化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>バイアス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>バイアスし、否定</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>サインイン (bx2)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>サインイン (bx2) および否定</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>補数</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>x2 (PS 1_4)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>x2 (PS 1 _ 4) を負数化と</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>dz (Z コンポーネント - PS 1 _ 4 による除算を)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xa</p></td>
<td align="left"><p>dw (W コンポーネント âˆ を通じて除算 ' PS 1 _ 4)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xb</p></td>
<td align="left"><p>コンピューティングの絶対値をので</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xc</p></td>
<td align="left"><p>-abs(x) が絶対値を計算し、否定</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xd</p></td>
<td align="left"><p>じゃない。 Bool predication のレジスタにのみ適用されます。 そのため、論理 NOT になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xe-0 xf です.</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<span id="_30_28_"></span>**\[30:28\]**  30 からビット 28 は最初の 3 つのビット\[0,1,2\]を示すため、[の種類を登録](https://msdn.microsoft.com/library/windows/hardware/ff569707)します。

<span id="_31_"></span>**\[31\]** ビット 31 は 0x1 です。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

ビット 28、29、30、11、および 12 フォーム register 型を示す 5 ビット値です。 登録の種類については、次を参照してください。[シェーダー登録型](https://msdn.microsoft.com/library/windows/hardware/ff569707)します。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





