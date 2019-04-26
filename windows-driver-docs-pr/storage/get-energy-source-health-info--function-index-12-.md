---
title: 電力源の正常性に関する情報の取得 (関数インデックス 12)
description: この関数は、エネルギー ソース (ES) モジュールの正常性に関する情報を返します。
ms.assetid: A2044F2A-79DA-4D3A-93B7-BE9D389DA399
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a5458376ec4e849e6d95b795b7fab113dc66d8d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355837"
---
# <a name="get-energy-source-health-info-function-index-12"></a>電力源の正常性に関する情報の取得 (関数インデックス 12)


この関数は、エネルギー ソース (ES) モジュールの正常性に関する情報を返します。 この関数は、ES が管理されているホストと正常性の情報が利用できない場合、エラー状態を返す可能性があります。

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
<td align="left"><p>この関数は、次の関数に固有のエラー コードを返すことができます。</p>
<p>1:プラットフォームは、ES の正常性に関する情報をサポートしていません。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES の有効期間の割合</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>最終正常 ES の有効期間の割合。</p>
<p><em>バイト 0 – <em>ES_LIFETIME</em> (1, 0x70 です)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES の現在の気温</strong></td>
<td align="left">2</td>
<td align="left">5</td>
<td align="left"><p>ES の温度を摂氏でします。 最小値は 0 です。</p>
<p></em>バイト 0 – <em>ES_TEMP0</em> (1, 0x71)</p>
<p><em>1 – バイト<em>ES_TEMP1</em> (1, 0x72)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>合計実行時間</strong></td>
<td align="left">4</td>
<td align="left">7</td>
<td align="left"><p>時間 (時間)、ES 経過運用製造時にします。</p>
<p></em>バイト 0 – <em>ES_RUNTIME0</em> (1, 0x73)</p>
<p>* バイト 1 – <em>ES_RUNTIME1</em> (1, 0x74)</p>
<p>バイト 2: 予約されています</p>
<p>バイト 3 – に予約されています</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NVDIMM-N の正常性の情報 (関数インデックス 11) を取得します。](get-nvdimm-n-health-info--function-index-11-.md)

[エネルギー ソース ヘルス情報 (関数インデックス 12) を取得します。](get-energy-source-health-info--function-index-12-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






