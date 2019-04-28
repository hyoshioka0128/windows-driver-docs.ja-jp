---
title: エラー挿入状態のクエリ (関数インデックス 16)
description: この関数は、NVDIMM-N のエラー挿入の状態を返します。
ms.assetid: 7CE07551-666F-4E07-8115-806F6256B595
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1f12342d3466f019ff23a431496bb4c4f86b77af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366266"
---
# <a name="query-error-injection-status-function-index-16"></a>エラー挿入状態のクエリ (関数インデックス 16)


この関数は、NVDIMM-N のエラー挿入の状態を返します。 プラットフォームのみなど、特定のシナリオでのエラーの挿入を有効にすることもできます、ユーザーが BIOS 設定を構成した後。

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
<td align="left"><strong>有効になっているエラーの挿入</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>エラーの挿入が有効になっているかどうか。</p>
<p>0 の場合、エラーの挿入は無効です。</p>
<p>1 の場合、エラーの挿入が有効にします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[エラー (関数インデックス 17) を挿入します。](inject-error--function-index-17-.md)

[挿入されたエラー (関数インデックス 18) の取得](get-injected-errors--function-index-18-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






