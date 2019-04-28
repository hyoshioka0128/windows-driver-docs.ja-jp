---
title: ファームウェア情報の取得 (関数インデックス 26)
description: この関数では、ファームウェア イメージのスロットに関する情報を取得します。
ms.assetid: ABE67651-6351-4D8E-BCFF-0488D2A34DC5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 131dd2bfe35d3abb3164943835ebe578b8982f58
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379212"
---
# <a name="get-firmware-info-function-index-26"></a>ファームウェア情報の取得 (関数インデックス 26)


この関数では、ファームウェア イメージのスロットに関する情報を取得します。 呼び出す[NVDIMM-N の Id を取得する (関数インデックス 1)](get-nvdimm-n-identification--function-index-1-.md)現在のスロット番号を取得します。

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
<td align="left"><p>情報を報告するファームウェア イメージのスロットです。</p></td>
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
<td align="left"><p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>について。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>バージョン</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>指定したスロット内のファームウェア イメージのファームウェアのバージョン。</p>
<p><em>バイト 0 – <em>SLOTX_FWVER0</em> (0, 0x07/0x09)</p>
<p></em>1 – バイト<em>SLOTX_FWVER1</em> (0, 0x08/0x0A)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ファームウェア更新を開始 (関数インデックス 22)](start-firmware-update--function-index-22-.md)

[ファームウェアの更新データ (関数インデックス 23) の送信します。](send-firmware-update-data--function-index-23-.md)

[ファームウェアの更新 (関数インデックス 24) の完了します。](finish-firmware-update--function-index-24-.md)

[ファームウェア イメージのスロット (25 のインデックス関数) を選択します。](select-firmware-image-slot--function-index-25-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






