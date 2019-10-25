---
title: KSK プロパティ\_VIDEOCONTROL\_実際の\_フレーム\_率
description: KSK プロパティ\_VIDEOCONTROL\_実際の\_フレーム\_レートプロパティは、指定されたピンのデバイスがストリーミングされるフレームレートを取得します。 このプロパティは省略可能です。
ms.assetid: 1681bb54-bdd8-499d-b544-c0e8b14deaa5
keywords:
- KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7abae78a5c39046d8a5c6146528c5b4689cf07f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837875"
---
# <a name="ksproperty_videocontrol_actual_frame_rate"></a>KSK プロパティ\_VIDEOCONTROL\_実際の\_フレーム\_率


KSK プロパティ\_VIDEOCONTROL\_実際の\_フレーム\_レートプロパティは、指定されたピンのデバイスがストリーミングされるフレームレートを取得します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videocontrol_actual_frame_rate_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S</strong></a></p></td>
<td><p>KSPROPERTY_VIDEOCONTROL</p>
<p>_ACTUAL_FRAME_RATE_S</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、\_VIDEOCONTROL\_実際のフレームレート情報を指定する、\_フレーム\_レート\_S 構造体です。これは、クエリの実行時に実際のフレームレート情報を指定します。たとえば、イメージ、現在の実際のフレームレート、および現在の最大使用可能なフレームレート。

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

[**KSK プロパティ\_VIDEOCONTROL\_実際の\_フレーム\_率\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)

 

 






