---
title: KSK プロパティ\_VPCONFIG\_VPDATAINFO
description: KSK プロパティ\_VPCONFIG\_VPDATAINFO プロパティは、ビデオポートの初期構成の状態を示します。
ms.assetid: 66419d5a-c701-45f4-9ac6-322997e2f000
keywords:
- KSPROPERTY_VPCONFIG_VPDATAINFO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_VPDATAINFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a99d0ee32321ecfacf6c58547d824226562bed12
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823604"
---
# <a name="ksproperty_vpconfig_vpdatainfo"></a>KSK プロパティ\_VPCONFIG\_VPDATAINFO


KSK プロパティ\_VPCONFIG\_VPDATAINFO プロパティは、ビデオポートの初期構成の状態を示します。

## <span id="ddk_ksproperty_vpconfig_vpdatainfo_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_VPDATAINFO_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_amvpdatainfo" data-raw-source="[&lt;strong&gt;KS_AMVPDATAINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_amvpdatainfo)"><strong>KS_AMVPDATAINFO</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ビデオポートのプロパティを記述する KS\_AMVPDATAINFO 構造体です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KS\_AMVPDATAINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_amvpdatainfo)

 

 






