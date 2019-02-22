---
title: 仕入先ログ ページ サイズ (関数インデックス 14) を取得します。
description: この関数は、ホストは、仕入先のログのページの読み取りに割り当てが必要なバッファーのサイズを認識するように、仕入先のサイズのログ ページを返します。
ms.assetid: 24211D67-1D36-4711-B87B-C99546E206FC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 772c34ded9f25f64eea11d6a06e0f626b02ff557
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551170"
---
# <a name="get-vendor-log-page-size-function-index-14"></a>仕入先ログ ページ サイズ (関数インデックス 14) を取得します。


この関数は、ホストは、仕入先のログのページの読み取りに割り当てが必要なバッファーのサイズを認識するように、仕入先のサイズのログ ページを返します。

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
<td align="left"><strong>状態</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>について。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>仕入先のログのページ サイズ</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>32 バイトの倍数で仕入先のログ ページのサイズ。</p>
<p>* バイト 0 – <em>VENDOR_LOG_PAGE_SIZE</em> (0, 0x31)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[仕入先ログ ページ (関数インデックス 15) を取得します。](get-vendor-log-page--function-index-15-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






