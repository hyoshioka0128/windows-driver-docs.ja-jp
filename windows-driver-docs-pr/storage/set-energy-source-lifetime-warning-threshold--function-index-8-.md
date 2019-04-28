---
title: 電力源の有効期間に関する警告しきい値の設定 (関数インデックス 8)
description: この関数は、エネルギー ソース (ES) の有効期間の残りの割合の警告しきい値を設定します。
ms.assetid: 18D80829-8B54-48CE-A4A1-C3D57D0F60DC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3ccd5d51b5aed7bcd56847cb66db1fab274c4726
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362262"
---
# <a name="set-energy-source-lifetime-warning-threshold-function-index-8"></a>電力源の有効期間に関する警告しきい値の設定 (関数インデックス 8)


この関数は、エネルギー ソース (ES) の有効期間の残りの割合の警告しきい値を設定します。 この関数は、ES が管理されているホストし、プラットフォームがしきい値をサポートしていない場合、エラー状態を返す可能性があります。

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
<td align="left"><strong>ES の有効期間のパーセンテージの警告しきい値</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>0 ~ 100 にする必要があります警告しきい値をパーセント値。</p>
<p>プラットフォームは、この値を書き込みは、*<em>ES_LIFETIME_WARNING_THRESHOLD</em> (0, 0x99) を登録します。</p></td>
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
<td align="left"><p>この関数は、次の関数に固有のエラー コードを返すことができます。</p>
<p>1:プラットフォームは、ES のしきい値をサポートしていません。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[エネルギー ソース温度の警告しきい値 (関数インデックス 9) の設定します。](set-energy-source-temperature-warning-threshold--function-index-9-.md)

[エネルギー ソースしきい値 (関数インデックス 7) を取得します。](get-energy-source-thresholds--function-index-7-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






