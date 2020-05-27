---
title: 保存操作要件の取得 (関数インデックス 2)
description: この関数は、保存操作のハードウェア要件に関する情報を返します。
ms.assetid: 502DAF89-F390-40A4-846C-C3B4DF3E505D
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5db57bd259630527f85d5885062dfd427f3bb795
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851269"
---
# <a name="get-save-operation-requirements-function-index-2"></a>保存操作要件の取得 (関数インデックス 2)


この関数は、保存操作のハードウェア要件に関する情報を返します。 この機能は、ホスト管理のエネルギーソース (ES) ポリシーをサポートするすべての NVDIMM で成功しますが、デバイスがデバイスで管理されている ES ポリシーをサポートしていて、保存操作の要件を利用できない場合は、エラー状態を返すことがあります。

> [!NOTE]
> スター () でマークされたすべてのレジスタ \* は、バイトアドレッシング可能なエネルギーバッキングインターフェイスの仕様で定義されているレジスタです。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>代入


### <a name="span-idarg3spanspan-idarg3spanspan-idarg3spanarg3"></a><span id="Arg3"></span><span id="arg3"></span><span id="ARG3"></span>Arg3

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
<td align="left"><p>この関数は、次の関数固有のエラーコードを返すことができます。</p>
<p>1: NVDIMM は、保存操作の要件を報告しません。</p>
<p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>に関するページを参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>平均電力要件</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>保存操作に必要な平均電力 (ミリワット)。</p>
<p><em>バイト0– <em>CSAVE_POWER_REQ0</em> (0, 0x29)</p>
<p></em>バイト1– <em>CSAVE_POWER_REQ1</em> (0, 0x2A)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>アイドル電力要件</strong></td>
<td align="left">2</td>
<td align="left">6</td>
<td align="left"><p>保存操作の完了後にモジュールが必要とする平均電力 (ミリワット)。</p>
<p><em>バイト0– <em>CSAVE_IDLE_POWER_REQ0</em> (0、0x2b)</p>
<p></em>バイト1– <em>CSAVE_IDLE_POWER_REQ1</em> (0, 0x2C)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最小電圧要件</strong></td>
<td align="left">2</td>
<td align="left">8</td>
<td align="left"><p>保存操作中に ES がサービスを必要とする最小電圧 (ミリボルト単位)</p>
<p><em>バイト0– <em>CSAVE_MIN_VOLT_REQ0</em> (0、0x2d)</p>
<p></em>バイト1– <em>CSAVE_MIN_VOLT_REQ1</em> (0、0x2e)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最大電圧要件</strong></td>
<td align="left">2</td>
<td align="left">10</td>
<td align="left"><p>保存操作中に ES がサービスを必要とする最大電圧 (ミリボルト単位)</p>
<p><em>バイト0– <em>CSAVE_MAX_VOLT_REQ0</em> (0, 0x2F)</p>
<p></em>バイト1– <em>CSAVE_MAX_VOLT_REQ1</em> (0, 0x30)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






