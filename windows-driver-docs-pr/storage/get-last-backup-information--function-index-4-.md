---
title: 最終バックアップ情報の取得 (関数インデックス 4)
description: この関数は、保存されたイメージに関する情報を返します。
ms.assetid: F73A763B-4A4A-4CAB-AA62-AFA79849884B
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 325b1f75ae1c4ae3f030224d38257f3ce397f913
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851361"
---
# <a name="get-last-backup-information-function-index-4"></a>最終バックアップ情報の取得 (関数インデックス 4)


この関数は、保存されたイメージに関する情報を返します。

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
<td align="left"><strong>トリガー情報</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>不揮発性メモリサブシステムおよび保存操作のトリガーソースに保存されている有効な DRAM イメージがあるかどうかに関する情報。</p>
<p><em>バイト0– <em>CSAVE_INFO0</em> (0, 0x80)</p>
<p>バイト1–予約済み。</p>
<p>バイト2–予約済み。</p>
<p>バイト3–予約済み。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>エラー情報の保存</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>保存操作の失敗情報。</p>
<p></em>バイト0– <em>CSAVE_FAIL_INFO0</em> (0、0x84)</p>
<p>* バイト1– <em>CSAVE_FAIL_INFO1</em> (0、0x85)</p>
<p>バイト2–予約済み。</p>
<p>バイト3–予約済み。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






