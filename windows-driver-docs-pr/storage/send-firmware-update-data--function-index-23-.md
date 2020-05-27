---
title: ファームウェア更新データの送信 (関数インデックス 23)
description: この関数は、ファームウェアデータをデバイスに送信します。
ms.assetid: 3F28C89B-040A-407B-B780-96D6767DC5C7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: be9d74fe6e2bb02a7568056a1f66bfd717b7b434
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851253"
---
# <a name="send-firmware-update-data-function-index-23"></a>ファームウェア更新データの送信 (関数インデックス 23)


この関数は、ファームウェアデータをデバイスに送信します。

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
<td align="left"><strong>領域の長さ</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>この関数で送信されているバイト数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Region ID\(リージョン ID\)</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>書き込まれている領域の id。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ブロック ID</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>領域内に記述されているブロックの id。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ファームウェアデータ</strong></td>
<td align="left"><em>領域の長さ</em>によって指定された数値。</td>
<td align="left">7</td>
<td align="left"><p>ファームウェアイメージデータのリージョンサイズのパケット。</p></td>
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
<p>1: ファームウェアの更新操作は実行されていません。</p>
<p>2: 領域のサイズが無効です。</p>
<p>3: データが破損しているため、転送に失敗しました。</p>
<p>4: 操作がタイムアウトしました。</p>
<p>5: ファームウェアのコミット操作に失敗しました。</p>
<p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>に関するページを参照してください。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> この関数は、ファームウェアデータの CRC を計算し、それを \* *fw \_ region \_ CRC0* (3, 0x40) と \* *fw \_ region \_ CRC1* (3, 0x41) と比較します。 値が一致しない場合、関数は関数固有のエラーコード3で失敗します。 CRC アルゴリズム仕様については、バイトアドレッシング可能なエネルギーバッキングインターフェイス JEDEC standard を参照してください。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ファームウェア更新の開始 (関数インデックス 22)](start-firmware-update--function-index-22-.md)

[ファームウェア更新の終了 (関数インデックス 24)](finish-firmware-update--function-index-24-.md)

[ファームウェア イメージ スロットの選択 (関数インデックス 25)](select-firmware-image-slot--function-index-25-.md)

[ファームウェア情報の取得 (関数インデックス 26)](get-firmware-info--function-index-26-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






