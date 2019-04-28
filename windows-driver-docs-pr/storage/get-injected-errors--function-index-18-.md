---
title: 挿入されたエラーの取得 (関数インデックス 18)
description: この関数は、挿入された現在のエラーに関する情報を返します。
ms.assetid: 60D4E64C-ABB6-4B24-971F-594306D8C07C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bcf77d0d8e67a87e4d60189fd9de968f8cd65ff5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379758"
---
# <a name="get-injected-errors-function-index-18"></a>挿入されたエラーの取得 (関数インデックス 18)


この関数は、挿入された現在のエラーに関する情報を返します。

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
<td align="left"><strong>挿入操作の失敗</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>エラーが挿入された現在どの操作または非揮発性メモリに関する情報。</p>
<p><em>バイト 0 – <em>INJECT_OPS_FAILURES</em> (2, 0x60 です)</p>
<p></em>1 – バイト場合<em>INJECT_BAD_BLOCKS</em>は '1' (7 バイトのビット 0)、これは<em> <em>INJECT_BAD_BLOCK_CAP</em> (2, 0x67)。 それ以外の場合、0 になりますこのものとします。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>挿入されたエネルギー ソース エラー</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>についてどのエネルギー ソース (ES) エラーが挿入された現在の情報。</p>
<p></em>バイト 0 – <em>INJECT_ES_FAILURES</em> (2, 0x64)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>挿入されたファームウェアの更新の失敗</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>操作エラーが挿入された現在ファームウェアに関する情報。</p>
<p>* バイト 0 – <em>INJECT_FW_FAILURES</em> (2, 0x65)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


プラットフォームには、エラー インジェクションが無効にした場合、この関数は成功し、現在挿入エラーがない場合と同じ情報を返す必要があります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[エラー (関数インデックス 17) を挿入します。](inject-error--function-index-17-.md)

[クエリ エラーの挿入の状態 (関数インデックス 16)](query-error-injection-status--function-index-16-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






