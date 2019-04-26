---
title: ビデオ デコーダーのプロパティ
description: ビデオ デコーダーのプロパティ
ms.assetid: 671a310b-52a6-49f0-8848-e586a37c25ff
keywords:
- ビデオ デコーダー プロパティ WDK ビデオのキャプチャします。
- デコーダーの WDK ビデオのプロパティをキャプチャします。
- PROPSETID_VIDCAP_VIDEODECODER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62a471ae2898091949e46f8652bc2adeb208e066
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359618"
---
# <a name="video-decoder-properties"></a>ビデオ デコーダーのプロパティ


[PROPSETID\_しました\_VIDEODECODER](https://msdn.microsoft.com/library/windows/hardware/ff568121)プロパティ セットには、標準や時間の送信通知などのアナログ ビデオ デコーダーのデバイスの操作に関連するプロパティが含まれます。 次の表に、プロパティ、PROPSETID の一部である\_しました\_VIDEODECODER プロパティ セット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_VIDEODECODER KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566046" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566046)"><strong>KSPROPERTY_VIDEODECODER_CAPS</strong></a></p></td>
<td><p>時間のうちは落ち着かないのビデオ デコーダーなどのデバイス標準信号 (NTSC、PAL、SECAM) の機能情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566058" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STANDARD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566058)"><strong>KSPROPERTY_VIDEODECODER_STANDARD</strong></a></p></td>
<td><p>現在のアナログ ビデオ標準を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566060" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566060)"><strong>KSPROPERTY_VIDEODECODER_STATUS</strong></a></p></td>
<td><p>ビデオのビデオ信号内の行の数などのデバイスと、シグナルがロックされているかどうかをデコードの状態を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566051" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566051)"><strong>KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE</strong></a></p></td>
<td><p>ビデオのデコーダーの 3 つの状態の出力を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566062" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_VCR_TIMING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566062)"><strong>KSPROPERTY_VIDEODECODER_VCR_TIMING</strong></a></p></td>
<td><p>ビデオ デコーダーが VCR のタイミングまたはブロードキャストのタイミングを使用するかどうかを制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




