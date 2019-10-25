---
title: KSK プロパティ\_MEDIASEEKING\_使用可能
description: KSK プロパティ\_MEDIASEEKING\_AVAILABLE プロパティは、現在フィルターで使用できるメディアの時間間隔を取得します。
ms.assetid: df59f32e-2783-418d-85b9-f9285034c6fa
keywords:
- KSPROPERTY_MEDIASEEKING_AVAILABLE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_AVAILABLE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce2b9c599d75605a9462e5190bc27c6b29afcbde
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827278"
---
# <a name="ksproperty_mediaseeking_available"></a>KSK プロパティ\_MEDIASEEKING\_使用可能


KSK プロパティ\_MEDIASEEKING\_AVAILABLE プロパティは、現在フィルターで使用できるメディアの時間間隔を取得します。

## <span id="ddk_ksproperty_mediaseeking_available_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_AVAILABLE_KS"></span>


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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_mediaavailable" data-raw-source="[&lt;strong&gt;KSPROPERTY_MEDIAAVAILABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_mediaavailable)"><strong>KSPROPERTY_MEDIAAVAILABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

メディアの期間は、クライアントがシークできる期間です。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSK プロパティ\_MEDIAAVAILABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_mediaavailable)

[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






