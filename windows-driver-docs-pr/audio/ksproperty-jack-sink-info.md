---
title: KSK プロパティ\_ジャック\_シンク\_情報
description: KSK プロパティ\_ジャック\_シンク\_INFO プロパティは、フィルターハンドルを使用してアクセスされるピン方向のプロパティとして実装されます。
ms.assetid: a51c03fa-91e4-49f2-ad76-35133c3b09ba
keywords:
- KSPROPERTY_JACK_SINK_INFO オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_SINK_INFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 855d5c862dd43a3cca61a8a5365b9b991b35ad76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832725"
---
# <a name="ksproperty_jack_sink_info"></a>KSK プロパティ\_ジャック\_シンク\_情報


KSK プロパティ\_ジャック\_シンク\_INFO プロパティは、フィルターハンドルを使用してアクセスされるピン方向のプロパティとして実装されます。

Windows 7 以降のオペレーティングシステムでは、このプロパティは、1つまたは複数の物理ジャックに関連付けられている任意のブリッジピンでサポートできます。 KSK プロパティ\_ジャック\_シンク\_情報は、ディスプレイ関連のデジタルオーディオデバイス (HDMI デバイス、ディスプレイポートなど) のジャックシンクの説明と機能を取得するために使用されます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksjack_sink_information" data-raw-source="[&lt;strong&gt;KSJACK_SINK_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksjack_sink_information)"><strong>KSJACK_SINK_INFORMATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (インスタンスデータ) は、\_シンク\_詳細構造体である KSK ジャックです。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_ジャック\_シンク\_INFO プロパティ要求では、 **Ksk ジャック\_シンク\_情報**構造体に情報が返されます。

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


[**KSK ジャック\_シンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksjack_sink_information)

 

 






