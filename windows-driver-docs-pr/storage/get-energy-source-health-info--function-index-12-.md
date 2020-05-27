---
title: 電力源の正常性に関する情報の取得 (関数インデックス 12)
description: この関数は、エネルギーソース (ES) モジュールの正常性に関する情報を返します。
ms.assetid: A2044F2A-79DA-4D3A-93B7-BE9D389DA399
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5600bcb32cbcbc152a7e7aceb32693929fa3804a
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851317"
---
# <a name="get-energy-source-health-info-function-index-12"></a>電力源の正常性に関する情報の取得 (関数インデックス 12)


この関数は、エネルギーソース (ES) モジュールの正常性に関する情報を返します。 ES がホストによって管理され、正常性の情報が利用できない場合、この関数はエラー状態を返すことがあります。

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
<td align="left"><p>この関数は、次の関数固有のエラーコードを返すことができます。</p>
<p>1: プラットフォームは ES の正常性情報をサポートしていません。</p>
<p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>に関するページを参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 有効期間の割合</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>最後に認識された有効期間の割合。</p>
<p><em>バイト0– <em>ES_LIFETIME</em> (1, 0x70)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>現在の気温</strong></td>
<td align="left">2</td>
<td align="left">5</td>
<td align="left"><p>温度 (摂氏)。 最小値は 0 です。</p>
<p></em>バイト0– <em>ES_TEMP0</em> (1, 0x71)</p>
<p><em>バイト1– <em>ES_TEMP1</em> (1, 0x72)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>合計実行時間</strong></td>
<td align="left">4</td>
<td align="left">7</td>
<td align="left"><p>ES が製造されてからの経過時間 (時間)。</p>
<p></em>バイト0– <em>ES_RUNTIME0</em> (1, 0x73)</p>
<p>* バイト1– <em>ES_RUNTIME1</em> (1, 0x74)</p>
<p>バイト2–予約済み</p>
<p>バイト3–予約済み</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NVDIMM-N の正常性に関する情報の取得 (関数インデックス 11)](get-nvdimm-n-health-info--function-index-11-.md)

[電力源の正常性に関する情報の取得 (関数インデックス 12)](get-energy-source-health-info--function-index-12-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






