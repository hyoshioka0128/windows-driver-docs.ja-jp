---
title: I2C 書き込み (関数インデックス 28)
description: この関数は、Inter-Integrated 回線 (I2C) レジスタを書き込みます。
ms.assetid: 72DE8C76-B910-4979-BCEC-7CFFABA4CC19
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: edd5f2dea1c80235154e4042a7fc2f70aee8e67f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530919"
---
# <a name="i2c-write-function-index-28"></a>I2C 書き込み (関数インデックス 28)


この関数は、Inter-Integrated 回線 (I2C) レジスタを書き込みます。 この機能は、ベンダー固有のレジスタの使用を必要とするシナリオを実現できます。 デバッグにも使用されます。

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
<td align="left"><strong>ページ</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>I2C レジスタが配置されているページ。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>オフセット</strong></td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left"><p>登録は、ページ内のオフセットします。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>データ</strong></td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left"><p>レジスタに書き込まれるデータ。</p></td>
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
<td align="left"><strong>状態</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>この関数は、次の関数に固有のエラー コードを返すことができます。</p>
<p>1:ページが無効です。</p>
<p>2:このレジスタを書き込むことはできません。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[I2C 読み取り (関数インデックス 27)](i2c-read--function-index-27-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






