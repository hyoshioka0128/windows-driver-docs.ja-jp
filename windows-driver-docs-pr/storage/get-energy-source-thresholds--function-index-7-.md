---
title: 電力源しきい値の取得 (関数インデックス 7)
description: この関数は、警告とエラーのしきい値を返します。ヒットした場合、またはそれを超える場合は、エネルギーソースに問題があることを示します。
ms.assetid: 12B7D7CF-DB65-42A5-9831-F0D85BED2574
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 928aa85aa695619f58012ab5ac8fc25e9f2709f8
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851339"
---
# <a name="get-energy-source-thresholds-function-index-7"></a>電力源しきい値の取得 (関数インデックス 7)


この関数は、警告とエラーのしきい値を返します。ヒットした場合、またはそれを超える場合は、エネルギーソースに問題があることを示します。 ES がホストによって管理されていて、プラットフォームでしきい値がサポートされていない場合、この関数はエラー状態を返すことがあります。

> [!NOTE]
> スター () でマークされたすべてのレジスタ \* は、バイトアドレッシング可能なエネルギーバッキングインターフェイスの仕様で定義されているレジスタです。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>代入


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

[なし] :

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Output


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
<th align="left">バイト長</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状態</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>にアクセスしてください。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 有効期間の割合-警告しきい値</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>ES の有効期間の警告しきい値のパーセント値。</p>
<p><em>バイト0– <em>ES_LIFETIME_WARNING_THRESHOLD</em> (0, 0x99)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 有効期間の割合のエラーしきい値</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>ES の有効期間のエラーしきい値のパーセント値。</p>
<p></em>バイト0– <em>ES_LIFETIME_ERROR_THRESHOLD</em> (0, 0x91)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 温度警告しきい値</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>ES 温度の警告しきい値のパーセント値。</p>
<p><em>バイト0– <em>ES_TEMP_WARNING_THRESHOLD</em> (0, 0x9a)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 温度エラーのしきい値</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>ES 温度のエラーしきい値のパーセント値。</p>
<p></em>バイト0– <em>ES_TEMP_ERROR_THRESHOLD</em> (0, 0x92)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[電力源の有効期間に関する警告しきい値の設定 (関数インデックス 8)](set-energy-source-lifetime-warning-threshold--function-index-8-.md)

[電力源の温度に関する警告しきい値の設定 (関数インデックス 9)](set-energy-source-temperature-warning-threshold--function-index-9-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






