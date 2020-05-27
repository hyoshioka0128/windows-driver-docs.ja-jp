---
title: ファームウェア情報の取得 (関数インデックス 26)
description: この関数は、ファームウェアイメージスロットに関する情報を取得します。
ms.assetid: ABE67651-6351-4D8E-BCFF-0488D2A34DC5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 82253e65ea939a7ae4821708cd517d056820b656
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851333"
---
# <a name="get-firmware-info-function-index-26"></a>ファームウェア情報の取得 (関数インデックス 26)


この関数は、ファームウェアイメージスロットに関する情報を取得します。 [GET NVDIMM-N id (関数インデックス 1)](get-nvdimm-n-identification--function-index-1-.md)を呼び出して、現在のスロット番号を取得します。

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
<td align="left"><p>情報を報告するファームウェアイメージスロット。</p></td>
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
<td align="left"><p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>にアクセスしてください。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Version</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>指定されたスロットのファームウェアイメージのファームウェアバージョン。</p>
<p><em>バイト0– <em>SLOTX_FWVER0</em> (0, 0x07/0x09)</p>
<p></em>バイト1– <em>SLOTX_FWVER1</em> (0、0X08/0x0a)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ファームウェア更新の開始 (関数インデックス 22)](start-firmware-update--function-index-22-.md)

[ファームウェア更新データの送信 (関数インデックス 23)](send-firmware-update-data--function-index-23-.md)

[ファームウェア更新の終了 (関数インデックス 24)](finish-firmware-update--function-index-24-.md)

[ファームウェア イメージ スロットの選択 (関数インデックス 25)](select-firmware-image-slot--function-index-25-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






