---
title: NVM 有効期間の割合に関する警告しきい値の設定 (関数インデックス 6)
description: この関数は、非揮発性メモリの有効期間の残りの割合の警告しきい値を設定します。
ms.assetid: B5568876-D9E1-4086-8819-FC5FF6BC2C15
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: af49417ca18f17f9e56f710921d7df32a848ebc2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373462"
---
# <a name="set-nvm-lifetime-percentage-warning-threshold-function-index-6"></a>NVM 有効期間の割合に関する警告しきい値の設定 (関数インデックス 6)


この関数は、非揮発性メモリの有効期間の残りの割合の警告しきい値を設定します。

&gt; \[!注\]    &gt;、星が付いたマークされているすべてのレジスタ (\*) バイト アドレス指定可能なエネルギー バックアップ インターフェイス仕様で定義されているレジスタします。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>入力


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

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
<td align="left"><strong>NVM の有効期間のパーセンテージの警告しきい値</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>0 ~ 100 にする必要があります警告しきい値をパーセント値。</p>
<p>プラットフォームは、この値を書き込みは、*<em>NVM_LIFETIME_WARNING_THRESHOLD (0, 0x98)</em>を登録します。</p></td>
</tr>
</tbody>
</table>

 

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
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NVM のしきい値 (関数インデックス 5) を取得します。](get-nvm-thresholds--function-index-5-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






