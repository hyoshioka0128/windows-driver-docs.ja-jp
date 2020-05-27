---
title: 型指定されたデータの書き込み (関数インデックス 30)
description: この関数は、型指定されたブロックデータ領域内に32バイトのブロックを書き込みます。
ms.assetid: 0162E7C3-CF1E-452C-908E-D65C090CD365
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d6f5cb57d8034a338512b04ffaeb3dcdc2b84e6e
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851329"
---
# <a name="write-typed-data-function-index-30"></a>型指定されたデータの書き込み (関数インデックス 30)


この関数は、型指定されたブロックデータ領域内に32バイトのブロックを書き込みます。 この機能により、ベンダー固有のレジスタを使用する必要があるシナリオが可能になります。 デバッグにも使用されます。

> [!NOTE]
> スター () でマークされたすべてのレジスタ \* は、バイトアドレッシング可能なエネルギーバッキングインターフェイスの仕様で定義されているレジスタです。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>代入


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
<th align="left">バイト長</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>[データ型]</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>データの型。 *<em>TYPED_BLOCK_DATA</em> (3, 0x04) で指定された値のいずれかである必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Region ID\(リージョン ID\)</strong></td>
<td align="left">2</td>
<td align="left">1</td>
<td align="left"><p>書き込まれているリージョンの id</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ブロック ID</strong></td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left"><p>領域内に記述されているブロックの id。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>データ</strong></td>
<td align="left">32</td>
<td align="left">4</td>
<td align="left"><p>書き込むデータ。</p></td>
</tr>
</tbody>
</table>

 

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
<p>1: データ型が無効です。</p>
<p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>に関するページを参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


このプラットフォームでは、型指定されたブロックデータレジスタを使用してこの関数を実装する必要があります。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[型指定されたデータの読み取り (関数インデックス 29)](read-typed-data--function-index-29-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






