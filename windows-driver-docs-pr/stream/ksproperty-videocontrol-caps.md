---
title: KSPROPERTY\_VIDEOCONTROL\_キャップ
description: KSPROPERTY\_VIDEOCONTROL\_CAPS プロパティは、デバイスのビデオ コントロールの機能を識別します。 このプロパティを実装する必要があります。
ms.assetid: 5861ae38-3253-4546-bd9f-975f98e9e3f4
keywords:
- KSPROPERTY_VIDEOCONTROL_CAPS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbae7147b2f69cf8adc3fb5c2d26fcdb39b1dec6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552785"
---
# <a name="kspropertyvideocontrolcaps"></a>KSPROPERTY\_VIDEOCONTROL\_キャップ


KSPROPERTY\_VIDEOCONTROL\_CAPS プロパティは、デバイスのビデオ コントロールの機能を識別します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videocontrol_caps_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_CAPS_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566036" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566036)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566036" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566036)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_VIDEOCONTROL\_CAP\_構造をイメージの回転、または機能をトリガーするイベントなど、ミニドライバーのビデオ コントロールの機能を指定します。

<a name="remarks"></a>注釈
-------

**VideoControlCaps** 、KSPROPERTY のメンバー\_VIDEOCONTROL\_CAP\_S 構造体をデバイスのビデオ コントロールの機能を指定します。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOCONTROL\_CAP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566036)

 

 






