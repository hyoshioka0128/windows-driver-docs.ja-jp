---
title: 設定にリセットして既定値は (関数インデックス 21)
description: この関数は、構成済みの仕入先の設定に戻す、NVDIMM-N をリセットします。
ms.assetid: 64CEF5C8-FC2A-4C6E-829C-27E18A4EDC26
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bb6598830bb7efc03f016b22dfe2949a2904eb42
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548618"
---
# <a name="reset-to-factory-defaults-function-index-21"></a>設定にリセットして既定値は (関数インデックス 21)


この関数は、構成済みの仕入先の設定に戻す、NVDIMM-N をリセットします。

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
<td align="left"><p>この関数は、次の関数に固有のエラー コードを返すことができます。</p>
<p>1:操作がタイムアウトになりました。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!注\]    &gt;プラットフォームは 3 回の最大保存を完了する工場出荷時の既定の操作のタイムアウトを待機 (たとえば、保存のタイムアウトの最大数が 60 秒の場合は、プラットフォームは 180 秒間待ってから)。 場合は、操作は、その間隔より長くかかる、プラットフォームは操作を中止し、関数固有のエラー コード (操作がタイムアウトになりました) 1 を返します。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






