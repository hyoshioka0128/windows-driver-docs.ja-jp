---
title: KSK プロパティ\_WAVE\_ボリューム
description: KSK プロパティ\_WAVE\_VOLUME プロパティは、wave デバイスのボリューム設定を指定します。
ms.assetid: c5725f7d-b965-43f3-9c49-faff82d99580
keywords:
- KSPROPERTY_WAVE_VOLUME ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_VOLUME
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0081da607e0195d901198d8d2a332033100624fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845547"
---
# <a name="ksproperty_wave_volume"></a>KSK プロパティ\_WAVE\_ボリューム


KSK プロパティ\_WAVE\_VOLUME プロパティは、wave デバイスのボリューム設定を指定します。

## <span id="ddk_ksproperty_wave_volume_ks"></span><span id="DDK_KSPROPERTY_WAVE_VOLUME_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_volume" data-raw-source="[&lt;strong&gt;KSWAVE_VOLUME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_volume)"><strong>KSWAVE_VOLUME</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、左と右の減衰の量を表す KSWAVE\_ボリューム構造です。

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

[**KSWAVE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_volume)

 

 






