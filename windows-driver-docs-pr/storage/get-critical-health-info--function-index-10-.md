---
title: 正常性に関する重要な情報の取得 (関数インデックス 10)
description: この関数は、重要な正常性関連の情報を返します。
ms.assetid: 2083628D-FB46-4104-9F70-F7124B35DD04
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aa0417aefa8af1ec41b2f9c27f4bbe938069f176
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580839"
---
# <a name="get-critical-health-info-function-index-10"></a>正常性に関する重要な情報の取得 (関数インデックス 10)


この関数は、重要な正常性関連の情報を返します。 呼び出す[NVDIMM-N ヘルス情報の取得 (関数インデックス 11)](get-nvdimm-n-health-info--function-index-11-.md)と[エネルギー ソース ヘルス情報の取得 (関数インデックス 12)](get-energy-source-health-info--function-index-12-.md)さらに正常性に関する情報を取得します。

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
<td align="left"><p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>について。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>重要な正常性の情報</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>NVDIMM-N モジュールを使用して問題の高レベルの状態レポート。</p>
<p>* バイト 0 – <em>MODULE_HEALTH</em> (0, 0xA0)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NVDIMM-N の正常性の情報 (関数インデックス 11) を取得します。](get-nvdimm-n-health-info--function-index-11-.md)

[エネルギー ソース ヘルス情報 (関数インデックス 12) を取得します。](get-energy-source-health-info--function-index-12-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






