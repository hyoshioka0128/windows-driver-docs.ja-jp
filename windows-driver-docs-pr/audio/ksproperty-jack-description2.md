---
title: KSK プロパティ\_ジャック\_DESCRIPTION2
description: KSK プロパティ\_JACK\_DESCRIPTION2 プロパティは、フィルターハンドルを使用してアクセスされるピン方向のプロパティとして実装されます。
ms.assetid: 6856060b-f735-4ed8-99bd-5896c87d581f
keywords:
- KSPROPERTY_JACK_DESCRIPTION2 オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_DESCRIPTION2
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3aa9daee2bb2008b7822bb0cab72a3582c2c5849
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832727"
---
# <a name="ksproperty_jack_description2"></a>KSK プロパティ\_ジャック\_DESCRIPTION2


KSK プロパティ\_JACK\_DESCRIPTION2 プロパティは、フィルターハンドルを使用してアクセスされるピン方向のプロパティとして実装されます。

Windows 7 以降の Windows オペレーティングシステムでは、このプロパティは、1つまたは複数の物理ジャックに関連付けられている任意のブリッジピンでサポートできます。 KSK プロパティ\_ジャック\_DESCRIPTION2 を使用して、デバイスの状態とジャック関連の機能を取得します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>の後に<a href="ksjack-description2.md" data-raw-source="[&lt;strong&gt;KSJACK_DESCRIPTION2&lt;/strong&gt;](ksjack-description2.md)"><strong>KSJACK_DESCRIPTION2</strong></a>構造体の配列</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (インスタンスデータ) は、KSMULTIPLE\_項目であり、その後に KSK ジャック\_DESCRIPTION2 構造体の配列が続きます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_JACK\_DESCRIPTION2 property 要求では、KSK の複数の\_項目の後に*N* ksk\_ジャックの配列が返されます ( *n* = 指定されたに関連付けられているジャックの数)。ブリッジ pin。 次の一覧は、プロパティ要求によって返される項目を示しています。

KSMULTIPLE\_項目。Size = sizeof (KSMULTIPLE\_ITEM) + N \* sizeof (KSK ジャック\_DESCRIPTION2)

KSMULTIPLE\_項目。カウント = N

KSJACK\_DESCRIPTION2\[0\]

...

KSJACK\_DESCRIPTION2\[N-1\]

<a name="remarks"></a>注釈
-------

各 KSK ジャック\_DESCRIPTION2 構造体には、1つのジャックに関する情報のみを含める必要があります。

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
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSJACK\_DESCRIPTION2**](ksjack-description2.md)

[KSMULTIPLE\_項目](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

 






