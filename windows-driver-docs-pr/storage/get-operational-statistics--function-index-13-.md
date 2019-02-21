---
title: (関数インデックス 13) の運用統計を取得します。
description: この関数は、NVDIMM N. によって実行される操作を追跡するカウンターを返します。
ms.assetid: D396F42E-9B11-46D7-8D9C-FE00B4998DEC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0b10feb825a656d6323e683e802f553d5117d626
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538383"
---
# <a name="get-operational-statistics-function-index-13"></a>(関数インデックス 13) の運用統計を取得します。


この関数は、NVDIMM N. によって実行される操作を追跡するカウンターを返します。

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
<td align="left"><strong>状態</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>について。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>保存操作の最後の期間</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>最後に操作の実行時間 (ミリ秒または秒単位) で保存します。</p>
<p><em>バイト 0 – <em>LAST_SAVE_DURATION0</em> (2, 0x04)</p>
<p></em>1 – バイト<em>LAST_SAVE_DURATION1</em> (2, 0x05)</p>
<p>2 – バイトに予約されています。</p>
<p>3 – バイトに予約されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最後の復元操作の実行中</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>最後の復元操作の期間 (ミリ秒または秒単位)。</p>
<p><em>バイト 0 – <em>LAST_RESTORE_DURATION0</em> (2, 0x06)</p>
<p></em>1 – バイト<em>LAST_RESTORE_DURATION1</em> (2, 0x07)</p>
<p>2 – バイトに予約されています。</p>
<p>3 – バイトに予約されています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最後の消去操作の実行中</strong></td>
<td align="left">4</td>
<td align="left">12</td>
<td align="left"><p>最後には、操作の実行時間のミリ秒または秒を消去します。</p>
<p><em>バイト 0 –<em>最後の消去 DURATION_TIME0</em> (2, 0x08)</p>
<p></em>1 – バイト<em>LAST_ERASE DURATION_TIME1</em> (2, 0x09)</p>
<p>バイト 2: 予約されています</p>
<p>バイト 3 – に予約されています</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>保存操作の完了数</strong></td>
<td align="left">4</td>
<td align="left">16</td>
<td align="left"><p>NVDIMM-N モジュール経由で保存操作の数が完了した&#39;有効期間。</p>
<p><em>バイト 0 – <em>NUM_SAVE_OPS_COUNT0</em> (2, 0x0A)</p>
<p></em>1 – バイト<em>NUM_SAVE_OPS_COUNT1</em> (2, 0x0B)</p>
<p>2 – バイトに予約されています。</p>
<p>3 – バイトに予約されています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>完了した復元操作の数</strong></td>
<td align="left">4</td>
<td align="left">20</td>
<td align="left"><p>NVDIMM-N モジュール経由で完了した復元操作の数&#39;有効期間。</p>
<p><em>バイト 0 – <em>NUM_RESTORE_OPS_COUNT0 0</em> (2, 0x0C)</p>
<p></em>1 – バイト<em>NUM_RESTORE_OPS_COUNT1</em> (2, 0x0D)</p>
<p>2 – バイトに予約されています。</p>
<p>3 – バイトに予約されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>完了した消去操作の数</strong></td>
<td align="left">4</td>
<td align="left">24</td>
<td align="left"><p>NVDIMM-N モジュール経由での消去が完了した操作の数&#39;有効期間。</p>
<p><em>バイト 0 – <em>NUM_ERASE_COUNTS0</em> (2, 0x0E)</p>
<p></em>1 – バイト<em>NUM_ERASE_COUNTS1</em> (2, 0x0F)</p>
<p>2 – バイトに予約されています。</p>
<p>3 – バイトに予約されています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>モジュールの電源サイクルの数</strong></td>
<td align="left">4</td>
<td align="left">28</td>
<td align="left"><p>電源の数が NVDIMM-N モジュール経由でサイクル&#39;有効期間。</p>
<p><em>バイト 0 – <em>NUM_MODULE_POWER_CYCLES0</em> (2, 0x10)</p>
<p></em>1 – バイト<em>NUM_MODULE_POWER_CYCLES1</em> (2, パターン)</p>
<p>2 – バイトに予約されています。</p>
<p>3 – バイトに予約されています。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






