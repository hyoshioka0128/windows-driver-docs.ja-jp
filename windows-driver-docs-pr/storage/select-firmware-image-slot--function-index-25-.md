---
title: ファームウェア イメージのスロット (25 のインデックス関数) を選択します。
description: この関数は、ファームウェア イメージがアクティブなを選択します。
ms.assetid: 65B8BF11-4377-455A-9A08-0C15FADC0BBC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: db61d647aabb4c20f6006d3bc348773eb80f9f08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532460"
---
# <a name="select-firmware-image-slot-function-index-25"></a>ファームウェア イメージのスロット (25 のインデックス関数) を選択します。


この関数は、ファームウェア イメージがアクティブなを選択します。 デバイスをリセットすると、選択したイメージを読み込む必要があります。

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
<td align="left"><strong>ファームウェア スロット</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>ファームウェア イメージ スロットに、デバイスをリセットするとアクティブとして選択する必要があります。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!注\]    &gt;ファームウェアを書き込む必要があります、**ファームウェア スロット**値の下位 4 ビットを\* *FW\_スロット\_情報*(3, 0x42) を登録します。

 

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
<p>1:無効なスロットの数。</p>
<p>2:このスロット内のイメージはありません。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ファームウェア更新を開始 (関数インデックス 22)](start-firmware-update--function-index-22-.md)

[ファームウェアの更新データ (関数インデックス 23) の送信します。](send-firmware-update-data--function-index-23-.md)

[ファームウェアの更新 (関数インデックス 24) の完了します。](finish-firmware-update--function-index-24-.md)

[ファームウェア情報 (関数インデックス 26) を取得します。](get-firmware-info--function-index-26-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






