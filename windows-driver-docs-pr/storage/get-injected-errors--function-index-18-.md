---
title: 挿入されたエラーの取得 (関数インデックス 18)
description: この関数は、現在挿入されているエラーに関する情報を返します。
ms.assetid: 60D4E64C-ABB6-4B24-971F-594306D8C07C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 51cafcd33b6004d1acb7316af53e7a66af26886c
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851331"
---
# <a name="get-injected-errors-function-index-18"></a>挿入されたエラーの取得 (関数インデックス 18)


この関数は、現在挿入されているエラーに関する情報を返します。

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
<td align="left"><strong>挿入した操作エラー</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>現在挿入されている操作または非揮発性メモリエラーに関する情報。</p>
<p><em>バイト0– <em>INJECT_OPS_FAILURES</em> (2, 0x60)</p>
<p></em>バイト1– <em>INJECT_BAD_BLOCKS</em>が ' 1 ' (バイト0のビット 7) の場合、これは <em> <em>INJECT_BAD_BLOCK_CAP</em> (2, 0x67) です。 それ以外の場合は0になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>エネルギーソースの障害が挿入</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>現在挿入されているエネルギーソースエラーに関する情報。</p>
<p></em>バイト0– <em>INJECT_ES_FAILURES</em> (2、0x64)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ファームウェア更新エラーが挿入</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>現在どのファームウェア操作エラーが挿入されているかについての情報。</p>
<p>* バイト0– <em>INJECT_FW_FAILURES</em> (2, 0x65)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


プラットフォームでエラーインジェクションが無効にされた場合、この関数は成功し、現在エラーが挿入されていない場合と同じ情報を返します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[エラーの挿入 (関数インデックス 17)](inject-error--function-index-17-.md)

[エラー挿入状態のクエリ (関数インデックス 16)](query-error-injection-status--function-index-16-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






