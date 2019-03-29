---
title: NVM イメージの消去 (関数インデックス 19)
description: この関数は、非揮発性メモリ モジュールで保存されたバックアップ イメージを消去します。
ms.assetid: D2856D56-413F-4444-9CDF-C42ACA3CFBA0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6aa3c424bbac28f25e2836b3e7b87dbecd96b70d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580835"
---
# <a name="erase-nvm-image-function-index-19"></a>NVM イメージの消去 (関数インデックス 19)


この関数は、非揮発性メモリ モジュールで保存されたバックアップ イメージを消去します。

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
<td align="left"><p>この関数は、次の関数に固有のエラー コードを返すことができます。</p>
<p>1:操作がタイムアウトになりました。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!注\]    &gt;これは、同期関数。 消去操作が完了またはタイムアウト時にのみを返します。操作で定義されているタイムアウトより長くかかる場合\**消去\_TIMEOUT0* (0, 0x1E) と\**消去\_TIMEOUT1* (0, 0x1F)、返す前に、プラットフォームはこの関数が中止されます。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






