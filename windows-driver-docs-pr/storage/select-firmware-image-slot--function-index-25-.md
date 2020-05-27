---
title: ファームウェア イメージ スロットの選択 (関数インデックス 25)
description: この関数は、アクティブなファームウェアイメージを選択します。
ms.assetid: 65B8BF11-4377-455A-9A08-0C15FADC0BBC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03858a7aaa6c4a2525175b91c94452c42100ad8d
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851257"
---
# <a name="select-firmware-image-slot-function-index-25"></a>ファームウェア イメージ スロットの選択 (関数インデックス 25)


この関数は、アクティブなファームウェアイメージを選択します。 選択したイメージは、デバイスのリセット時に読み込まれます。

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
<td align="left"><strong>ファームウェアスロット</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>デバイスがリセットされたときにアクティブとして選択されるファームウェアイメージスロット。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> ファームウェアは、**ファームウェアスロット**値を \* *FW \_ スロット \_ 情報*(3、0x42) レジスタの下位4ビットに書き込みます。

 

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
<p>1: 無効なスロット番号。</p>
<p>2: このスロットにはイメージがありません。</p>
<p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>に関するページを参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ファームウェア更新の開始 (関数インデックス 22)](start-firmware-update--function-index-22-.md)

[ファームウェア更新データの送信 (関数インデックス 23)](send-firmware-update-data--function-index-23-.md)

[ファームウェア更新の終了 (関数インデックス 24)](finish-firmware-update--function-index-24-.md)

[ファームウェア情報の取得 (関数インデックス 26)](get-firmware-info--function-index-26-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






