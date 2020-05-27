---
title: 出荷時の既定値へのリセット (関数インデックス 21)
description: この関数は、製造元が事前に構成した設定に NVDIMM をリセットします。
ms.assetid: 64CEF5C8-FC2A-4C6E-829C-27E18A4EDC26
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 455f32429fc67349788dde17465a2980a6d6c379
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851263"
---
# <a name="reset-to-factory-defaults-function-index-21"></a>出荷時の既定値へのリセット (関数インデックス 21)


この関数は、製造元が事前に構成した設定に NVDIMM をリセットします。

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
<td align="left"><p>この関数は、次の関数固有のエラーコードを返すことができます。</p>
<p>1: 操作がタイムアウトしました。</p>
<p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>に関するページを参照してください。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> プラットフォームは、出荷時の既定の操作が完了するまでの最大保存タイムアウトを3倍にする必要があります (たとえば、最大保存タイムアウトが60秒の場合、プラットフォームは180秒待機します)。 操作がその間隔よりも時間がかかる場合、プラットフォームは操作を中止し、関数固有のエラーコード 1 (操作がタイムアウトしました) で戻ります。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






