---
title: ビデオ処理アンプのプロパティ
description: ビデオ処理アンプのプロパティ
ms.assetid: 1adc4fcc-c9a2-41a8-90db-1030ba7c257f
keywords:
- ビデオの処理アンプ プロパティ WDK ビデオ キャプチャ
- 増幅プロパティ WDK ビデオのキャプチャします。
- 彩度 WDK ビデオ キャプチャ
- コントラスト WDK ビデオ キャプチャ
- hue WDK ビデオ キャプチャ
- PROPSETID_VIDCAP_VIDEOPROCAMP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb01ffe1d21a54b6a3aa86b9771d341df1ae069d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385371"
---
# <a name="video-processing-amplifier-properties"></a>ビデオ処理アンプのプロパティ


[PROPSETID\_しました\_ビデオ プロシージャ アンプ](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)プロパティ セットには、ビデオ、対照的に、hue を含むビデオの属性の増幅を処理および彩度に関連するプロパティが含まれています。 次の表に、プロパティ、PROPSETID の一部である\_しました\_VIDOPROCAMP プロパティ セット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_VIDEOPROCAMP KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-backlight-compensation" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-backlight-compensation)"><strong>KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION</strong></a></p></td>
<td><p>カメラのバックライトの報酬が設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-brightness" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-brightness)"><strong>KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS</strong></a></p></td>
<td><p>カメラの明るさを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-colorenable" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_COLORENABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-colorenable)"><strong>KSPROPERTY_VIDEOPROCAMP_COLORENABLE</strong></a></p></td>
<td><p>カメラの色を使用する設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-contrast" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_CONTRAST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-contrast)"><strong>KSPROPERTY_VIDEOPROCAMP_CONTRAST</strong></a></p></td>
<td><p>カメラの明るさの設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-gamma" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_GAMMA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-gamma)"><strong>KSPROPERTY_VIDEOPROCAMP_GAMMA</strong></a></p></td>
<td><p>カメラの色域の設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-hue" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_HUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-hue)"><strong>KSPROPERTY_VIDEOPROCAMP_HUE</strong></a></p></td>
<td><p>カメラの hue の設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-saturation" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_SATURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-saturation)"><strong>KSPROPERTY_VIDEOPROCAMP_SATURATION</strong></a></p></td>
<td><p>カメラのクロミナンスの設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-sharpness" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_SHARPNESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-sharpness)"><strong>KSPROPERTY_VIDEOPROCAMP_SHARPNESS</strong></a></p></td>
<td><p>カメラの鮮明度の設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-whitebalance" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-whitebalance)"><strong>KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE</strong></a></p></td>
<td><p>ホワイト バランスのカメラの設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-gain" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_GAIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-gain)"><strong>KSPROPERTY_VIDEOPROCAMP_GAIN</strong></a></p></td>
<td><p>カメラのコントロールは、設定を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-digital-multiplier" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-digital-multiplier)"><strong>KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER</strong></a></p></td>
<td><p>カメラのデジタル ズームの乗数を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-digital-multiplier-limit" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-digital-multiplier-limit)"><strong>KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT</strong></a></p></td>
<td><p>カメラのデジタル ズームの上限を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-whitebalance-component" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-whitebalance-component)"><strong>KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT</strong></a></p></td>
<td><p>ホワイト バランスのカメラの設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-powerline-frequency" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-powerline-frequency)"><strong>KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY</strong></a></p></td>
<td><p>カメラの運用環境の powerline 頻度を制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




