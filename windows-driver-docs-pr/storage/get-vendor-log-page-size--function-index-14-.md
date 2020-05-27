---
title: ベンダーのログ ページ サイズの取得 (関数インデックス 14)
description: この関数は、ベンダーログページのサイズを返します。これにより、ホストは、ベンダログページを読み取るために割り当てる必要があるバッファーのサイズを把握できます。
ms.assetid: 24211D67-1D36-4711-B87B-C99546E206FC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aafc1d581b67a9f36a8e72db53827f755297dcab
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851701"
---
# <a name="get-vendor-log-page-size-function-index-14"></a>ベンダーのログ ページ サイズの取得 (関数インデックス 14)


この関数は、ベンダーログページのサイズを返します。これにより、ホストは、ベンダログページを読み取るために割り当てる必要があるバッファーのサイズを把握できます。

> [!NOTE]
> スター () でマークされたすべてのレジスタ \* は、バイトアドレッシング可能なエネルギーバッキングインターフェイスの仕様で定義されているレジスタです。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>代入


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

[なし] :

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
<td align="left"><strong>ベンダログのページサイズ</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>32バイトの倍数単位のベンダログページのサイズ。</p>
<p>* バイト0– <em>VENDOR_LOG_PAGE_SIZE</em> (0, 0x31)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ベンダーのログ ページの取得 (関数インデックス 15)](get-vendor-log-page--function-index-15-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






