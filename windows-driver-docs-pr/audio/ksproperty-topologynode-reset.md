---
title: KSK プロパティ\_TOPOLOGYNODE\_リセット
description: KSK プロパティ\_TOPOLOGYNODE\_RESET プロパティは、ノードを完全にリセットし、初期状態に復元します。
ms.assetid: c7558518-53c5-43c6-94ac-107823e2a0ab
keywords:
- KSPROPERTY_TOPOLOGYNODE_RESET オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGYNODE_RESET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24185f1be1f84a274ec132630049b0398f7e88ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832677"
---
# <a name="ksproperty_topologynode_reset"></a>KSK プロパティ\_TOPOLOGYNODE\_リセット


KSK プロパティ\_TOPOLOGYNODE\_RESET プロパティは、ノードを完全にリセットし、初期状態に復元します。

## <span id="ddk_ksproperty_topologynode_reset_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGYNODE_RESET_KS"></span>


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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) はブール型で、ノードをリセットする必要があるかどうかを示します。 値を**TRUE**に設定すると、ノードは作成時に既定の初期状態にリセットされます。 値を**FALSE**に設定しても効果はありませんが、エラーとして扱うことはできません。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_TOPOLOGYNODE\_RESET property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Microsoft Windows XP 以降のオペレーティングシステムでサポートされています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

 

 






