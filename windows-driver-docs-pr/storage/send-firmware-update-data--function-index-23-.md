---
title: ファームウェア更新データの送信 (関数インデックス 23)
description: この関数は、デバイスにファームウェアのデータを送信します。
ms.assetid: 3F28C89B-040A-407B-B780-96D6767DC5C7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03fa586e262c45e0e1f80c141bd3fb7732de7827
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372357"
---
# <a name="send-firmware-update-data-function-index-23"></a>ファームウェア更新データの送信 (関数インデックス 23)


この関数は、デバイスにファームウェアのデータを送信します。

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
<td align="left"><strong>領域の長さ</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>この関数に送信するバイト数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>地域 ID</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>書き込まれる領域の id です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ブロック ID</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>領域の内側に書き込まれるブロックの id です。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ファームウェアのデータ</strong></td>
<td align="left">指定された数<em>領域の長さ</em>します。</td>
<td align="left">7</td>
<td align="left"><p>リージョン規模のファームウェア イメージのデータのパケットです。</p></td>
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
<p>1:実行中のファームウェア更新操作はありません。</p>
<p>2:無効な領域のサイズ。</p>
<p>3:データの破損により、転送が失敗しました。</p>
<p>4:操作がタイムアウトしました。</p>
<p>5:ファームウェアのコミット操作が失敗しました。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!注\]    &gt;この関数はファームウェアのデータの CRC を計算し、比較して\* *FW\_リージョン\_CRC0* (3, 0x40) と\* *FW\_リージョン\_CRC1* (3, 0x41)。 値が一致しない場合、関数は関数に固有のエラー コード 3 では失敗します。 バイト アドレス指定可能なエネルギー バックアップ インターフェイス JEDEC CRC アルゴリズムの指定の標準を参照してください。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ファームウェア更新を開始 (関数インデックス 22)](start-firmware-update--function-index-22-.md)

[ファームウェアの更新 (関数インデックス 24) の完了します。](finish-firmware-update--function-index-24-.md)

[ファームウェア イメージのスロット (25 のインデックス関数) を選択します。](select-firmware-image-slot--function-index-25-.md)

[ファームウェア情報 (関数インデックス 26) を取得します。](get-firmware-info--function-index-26-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






