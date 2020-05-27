---
title: NVM イメージの消去 (関数インデックス 19)
description: この関数は、不揮発性メモリモジュールに保存されているバックアップイメージを消去します。
ms.assetid: D2856D56-413F-4444-9CDF-C42ACA3CFBA0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c28dffb4c037ab4c24dfef4db7c57cdcf5cfd76c
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851703"
---
# <a name="erase-nvm-image-function-index-19"></a>NVM イメージの消去 (関数インデックス 19)


この関数は、不揮発性メモリモジュールに保存されているバックアップイメージを消去します。

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
<td align="left"><p>この関数は、次の関数固有のエラーコードを返すことができます。</p>
<p>1: 操作がタイムアウトしました。</p>
<p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>に関するページを参照してください。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> これは同期関数です。 このメソッドは、消去操作が完了またはタイムアウトした場合にのみを返します。操作が、 \* *erase \_ TIMEOUT0* (0, 0x1e) と erase TIMEOUT1 (0, 0x1f) で定義されたタイムアウトよりも時間がかかる場合、 \* * \_ *プラットフォームは制御が戻る前に、この関数を中止する必要があります。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






