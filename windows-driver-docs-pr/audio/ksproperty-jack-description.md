---
title: KSK プロパティ\_ジャック\_の説明
description: KSK プロパティ\_JACK\_DESCRIPTION プロパティは、フィルターハンドルを介してアクセスされる複数項目のピン方向のプロパティとして実装されます。
ms.assetid: 005c7edc-8eb2-4387-b818-edef9b9dd4ee
keywords:
- KSPROPERTY_JACK_DESCRIPTION オーディオデバイス
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
ms.openlocfilehash: b3504ca472b418a5887be965bcd26bf909458e59
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830706"
---
# <a name="ksproperty_jack_description"></a>KSK プロパティ\_ジャック\_の説明


KSK プロパティ\_JACK\_DESCRIPTION プロパティは、フィルターハンドルを介してアクセスされる複数項目のピン方向のプロパティとして実装されます。

Windows Vista 以降では、このプロパティは、1つまたは複数の物理ジャックに関連付けられている任意のブリッジピンでサポートできます。 これは、特定のジャックの物理的な特性と使用法の説明を取得するために使用されます。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>Pin ファクトリ (フィルターハンドル経由)</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>の後に<a href="ksjack-description.md" data-raw-source="[&lt;strong&gt;KSJACK_DESCRIPTION&lt;/strong&gt;](ksjack-description.md)"><strong>KSJACK_DESCRIPTION</strong></a>構造体の配列</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (インスタンスデータ) は、KSMULTIPLE\_項目であり、その後に KSK ジャック\_DESCRIPTION 構造体の配列が続きます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_JACK\_DESCRIPTION プロパティ要求では、KSK の複数の\_項目の後に*N 個*の ksproperty\_説明の構造体の配列が返されます。ここで、 *n* = 指定したブリッジピンに関連付けられているジャックの数です。 このため、プロパティ要求によって返されるメンバーは次のようになります。

KSMULTIPLE\_項目。Size = sizeof (KSMULTIPLE\_ITEM) + N \* sizeof (KSK ジャック\_DESCRIPTION)

KSMULTIPLE\_項目。カウント = N

KSJACK\_DESCRIPTION\[0\]

...

KSJACK\_DESCRIPTION\[N-1\]

<a name="remarks"></a>注釈
-------

各 KSK ジャック\_DESCRIPTION 構造体には、1つのジャックに関する情報が必要です。 たとえば、3つのステレオジャックで5.1 オーディオをサポートする出力ブリッジピンは、サイズのデータバッファーを必要とします。

sizeof (KSMULTIPLE\_ITEM) + 3 \* sizeof (KSK ジャック\_DESCRIPTION)

また、各 KSK ジャック\_DESCRIPTION 構造体には、2ビットの ChannelMapping 値があります。

<a name="requirements"></a>要件
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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSJACK\_の説明**](ksjack-description.md)

[KSMULTIPLE\_項目](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






