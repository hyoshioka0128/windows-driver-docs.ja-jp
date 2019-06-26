---
title: KSPROPERTY\_VIDEOCONTROL\_実際\_フレーム\_率
description: KSPROPERTY\_VIDEOCONTROL\_実際\_フレーム\_レート プロパティをデバイスは、指定した pin のストリーミング、フレーム レートを取得します。 このプロパティは省略可能です。
ms.assetid: 1681bb54-bdd8-499d-b544-c0e8b14deaa5
keywords:
- KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE ストリーミング メディア デバイス
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
ms.openlocfilehash: f532dffb1fe49e53575459f2a19c71bfc0d3a07e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355919"
---
# <a name="kspropertyvideocontrolactualframerate"></a>KSPROPERTY\_VIDEOCONTROL\_実際\_フレーム\_率


KSPROPERTY\_VIDEOCONTROL\_実際\_フレーム\_レート プロパティをデバイスは、指定した pin のストリーミング、フレーム レートを取得します。 このプロパティは省略可能です。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S</strong></a></p></td>
<td><p>KSPROPERTY_VIDEOCONTROL</p>
<p>_ACTUAL_FRAME_RATE_S</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_VIDEOCONTROL\_実際\_フレーム\_レート\_構造など、クエリ時に実際のフレーム レート情報を指定する、ディメンション (幅と高さ) のイメージ、現在の実際のフレーム レート、および現在の最大使用可能なフレーム レート

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOCONTROL\_実際\_フレーム\_レート\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)

 

 






