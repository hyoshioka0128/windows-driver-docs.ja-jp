---
title: NVM のしきい値 (関数インデックス 5) を取得します。
description: この関数は NVDIMM N. 問題がある場合はヒットまたは群を抜いて、警告およびエラーのしきい値の有効期間の割合を返します
ms.assetid: E243AF8B-D70A-4FEF-BB88-ED78C4883D42
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9de60d95aeb322250c93a840d96a3e8ebfd27710
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529675"
---
# <a name="get-nvm-thresholds-function-index-5"></a>NVM のしきい値 (関数インデックス 5) を取得します。


この関数は NVDIMM N. 問題がある場合はヒットまたは群を抜いて、警告およびエラーのしきい値の有効期間の割合を返します

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
<td align="left"><strong>NVM の有効期間のパーセンテージの警告しきい値</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>非揮発性メモリの有効期間の警告しきい値の割合の値。</p>
<p><em>バイト 0 – <em>NVM_LIFETIME_WARNING_THRESHOLD</em> (0, 0x98)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NVM の有効期間の割合によるエラーのしきい値</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>非揮発性メモリの有効期間のエラーしきい値の割合の値。</p>
<p></em>バイト 0 – <em>NVM_LIFETIME_ERROR_THRESHOLD</em> (0, 0x90)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NVM の有効期間率の警告しきい値 (関数のインデックス 6) の設定します。](set-nvm-lifetime-percentage-warning-threshold--function-index-6-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






