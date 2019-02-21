---
title: メモリ エラー カウンター (関数インデックス 31) の設定します。
description: この関数は、呼び出し元が指定した値を修正し、修正不可能なメモリ エラーのイベントを追跡するカウンターを設定します。 この関数では、ソフトウェアの検証を有効にします。
ms.assetid: 0EC4B442-902B-4589-A831-9637F4D60F86
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 60d21eb2395e2ccdac11ec39b1f71c2044b74527
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532428"
---
# <a name="set-memory-error-counters-function-index-31"></a>メモリ エラー カウンター (関数インデックス 31) の設定します。


この関数は、呼び出し元が指定した値を修正し、修正不可能なメモリ エラーのイベントを追跡するカウンターを設定します。 この関数では、ソフトウェアの検証を有効にします。

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
<td align="left"><strong>DRAM ECC 修正不可能なエラーの数</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>NVDIMM-N モジュールから、プラットフォームによって検出不可能の ECC エラーの数。</p>
<p>プラットフォームは、この値を書き込みは、 <em> <em>DRAM_ECC_ERROR_COUNT</em> (2, 0x80) を登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>DRAM 修正可能な ECC エラーしきい値イベントの数</strong></td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left"><p>修正可能な ECC しきい値を超えましたイベント数、NVDIMM-N のモジュールから、プラットフォームによって検出されました。</p>
<p>プラットフォームは、この値を書き込みは、 <em></em> DRAM_THRESHOLD_ECC_COUNT</em> (2, 0x81) を登録します。</p></td>
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
<td align="left"><strong>状態</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NVDIMM-N の正常性の情報 (関数インデックス 11) を取得します。](get-nvdimm-n-health-info--function-index-11-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






