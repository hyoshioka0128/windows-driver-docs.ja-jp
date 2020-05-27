---
title: NVDIMM-N の遮断 (関数インデックス 20)
description: この関数は、停電が発生した場合に、保存操作のために NVDIMM を遮断します。
ms.assetid: 15D21B5A-2320-4C22-9957-ECC0EB46B02E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4d390678148b220456423c06f90500ec57ae8407
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851475"
---
# <a name="span-idstoragearm_nvdimm-n__function_index_20_spanarm-nvdimm-n-function-index-20"></a><span id="storage.arm_nvdimm-n__function_index_20_"></span>NVDIMM-N の遮断 (関数インデックス 20)


この関数は、停電が発生した場合に、保存操作のために NVDIMM を遮断します。 プラットフォームは、適切な保存トリガーを選択する役割を担います。

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
<p>詳細については、<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Interface for Byte Addressable Energy Backed Function Class (Function Interface 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">バイトアドレッシング可能なエネルギー対応関数クラス (関数インターフェイス 1) の _DSM インターフェイス</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> これは同期関数です。 これは、arm 操作が完了またはタイムアウトした場合にのみを返します。操作が \* *arm \_ TIMEOUT0* (0, 0x20) と arm TIMEOUT1 (0, 0x21) で定義されているタイムアウトよりも時間がかかる場合、 \* * \_ *プラットフォームは制御が戻る前にこの関数を中止する必要があります。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






