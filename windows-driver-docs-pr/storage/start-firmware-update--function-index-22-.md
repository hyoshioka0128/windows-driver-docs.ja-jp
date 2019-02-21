---
title: ファームウェア更新を開始 (関数インデックス 22)
description: この関数は、特定のファームウェア スロットにファームウェアの更新を開始します。
ms.assetid: 34950124-6DBF-43CE-862A-E6DEF7A5FADE
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8479001241b1fdfade828f17224174cca17c5ee9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535766"
---
# <a name="start-firmware-update-function-index-22"></a>ファームウェア更新を開始 (関数インデックス 22)


この関数は、特定のファームウェア スロットにファームウェアの更新を開始します。 特定の時点のファームウェア更新操作の 1 つだけあります。

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
<td align="left"><strong>ファームウェア スロット</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>更新されるファームウェア スロットです。</p></td>
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
<p>1:現在進行中のファームウェア更新操作があります。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


ホストは、更新 (&)、ファームウェアのアクティブ化するには、次のファームウェア関数を呼び出します。

1.  ホストは、ファームウェア更新の開始 (関数インデックス 22) ファームウェアの更新操作を開始するを呼び出します。 この手順では、ホストは、更新するファームウェア スロットを選択します。

2.  ホストを繰り返し呼び出す[ファームウェア更新データの送信 (関数インデックス 23)](send-firmware-update-data--function-index-23-.md)デバイスにデータを転送します。 各呼び出しは、データの領域のサイズのチャンクを送信します。ホストは、最後の転送が領域のサイズがない場合のパディング責任を負います。

3.  ホスト呼び出し[完了ファームウェアの更新 (関数インデックス 24)](finish-firmware-update--function-index-24-.md)ファームウェアの更新操作があること、プラットフォームに通知します。

4.  ホスト呼び出し[ファームウェア イメージ スロットの選択 (関数インデックス 25)](select-firmware-image-slot--function-index-25-.md)新しいファームウェア イメージをアクティブ化するためにします。 更新プログラムは、次のシステム再起動時に有効になります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ファームウェアの更新データ (関数インデックス 23) の送信します。](send-firmware-update-data--function-index-23-.md)

[ファームウェアの更新 (関数インデックス 24) の完了します。](finish-firmware-update--function-index-24-.md)

[ファームウェア イメージのスロット (25 のインデックス関数) を選択します。](select-firmware-image-slot--function-index-25-.md)

[ファームウェア情報 (関数インデックス 26) を取得します。](get-firmware-info--function-index-26-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






