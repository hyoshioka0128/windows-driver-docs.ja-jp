---
title: 保存操作要件の取得 (関数インデックス 2)
description: この関数は、保存を行うためのハードウェア要件に関する情報を返します操作。
ms.assetid: 502DAF89-F390-40A4-846C-C3B4DF3E505D
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 73350bb78925e11a1507e19e25c5cea67f174e0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579797"
---
# <a name="get-save-operation-requirements-function-index-2"></a>保存操作要件の取得 (関数インデックス 2)


この関数は、保存を行うためのハードウェア要件に関する情報を返します操作。 この関数は、ホストで管理されたエネルギー ソース (ES) ポリシーをサポートするデバイスが ES ポリシーのデバイス管理をサポートし、保存操作の要件が使用できない場合、エラー状態を返す可能性がありますすべての Nvdimm-n の成功ものとします。

&gt; \[!注\]    &gt;、星が付いたマークされているすべてのレジスタ (\*) バイト アドレス指定可能なエネルギー バックアップ インターフェイス仕様で定義されているレジスタします。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>入力


### <a name="span-idarg3spanspan-idarg3spanspan-idarg3spanarg3"></a><span id="Arg3"></span><span id="arg3"></span><span id="ARG3"></span>arg3…

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
<td align="left"><p>この関数は、次の関数に固有のエラー コードを返すことができます。</p>
<p>1:NVDIMM-N は、保存操作の要件は報告されません。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>平均電力要件</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>平均電力 (ミリ) の保存に必要な操作です。</p>
<p><em>バイト 0 – <em>CSAVE_POWER_REQ0</em> (0, 0x29)</p>
<p></em>1 – バイト<em>CSAVE_POWER_REQ1</em> (0, 0x2A)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>アイドル状態の電源の要件</strong></td>
<td align="left">2</td>
<td align="left">6</td>
<td align="left"><p>平均の能力 (ミリ) のモジュールに、保存後に必要な操作が完了します。</p>
<p><em>バイト 0 – <em>CSAVE_IDLE_POWER_REQ0</em> (0, 0x2B)</p>
<p></em>1 – バイト<em>CSAVE_IDLE_POWER_REQ1</em> (0, 0x2C)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>電圧が最小要件</strong></td>
<td align="left">2</td>
<td align="left">8</td>
<td align="left"><p>最小の電圧 ((ミリボルト)) で、ES がサービスに保存するときに操作</p>
<p><em>バイト 0 – <em>CSAVE_MIN_VOLT_REQ0</em> (0, 0x2D)</p>
<p></em>1 – バイト<em>CSAVE_MIN_VOLT_REQ1</em> (0, 0x2E)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最大 Voltage 要件</strong></td>
<td align="left">2</td>
<td align="left">10</td>
<td align="left"><p>最大の電圧 ((ミリボルト)) で、ES がサービスに保存するときに操作</p>
<p><em>バイト 0 – <em>CSAVE_MAX_VOLT_REQ0</em> (0, 0x2F)</p>
<p></em>1 – バイト<em>CSAVE_MAX_VOLT_REQ1</em> (0, 0x30)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






