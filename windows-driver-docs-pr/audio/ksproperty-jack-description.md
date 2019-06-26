---
title: KSPROPERTY\_ジャック\_の説明
description: KSPROPERTY\_ジャック\_DESCRIPTION プロパティがフィルター ハンドル経由でアクセスする複数の項目、pin-wise プロパティとして実装されます。
ms.assetid: 005c7edc-8eb2-4387-b818-edef9b9dd4ee
keywords:
- KSPROPERTY_JACK_DESCRIPTION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_DESCRIPTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c09565b3821b6b6850f9f2643645e5f822d0b153
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360522"
---
# <a name="kspropertyjackdescription"></a>KSPROPERTY\_ジャック\_の説明


KSPROPERTY\_ジャック\_DESCRIPTION プロパティがフィルター ハンドル経由でアクセスする複数の項目、pin-wise プロパティとして実装されます。

Windows Vista 以降では、このプロパティは、1 つまたは複数の物理ジャックに関連付けられているブリッジ暗証番号 (pin) をサポートできます。 これを使用して、物理的な特性の説明と、特定のジャックの使用状況を取得します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>(フィルターのハンドル) を使用してファクトリをピン留めします。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong> </a>の配列を続けて<a href="ksjack-description.md" data-raw-source="[&lt;strong&gt;KSJACK_DESCRIPTION&lt;/strong&gt;](ksjack-description.md)"> <strong>KSJACK_DESCRIPTION</strong> </a>構造体</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (インスタンス データ) は、KSMULTIPLE\_KSJACK の配列で\_構造を説明します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_ジャック\_説明プロパティ要求が、KSMULTIPLE を返します\_項目配列の後に*N* KSJACK\_構造体の説明、場所*N* = 指定したブリッジの暗証番号 (pin) に関連付けられているジャックの数。 プロパティ要求によって返されるメンバーはそのためのようになります。

KSMULTIPLE\_項目。サイズ = sizeof (KSMULTIPLE\_項目) + N \* sizeof (KSJACK\_説明)

KSMULTIPLE\_ITEM.Count = N

KSJACK\_説明\[0\]

...

KSJACK\_説明\[N-1\]

<a name="remarks"></a>注釈
-------

各 KSJACK\_構造の説明については 1 つのジャック必要があります。 たとえば、5.1 オーディオ 3 つのステレオ ジャックをサポートする出力ブリッジ pin が必要になりますデータ バッファーのサイズ

sizeof (KSMULTIPLE\_項目) + 3 \* sizeof (KSJACK\_説明)

各 KSJACK\_two-bit ChannelMapping 値構造体の説明が必要があります。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows Vista</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSJACK\_の説明**](ksjack-description.md)

[KSMULTIPLE\_項目](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)

[KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






