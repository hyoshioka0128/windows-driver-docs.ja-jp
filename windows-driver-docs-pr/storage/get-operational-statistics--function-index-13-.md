---
title: 操作に関する統計情報の取得 (関数インデックス 13)
description: この関数は、NVDIMM によって実行される操作を追跡するカウンターを返します。
ms.assetid: D396F42E-9B11-46D7-8D9C-FE00B4998DEC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 46d7975d85c7620b758ad2e83f3dc5411b6718d7
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851449"
---
# <a name="get-operational-statistics-function-index-13"></a>操作に関する統計情報の取得 (関数インデックス 13)


この関数は、NVDIMM によって実行される操作を追跡するカウンターを返します。

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
<td align="left"><strong>最後の保存操作の期間</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>最後の保存操作の期間 (ミリ秒または秒単位)。</p>
<p><em>バイト0– <em>LAST_SAVE_DURATION0</em> (2, 0x04)</p>
<p></em>バイト1– <em>LAST_SAVE_DURATION1</em> (2、0x05)</p>
<p>バイト2–予約済み。</p>
<p>バイト3–予約済み。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最後の復元操作の期間</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>最後の復元操作の実行時間 (ミリ秒または秒単位)。</p>
<p><em>バイト0– <em>LAST_RESTORE_DURATION0</em> (2, 0x06)</p>
<p></em>バイト1– <em>LAST_RESTORE_DURATION1</em> (2, 0x07)</p>
<p>バイト2–予約済み。</p>
<p>バイト3–予約済み。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最後の消去操作の期間</strong></td>
<td align="left">4</td>
<td align="left">12</td>
<td align="left"><p>最後の消去操作の実行時間 (ミリ秒または秒単位)。</p>
<p><em>バイト0–<em>最後の消去 DURATION_TIME0</em> (2, 0x08)</p>
<p></em>バイト1– <em>LAST_ERASE DURATION_TIME1</em> (2, 0x09)</p>
<p>バイト2–予約済み</p>
<p>バイト3–予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>完了した保存操作の数</strong></td>
<td align="left">4</td>
<td align="left">16</td>
<td align="left"><p>NVDIMM モジュールの有効期間にわたって実行された保存操作の数。</p>
<p><em>バイト0– <em>NUM_SAVE_OPS_COUNT0</em> (2, 0x0a)</p>
<p></em>バイト1– <em>NUM_SAVE_OPS_COUNT1</em> (2、0x0b)</p>
<p>バイト2–予約済み。</p>
<p>バイト3–予約済み。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>完了した復元操作の数</strong></td>
<td align="left">4</td>
<td align="left">20</td>
<td align="left"><p>NVDIMM モジュールの有効期間中に完了した復元操作の数。</p>
<p><em>バイト0– <em>NUM_RESTORE_OPS_COUNT0 0</em> (2, 0x0C)</p>
<p></em>バイト1– <em>NUM_RESTORE_OPS_COUNT1</em> (2, 0x0D)</p>
<p>バイト2–予約済み。</p>
<p>バイト3–予約済み。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>完了した消去操作の数</strong></td>
<td align="left">4</td>
<td align="left">24</td>
<td align="left"><p>NVDIMM モジュールの有効期間中に完了した消去操作の数。</p>
<p><em>バイト0– <em>NUM_ERASE_COUNTS0</em> (2, 0x0e)</p>
<p></em>バイト1– <em>NUM_ERASE_COUNTS1</em> (2, 0x0F)</p>
<p>バイト2–予約済み。</p>
<p>バイト3–予約済み。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>モジュールの電源サイクル数</strong></td>
<td align="left">4</td>
<td align="left">28</td>
<td align="left"><p>NVDIMM モジュールの有効期間における電源サイクルの数。</p>
<p><em>バイト0– <em>NUM_MODULE_POWER_CYCLES0</em> (2, 0x10)</p>
<p></em>バイト1– <em>NUM_MODULE_POWER_CYCLES1</em> (2, 0x11)</p>
<p>バイト2–予約済み。</p>
<p>バイト3–予約済み。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






