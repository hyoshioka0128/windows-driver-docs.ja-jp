---
title: KSK プロパティ\_VIDEOCONTROL\_モード
description: KSK プロパティ\_VIDEOCONTROL\_MODE プロパティは、イメージの運用モードを制御します。 これには、水平方向および垂直方向のイメージ反転の設定と、外部トリガーによるフレームキャプチャの有効化が含まれます。 このプロパティは省略可能です。
ms.assetid: b101b348-cfd4-46a1-857a-9e7cb3f35ce5
keywords:
- KSPROPERTY_VIDEOCONTROL_MODE ストリーミングメディアデバイス
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
ms.openlocfilehash: e4705f9bd290368b656bd3d08b4c25ace1dbc1d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837869"
---
# <a name="ksproperty_videocontrol_mode"></a>KSK プロパティ\_VIDEOCONTROL\_モード


KSK プロパティ\_VIDEOCONTROL\_MODE プロパティは、イメージの運用モードを制御します。 これには、水平方向および垂直方向のイメージ反転の設定と、外部トリガーによるフレームキャプチャの有効化が含まれます。 このプロパティは省略可能です。

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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s)"><strong>KSPROPERTY_VIDEOCONTROL_MODE_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s)"><strong>KSPROPERTY_VIDEOCONTROL_MODE_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ミニドライバーのビデオコントロール機能 (画像の反転やイベントトリガー機能など) を指定する、VIDEOCONTROL\_CAPS\_S 構造体\_KSK プロパティです。

<a name="remarks"></a>注釈
-------

KSK プロパティの**モード**メンバー\_videocontrol\_Mode\_S 構造体で、video control モードを指定します。

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

[**KSK プロパティ\_VIDEOCONTROL\_MODE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s)

 

 






