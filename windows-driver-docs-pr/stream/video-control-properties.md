---
title: ビデオ コントロールのプロパティ
description: ビデオ コントロールのプロパティ
ms.assetid: 3b39295f-b4fa-4d6a-bad8-f759bda284b1
keywords:
- ビデオ コントロール プロパティ WDK ビデオのキャプチャします。
- コントロールのプロパティの WDK ビデオ キャプチャ
- PROPSETID_VIDCAP_VIDEOCONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d86bca4979673244c4c10305fc96ce3b50abe419
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385377"
---
# <a name="video-control-properties"></a>ビデオ コントロールのプロパティ


[PROPSETID\_しました\_VIDEOCONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)コントロールとビデオ ハードウェアの機能に関連するプロパティがプロパティ セットに含まれていますにハードウェアをキャプチャできるなど、使用可能なフレーム レートをビデオのイメージの向き。 次の表に、プロパティ、PROPSETID の一部である\_しました\_VIDEOCONTROL プロパティ セット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_VIDEOCONTROL KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-caps)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS</strong></a></p></td>
<td><p>イメージの向きと、ストリームからのビデオのフレームの取得をトリガーするなど、ビデオ ストリームの機能情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-actual-frame-rate" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-actual-frame-rate)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE</strong></a></p></td>
<td><p>ハードウェアが特定の暗証番号 (pin) のビデオをストリーミングする実際のフレーム レートを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-frame-rates" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-frame-rates)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES</strong></a></p></td>
<td><p>ビデオのストリーミングを実行できるデバイスを使用可能なフレーム レートの数を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-mode)"><strong>KSPROPERTY_VIDEOCONTROL_MODE</strong></a></p></td>
<td><p>イメージを反転し、ストリームからのビデオのフレームの取得を開始することなどのビデオ ストリームのモードを制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




