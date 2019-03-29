---
title: NVDIMM-N の遮断 (関数インデックス 20)
description: この関数腕、NVDIMM-N の電力喪失が発生した場合の操作を保存します。
ms.assetid: 15D21B5A-2320-4C22-9957-ECC0EB46B02E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 68d4792fdc244f1d5ca998792b785a05fbb89d8b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571346"
---
# <a name="span-idstoragearmnvdimm-nfunctionindex20spanarm-nvdimm-n-function-index-20"></a><span id="storage.arm_nvdimm-n__function_index_20_"></span>Arm の Nvdimm-n (関数インデックス 20)


この関数腕、NVDIMM-N の電力喪失が発生した場合の操作を保存します。 プラットフォームは、適切な保存のトリガーを選択します。

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
<p>1:操作がタイムアウトになりました。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Interface for Byte Addressable Energy Backed Function Class (Function Interface 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">バイト アドレス指定可能なエネルギー バックアップ関数クラス (関数のインターフェイスの 1) のためのインターフェイスを _DSM</a>について。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!注\]    &gt;これは、同期関数。 Arm 操作が完了またはタイムアウト時にのみを返します。操作で定義されているタイムアウトより長くかかる場合\* *ARM\_TIMEOUT0* (0, 0x20) と\* *ARM\_TIMEOUT1* (0, 0x21) プラットフォーム返す前に、この関数を中止する必要があります。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






