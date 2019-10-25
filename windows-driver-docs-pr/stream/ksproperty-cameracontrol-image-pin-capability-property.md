---
title: KSK プロパティ\_CAMERACONTROL\_IMAGE\_PIN\_機能\_プロパティ
description: ユーザーモードのクライアントは、このプロパティを使用して、カメラのイメージの pin とレコードの pin が相互に排他的であるかどうかを識別します。 相互に排他的な場合、レコードの pin がアクティブである場合は、イメージの pin をアクティブにすることはできません。また、その逆も可能です。
ms.assetid: 4D000551-3AFB-4E14-9C67-EEDAB676AE03
keywords:
- KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_PROPERTY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8be1fd4d349f96ac03af3299b52dca2d6806512d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843350"
---
# <a name="ksproperty_cameracontrol_image_pin_capability_property"></a>KSK プロパティ\_CAMERACONTROL\_IMAGE\_PIN\_機能\_プロパティ


ユーザーモードのクライアントは、このプロパティを使用して、カメラのイメージの pin とレコードの pin が相互に排他的であるかどうかを識別します。 相互に排他的な場合、レコードの pin がアクティブである場合は、イメージの pin をアクティブにすることはできません。また、その逆も可能です。

## <span id="ddk_ksproperty_cameracontrol_pan_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PAN_KS"></span>


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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)"><strong>KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_S</strong></a></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ドライバーがこのプロパティを実装し、画像の pin がレコードピンと排他的であることを識別する場合、メディアストリーミングパイプラインは、録音中に "写真の撮影" コマンドがドライバーに送信されないようにします。

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_CAMERACONTROL\_IMAGE\_PIN\_機能\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)

 

 






