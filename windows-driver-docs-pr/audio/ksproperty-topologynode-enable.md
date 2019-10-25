---
title: KSK プロパティ\_TOPOLOGYNODE\_ENABLE
description: KSK プロパティ\_TOPOLOGYNODE\_ENABLE プロパティは、既に構築されているトポロジでトポロジノードをオンまたはオフにするために使用されます。
ms.assetid: 6b9f7a92-97dc-476b-962a-40ccf1987154
keywords:
- KSPROPERTY_TOPOLOGYNODE_ENABLE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGYNODE_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63edfc77bd25a68c2c6b7e4d3dacc15346ca7286
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830475"
---
# <a name="ksproperty_topologynode_enable"></a>KSK プロパティ\_TOPOLOGYNODE\_ENABLE


KSK プロパティ\_TOPOLOGYNODE\_ENABLE プロパティは、既に構築されているトポロジでトポロジノードをオンまたはオフにするために使用されます。

## <span id="ddk_ksproperty_topologynode_enable_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGYNODE_ENABLE_KS"></span>


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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は BOOL で、ノードの電源をオンまたはオフにするかどうかを指定します。 値が**TRUE の場合**は、ノードがオンになっていることを示します。 **FALSE**は、ノードがオフになっていることを示します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

TOPOLOGYNODE を有効にした KSK プロパティ\_\_プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

既に有効になっているノードを有効にしたり、既に無効になっているノードを無効にしても効果はありませんが、エラーとして処理しないでください。

ノードを無効にすると、ノードを通過するストリームでノードが実行する変換がオフになります。 AEC、AGC、またはノイズ抑制ノード ([**KSNODETYPE\_音響\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)、 [**KSNODETYPE\_agc**](ksnodetype-agc.md)、または[**KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md)) の場合 (無効になっているノードなど)パススルーモードで動作します (つまり、ノードの入力ピンから出力ピンにフローするため、ストリームに対して操作が実行されません)。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_音響\_ECHO\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_AGC**](ksnodetype-agc.md)

[**KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md)

 

 






