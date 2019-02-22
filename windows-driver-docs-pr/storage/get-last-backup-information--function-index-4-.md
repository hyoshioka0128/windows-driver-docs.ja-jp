---
title: 最後のバックアップ情報 (関数インデックス 4) を取得します。
description: この関数は、保存されたイメージに関する情報を返します。
ms.assetid: F73A763B-4A4A-4CAB-AA62-AFA79849884B
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 76b0e061c53f230e4ba6905a81d69226236bcd30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558089"
---
# <a name="get-last-backup-information-function-index-4"></a>最後のバックアップ情報 (関数インデックス 4) を取得します。


この関数は、保存されたイメージに関する情報を返します。

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
<td align="left"><strong>トリガー情報</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>に関する情報が存在しないかどうかは、非揮発性メモリ サブシステムと保存のトリガーのソースに保存されている有効な DRAM イメージ操作。</p>
<p><em>バイト 0 – <em>CSAVE_INFO0</em> (0, 0x80)</p>
<p>1 – バイトに予約されています。</p>
<p>2 – バイトに予約されています。</p>
<p>3 – バイトに予約されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>エラーに関する情報を保存します。</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>エラー情報の保存操作。</p>
<p></em>バイト 0 – <em>CSAVE_FAIL_INFO0</em> (0, 0x84)</p>
<p>* バイト 1 – <em>CSAVE_FAIL_INFO1</em> (0, 0x85)</p>
<p>2 – バイトに予約されています。</p>
<p>3 – バイトに予約されています。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






