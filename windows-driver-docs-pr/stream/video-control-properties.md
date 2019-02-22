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
ms.openlocfilehash: 5bcf8a47ebf325b6a99e27dbc5a2d83179e64d33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531369"
---
# <a name="video-control-properties"></a>ビデオ コントロールのプロパティ


[PROPSETID\_しました\_VIDEOCONTROL](https://msdn.microsoft.com/library/windows/hardware/ff568120)コントロールとビデオ ハードウェアの機能に関連するプロパティがプロパティ セットに含まれていますにハードウェアをキャプチャできるなど、使用可能なフレーム レートをビデオのイメージの向き。 次の表に、プロパティ、PROPSETID の一部である\_しました\_VIDEOCONTROL プロパティ セット。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566035" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566035)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS</strong></a></p></td>
<td><p>イメージの向きと、ストリームからのビデオのフレームの取得をトリガーするなど、ビデオ ストリームの機能情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566024" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566024)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE</strong></a></p></td>
<td><p>ハードウェアが特定の暗証番号 (pin) のビデオをストリーミングする実際のフレーム レートを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566040" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566040)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES</strong></a></p></td>
<td><p>ビデオのストリーミングを実行できるデバイスを使用可能なフレーム レートの数を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566042" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566042)"><strong>KSPROPERTY_VIDEOCONTROL_MODE</strong></a></p></td>
<td><p>イメージを反転し、ストリームからのビデオのフレームの取得を開始することなどのビデオ ストリームのモードを制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




