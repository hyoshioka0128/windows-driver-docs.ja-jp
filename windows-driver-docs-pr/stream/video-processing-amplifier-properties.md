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
ms.openlocfilehash: 84b178240c02f04a36a2f4381fcf9a4e6ba0570c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359609"
---
# <a name="video-processing-amplifier-properties"></a>ビデオ処理アンプのプロパティ


[PROPSETID\_しました\_ビデオ プロシージャ アンプ](https://msdn.microsoft.com/library/windows/hardware/ff568122)プロパティ セットには、ビデオ、対照的に、hue を含むビデオの属性の増幅を処理および彩度に関連するプロパティが含まれています。 次の表に、プロパティ、PROPSETID の一部である\_しました\_VIDOPROCAMP プロパティ セット。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566063" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566063)"><strong>KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION</strong></a></p></td>
<td><p>カメラのバックライトの報酬が設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566065" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566065)"><strong>KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS</strong></a></p></td>
<td><p>カメラの明るさを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566066" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_COLORENABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566066)"><strong>KSPROPERTY_VIDEOPROCAMP_COLORENABLE</strong></a></p></td>
<td><p>カメラの色を使用する設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566070" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_CONTRAST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566070)"><strong>KSPROPERTY_VIDEOPROCAMP_CONTRAST</strong></a></p></td>
<td><p>カメラの明るさの設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566076" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_GAMMA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566076)"><strong>KSPROPERTY_VIDEOPROCAMP_GAMMA</strong></a></p></td>
<td><p>カメラの色域の設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566078" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_HUE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566078)"><strong>KSPROPERTY_VIDEOPROCAMP_HUE</strong></a></p></td>
<td><p>カメラの hue の設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566092" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_SATURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566092)"><strong>KSPROPERTY_VIDEOPROCAMP_SATURATION</strong></a></p></td>
<td><p>カメラのクロミナンスの設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566093" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_SHARPNESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566093)"><strong>KSPROPERTY_VIDEOPROCAMP_SHARPNESS</strong></a></p></td>
<td><p>カメラの鮮明度の設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566095" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566095)"><strong>KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE</strong></a></p></td>
<td><p>ホワイト バランスのカメラの設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566074" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_GAIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566074)"><strong>KSPROPERTY_VIDEOPROCAMP_GAIN</strong></a></p></td>
<td><p>カメラのコントロールは、設定を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566071" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566071)"><strong>KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER</strong></a></p></td>
<td><p>カメラのデジタル ズームの乗数を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566072" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566072)"><strong>KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT</strong></a></p></td>
<td><p>カメラのデジタル ズームの上限を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566097" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566097)"><strong>KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT</strong></a></p></td>
<td><p>ホワイト バランスのカメラの設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566086" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566086)"><strong>KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY</strong></a></p></td>
<td><p>カメラの運用環境の powerline 頻度を制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




