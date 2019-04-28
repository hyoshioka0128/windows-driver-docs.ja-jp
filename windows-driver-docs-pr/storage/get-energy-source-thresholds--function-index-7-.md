---
title: 電力源しきい値の取得 (関数インデックス 7)
description: この関数は、エネルギー ソース (ES) でに問題がある場合はヒットまたは群を抜いて、する警告およびエラーのしきい値を返します。
ms.assetid: 12B7D7CF-DB65-42A5-9831-F0D85BED2574
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2dad016b5e1db55de9e96a17dbcc697ab70e1b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380120"
---
# <a name="get-energy-source-thresholds-function-index-7"></a>電力源しきい値の取得 (関数インデックス 7)


この関数は、エネルギー ソース (ES) でに問題がある場合はヒットまたは群を抜いて、する警告およびエラーのしきい値を返します。 この関数は、ES が管理されているホストし、プラットフォームがしきい値をサポートしていない場合、エラー状態を返す可能性があります。

&gt; \[!注\]    &gt;、星が付いたマークされているすべてのレジスタ (\*) バイト アドレス指定可能なエネルギー バックアップ インターフェイス仕様で定義されているレジスタします。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>入力


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

なし。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>出力


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">バイトの長さ</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ステータス</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>について。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES の有効期間のパーセンテージの警告しきい値</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>ES の有効期間の警告しきい値の割合の値。</p>
<p><em>バイト 0 – <em>ES_LIFETIME_WARNING_THRESHOLD</em> (0, 0x99)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES の有効期間の割合によるエラーのしきい値</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>ES の有効期間のエラーしきい値の割合の値。</p>
<p></em>バイト 0 – <em>ES_LIFETIME_ERROR_THRESHOLD</em> (0, 0x91)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES の温度の警告しきい値</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>ES の温度の警告しきい値の割合の値。</p>
<p><em>バイト 0 – <em>ES_TEMP_WARNING_THRESHOLD</em> (0, 0x9A)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 温度エラーのしきい値</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>ES の温度のエラーしきい値の割合の値。</p>
<p></em>バイト 0 – <em>ES_TEMP_ERROR_THRESHOLD</em> (0, 0x92)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[エネルギーのソースの有効期間の警告しきい値 (関数インデックス 8) の設定します。](set-energy-source-lifetime-warning-threshold--function-index-8-.md)

[エネルギー ソース温度の警告しきい値 (関数インデックス 9) の設定します。](set-energy-source-temperature-warning-threshold--function-index-9-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






