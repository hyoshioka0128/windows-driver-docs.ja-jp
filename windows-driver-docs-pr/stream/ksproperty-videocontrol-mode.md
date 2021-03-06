---
title: KSPROPERTY\_VIDEOCONTROL\_モード
description: KSPROPERTY\_VIDEOCONTROL\_モード プロパティは、イメージの運用環境のモードを制御します。 これには、反転、および外部のトリガーによってフレームのキャプチャを有効にすると、水平および垂直のイメージの設定が含まれます。 このプロパティは省略可能です。
ms.assetid: b101b348-cfd4-46a1-857a-9e7cb3f35ce5
keywords:
- KSPROPERTY_VIDEOCONTROL_MODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7662129557b64a9988d250eec45c4a9e5426e8dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381997"
---
# <a name="kspropertyvideocontrolmode"></a>KSPROPERTY\_VIDEOCONTROL\_モード


KSPROPERTY\_VIDEOCONTROL\_モード プロパティは、イメージの運用環境のモードを制御します。 これには、反転、および外部のトリガーによってフレームのキャプチャを有効にすると、水平および垂直のイメージの設定が含まれます。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videocontrol_mode_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_MODE_KS"></span>


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
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s)"><strong>KSPROPERTY_VIDEOCONTROL_MODE_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s)"><strong>KSPROPERTY_VIDEOCONTROL_MODE_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_VIDEOCONTROL\_CAP\_構造をイメージの回転、または機能をトリガーするイベントなど、ミニドライバーのビデオ コントロールの機能を指定します。

<a name="remarks"></a>注釈
-------

**モード**、KSPROPERTY のメンバー\_VIDEOCONTROL\_モード\_の構造は、ビデオ コントロールのモードを指定します。

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

[**KSPROPERTY\_VIDEOCONTROL\_モード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s)

 

 






