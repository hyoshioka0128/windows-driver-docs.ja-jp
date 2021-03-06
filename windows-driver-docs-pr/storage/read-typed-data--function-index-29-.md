---
title: 型指定されたデータの読み取り (関数インデックス 29)
description: この関数は、型指定されたブロックのデータ領域内で 32 バイトのブロックを読み取ります。
ms.assetid: 67B13EBA-F751-4E85-9143-1C331C405B85
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: afad7c003f75a3bd33c4e5c37f4f48e7403c1ebb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366358"
---
# <a name="read-typed-data-function-index-29"></a>型指定されたデータの読み取り (関数インデックス 29)


この関数は、型指定されたブロックのデータ領域内で 32 バイトのブロックを読み取ります。 この機能は、ベンダー固有のレジスタの使用を必要とするシナリオを実現できます。 デバッグにも使用されます。

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
<td align="left"><strong>[データ型]</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>データの型。 指定された値のいずれかにあるこの必要があります *<em>TYPED_BLOCK_DATA</em> (3, 0x04)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>地域 ID</strong></td>
<td align="left">2</td>
<td align="left">1</td>
<td align="left"><p>読み取られている領域の id です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ブロック ID</strong></td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left"><p>リージョン内で読み取られるブロックの id です。</p></td>
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
<p>1:無効なデータを入力します。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Data</strong></td>
<td align="left">32</td>
<td align="left">4</td>
<td align="left"><p>指定されたブロックからのデータ。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


プラットフォームは、この関数を実装するのにブロックの型指定されたデータ レジスタを使用する必要があります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[型指定されたデータ (関数インデックス 30) の書き込み](write-typed-data--function-index-30-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






