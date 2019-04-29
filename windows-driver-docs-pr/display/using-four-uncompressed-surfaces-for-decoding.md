---
title: デコードに 4 つの非圧縮サーフェスを使用する
description: デコードに 4 つの非圧縮サーフェスを使用する
ms.assetid: ceeea614-6793-4a75-8334-7dd062ac0b46
keywords:
- ビデオのデコード WDK DirectX va なので、シーケンスの要件
- ビデオの WDK DirectX va なので、シーケンスの要件をデコード
- WDK の DirectX va なので、シーケンスの要件をデコードする画像
- WDK DirectX VA の要件をシーケンス処理します。
- 連続して要件 WDK DirectX VA
- 複数の圧縮されていないサーフェスの WDK DirectX VA のデコード
- WDK DirectX VA をデコードの圧縮されていないサーフェスの例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c02155fd59e9ef392f04a00564abd84bb8400708
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389033"
---
# <a name="using-four-uncompressed-surfaces-for-decoding"></a>デコードに 4 つの非圧縮サーフェスを使用する


## <span id="ddk_using_four_uncompressed_surfaces_for_decoding_gg"></span><span id="DDK_USING_FOUR_UNCOMPRESSED_SURFACES_FOR_DECODING_GG"></span>


次の表では、ビデオ デコーダーが各画像をデコードする 1 つのフレーム時間を必要と仮定の状況を示します。 これは、0 B の画像から画像は、最初から B 画像数が絶えず増加から成るビット ストリームをデコードします。 B の画像のビット ストリームでは、P 画像のペアの間に発生します。 この表で、文字 (は、B、または P) は、各画像の種類を表示する、添字は、フレームの表示インデックス (各画像のテンポラルの表示順) を示しています。 および、上付き文字は、写真を含むバッファーの数を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デコードされた画像</th>
<th align="left">画像を表示</th>
<th align="left">フレーム Decoded (先頭の間隔など)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>I⁰₀</p></td>
<td align="left"></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>P¹₁</p></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P²₃</p></td>
<td align="left"><p>I⁰₀</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₂</p></td>
<td align="left"><p>P¹₁</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P⁰₆</p></td>
<td align="left"><p>B³₂</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p>B¹₄</p></td>
<td align="left"><p>P²₃</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B³₅</p></td>
<td align="left"><p>B¹₄</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>P²₁₀</p></td>
<td align="left"><p>B³₅</p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B¹₇</p></td>
<td align="left"><p>P⁰₆</p></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₈</p></td>
<td align="left"><p>B¹₇</p></td>
<td align="left"><p>9</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B¹₉</p></td>
<td align="left"><p>B³₈</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>P⁰₁₅</p></td>
<td align="left"><p>B¹₉</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B³₁₁</p></td>
<td align="left"><p>P²₁₀</p></td>
<td align="left"><p>12</p></td>
</tr>
<tr class="even">
<td align="left"><p>B¹₁₂</p></td>
<td align="left"><p>B³₁₁</p></td>
<td align="left"><p>13</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B³₁₃</p></td>
<td align="left"><p>B¹₁₂</p></td>
<td align="left"><p>14</p></td>
</tr>
<tr class="even">
<td align="left"><p>B¹₁₄</p></td>
<td align="left"><p>B³₁₃</p></td>
<td align="left"><p>15</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P²₂₁</p></td>
<td align="left"><p>B¹₁₄</p></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₁₆</p></td>
<td align="left"><p>P²₂₁</p></td>
<td align="left"><p>17</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B¹₁₇</p></td>
<td align="left"><p>B³₁₆</p></td>
<td align="left"><p>18</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₁₈</p></td>
<td align="left"><p>B¹₁₇</p></td>
<td align="left"><p>19</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B¹₁₉</p></td>
<td align="left"><p>B³₁₈</p></td>
<td align="left"><p>20</p></td>
</tr>
<tr class="even">
<td align="left"><p>B³₂₀</p></td>
<td align="left"><p>B¹₁₉</p></td>
<td align="left"><p>21</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P⁰₂₈</p></td>
<td align="left"><p>B³₂₀</p></td>
<td align="left"><p>22</p></td>
</tr>
</tbody>
</table>

 

上記の表に各 B の画像では、これをデコードする前に、ビット ストリームの順序で 2 つ前の画像のデコードが必要です。 結果として、デコーダーでは、2 番目の画像が (つまり、まで中にデコードの 3 番目のタイム スライス) デコードされた後、まで、適切なタイミングで画像を表示するを始めることはできません。 どこかにこのタイム スライスの中に、適切なタイミングで画像の表示を開始できます。

画像の表示の開始は、ディスプレイに表示される画像と完全に一致しない可能性があります。 代わりに、表示は、適切な時間が新しい画像に切り替えるが到着するまで表示するために送信された 1 つ前の画像の表示を続行できます。 最適なパフォーマンス、サーフェス 0 (最初の画像を保持) する上書きしてはならない場合でも、画像は、後で、次の 3 つのフレーム時間が到着する B の図で使用が参照するには、その B 画像が必要としないのです。 代わりに、その B 画像を保持するために 4 番目の画面 (画面 3) を使用する必要があります。 これにより、画像は、最初の表示期間が B の画像をデコードする前に完了したかどうかを確認する必要があります。

2 つのルールに従って[要件をシーケンス](sequence-requirements.md)デコーダーが間に、3 番目の期間 (までどれもが表示されたため、異なるサーフェスは、最初の 3 つのデコードされた画像のそれぞれに配置することを必要期間 2)。 次に、4 番目のデコード済み画像は表示されている最初の画像の表示されないことがあります経由で (ピリオド 3) の 4 番目の期間中にいくつかの時間までために、4 番目の画面で配置する必要があります。

B の 2 つ以上の画像を連続してないデコード処理で重大な障害が発生します。 これは、10 番目のデコード済み画像 (B¹₉) を検出したときに、前の表で発生します。 連続する一連の 3 つ目以降の B 画像が発生した場合に、B の 1 つの画像の表示と、使用して、次のデコードされた B 画像を保持するために、画面間のタイム ラグの許容範囲は削除されました。 ホスト デコーダーは、[次へ] の B pictur の前の期間を確認して (必要な場合に発生する待機中)、表示から削除されたことから、同じ画面をすぐに使用する必要があります。 (B¹₇) に表示されていた B 画像の表示状態を確認する必要があります。デコード (画面 1 B¹₉ の使用) を使用する電子メール。 デコーダーはまたは P の参照を保持するために使用されている (この場合、サーフェス 0 および 2 P⁰₆ と P²₁₀ 使用) にあるピクチャし、t の同じ期間中に表示される画面に新しい B 画像をデコードできないサーフェスのいずれかに新しい B 画像をデコードすることはできません。(この例では、画面 3 B³₈ の使用) での ime。 そのため、直前の期間 (この場合、画面 1) 内で表示された画面を使用して、必要があります。

 

 





