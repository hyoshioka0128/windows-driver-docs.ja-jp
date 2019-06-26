---
title: KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_プロパティ
description: ユーザー モードのクライアントでは、このプロパティを使用して、カメラのイメージの暗証番号 (pin) とレコードの暗証番号 (pin) は相互に排他的であるかどうかを識別します。 相互に排他的な場合は、し、レコードの暗証番号 (pin) がアクティブなときイメージ ピン留めすることはできませんアクティブ、およびその逆です。
ms.assetid: 4D000551-3AFB-4E14-9C67-EEDAB676AE03
keywords:
- KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_PROPERTY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec1f02ea1e8f1d72fd0e4b616647e80240d63b43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353249"
---
# <a name="kspropertycameracontrolimagepincapabilityproperty"></a>KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_プロパティ


ユーザー モードのクライアントでは、このプロパティを使用して、カメラのイメージの暗証番号 (pin) とレコードの暗証番号 (pin) は相互に排他的であるかどうかを識別します。 相互に排他的な場合は、し、レコードの暗証番号 (pin) がアクティブなときイメージ ピン留めすることはできませんアクティブ、およびその逆です。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)"><strong>KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_S</strong></a></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ドライバーは、このプロパティを実装し、イメージの暗証番号 (pin) は、レコードの暗証番号 (pin) と排他的ことを識別する場合、メディア ストリーミング パイプラインから記録が行われている間は、ドライバーに送信される「take photo」コマンドができなくなります。

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)

 

 






