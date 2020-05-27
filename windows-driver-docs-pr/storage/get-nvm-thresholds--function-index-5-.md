---
title: NVM しきい値の取得 (関数インデックス 5)
description: この関数は、有効期間の割合の警告とエラーのしきい値を返します。ヒットした場合、またはそれを超える場合は、NVDIMM に問題があることを示します。
ms.assetid: E243AF8B-D70A-4FEF-BB88-ED78C4883D42
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 648ead7aea1931b520f819cbbaaa9c4df83b7acf
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851455"
---
# <a name="get-nvm-thresholds-function-index-5"></a>NVM しきい値の取得 (関数インデックス 5)


この関数は、有効期間の割合の警告とエラーのしきい値を返します。ヒットした場合、またはそれを超える場合は、NVDIMM に問題があることを示します。

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
<td align="left"><strong>NVM の有効期間の割合-警告しきい値</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>非揮発性メモリの有効期間の警告しきい値の割合の値。</p>
<p><em>バイト0– <em>NVM_LIFETIME_WARNING_THRESHOLD</em> (0、0x98)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NVM の有効期間の割合のエラーしきい値</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>不揮発性メモリの有効期間のエラーしきい値の割合の値。</p>
<p></em>バイト0– <em>NVM_LIFETIME_ERROR_THRESHOLD</em> (0、0x90)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NVM 有効期間の割合に関する警告しきい値の設定 (関数インデックス 6)](set-nvm-lifetime-percentage-warning-threshold--function-index-6-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






