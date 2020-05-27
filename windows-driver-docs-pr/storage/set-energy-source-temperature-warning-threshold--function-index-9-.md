---
title: 電力源の温度に関する警告しきい値の設定 (関数インデックス 9)
description: この関数は、エネルギーソースの温度の警告しきい値を設定します。
ms.assetid: AE624191-87F2-4673-A31B-CABE94623535
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8e97e76b26045ff1068ce65bb77a4b75911c2439
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851480"
---
# <a name="set-energy-source-temperature-warning-threshold-function-index-9"></a>電力源の温度に関する警告しきい値の設定 (関数インデックス 9)


この関数は、エネルギーソースの温度の警告しきい値を設定します。 ES がホストによって管理され、しきい値がプラットフォームでサポートされていない場合、この関数はエラー状態を返すことがあります。

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
<td align="left"><strong>ES 有効期間の温度警告のしきい値</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>警告しきい値の新しい値 (摂氏)。</p>
<p>プラットフォームは、この値を *<em>ES_TEMP_WARNING_THRESHOLD</em> (0, 0x99) レジスタに書き込みます。</p></td>
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
<p>1: プラットフォームは、ES のしきい値をサポートしていません。</p>
<p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>に関するページを参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[電力源の有効期間に関する警告しきい値の設定 (関数インデックス 8)](set-energy-source-lifetime-warning-threshold--function-index-8-.md)

[電力源しきい値の取得 (関数インデックス 7)](get-energy-source-thresholds--function-index-7-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






