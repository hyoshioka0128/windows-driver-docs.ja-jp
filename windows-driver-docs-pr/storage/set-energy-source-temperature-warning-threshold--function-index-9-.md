---
title: 電力源の温度に関する警告しきい値の設定 (関数インデックス 9)
description: この関数は、温度がエネルギー ソース (ES) の警告しきい値を設定します。
ms.assetid: AE624191-87F2-4673-A31B-CABE94623535
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8cd26d9b84f1d9e3a57b5f0a21c5e7845997cb91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376426"
---
# <a name="set-energy-source-temperature-warning-threshold-function-index-9"></a>電力源の温度に関する警告しきい値の設定 (関数インデックス 9)


この関数は、温度がエネルギー ソース (ES) の警告しきい値を設定します。 この関数は、ES が管理されているホストとしきい値が、プラットフォームでサポートされていない場合、エラー状態を返す可能性があります。

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
<td align="left"><strong>ES の有効期間の温度の警告しきい値</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>警告しきい値の (摂氏) に新しい値。</p>
<p>プラットフォームは、この値を書き込みは、*<em>ES_TEMP_WARNING_THRESHOLD</em> (0, 0x99) を登録します。</p></td>
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


[エネルギーのソースの有効期間の警告しきい値 (関数インデックス 8) の設定します。](set-energy-source-lifetime-warning-threshold--function-index-8-.md)

[エネルギー ソースしきい値 (関数インデックス 7) を取得します。](get-energy-source-thresholds--function-index-7-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






