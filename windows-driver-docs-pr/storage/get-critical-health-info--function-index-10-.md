---
title: 正常性に関する重要な情報の取得 (関数インデックス 10)
description: この関数は、重大な正常性に関連する情報を返します。
ms.assetid: 2083628D-FB46-4104-9F70-F7124B35DD04
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 019203df61baec312c465bdb82e302477b94bb8d
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851324"
---
# <a name="get-critical-health-info-function-index-10"></a>正常性に関する重要な情報の取得 (関数インデックス 10)


この関数は、重大な正常性に関連する情報を返します。 [GET NVDIMM Health info (関数インデックス 11)](get-nvdimm-n-health-info--function-index-11-.md)を呼び出し、さらに正常性に関連する情報を取得する[エネルギーソース正常性情報 (関数インデックス 12) を取得](get-energy-source-health-info--function-index-12-.md)します。

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
<td align="left"><strong>重大な正常性の情報</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>NVDIMM モジュールに関する問題の高レベルの状態レポート。</p>
<p>* バイト0– <em>MODULE_HEALTH</em> (0、0xa0)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NVDIMM-N の正常性に関する情報の取得 (関数インデックス 11)](get-nvdimm-n-health-info--function-index-11-.md)

[電力源の正常性に関する情報の取得 (関数インデックス 12)](get-energy-source-health-info--function-index-12-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






