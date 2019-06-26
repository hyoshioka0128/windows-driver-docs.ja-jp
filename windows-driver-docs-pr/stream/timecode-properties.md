---
title: タイムコードのプロパティ
description: タイムコードのプロパティ
ms.assetid: e8359778-8cc6-4f19-b869-f9597dae0502
keywords:
- タイムコード プロパティ WDK ビデオのキャプチャします。
- PROPSETID_TIMECODE_READER
- テープのタイムコード プロパティ WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8c5420e648bfd3217caecdfee07e5d877341cd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377736"
---
# <a name="timecode-properties"></a>タイムコードのプロパティ


[PROPSETID\_タイムコード\_リーダー](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-timecode-reader)タイムコード DVHS のテープ デッキや MiniDV ビデオ_カメラなどのテープ上に関連するプロパティがプロパティ セットに含まれています。 次の表に、プロパティ、PROPSETID の一部である\_タイムコード\_リーダー プロパティのセット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_TIMECODE_READER KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-timecode-reader" data-raw-source="[&lt;strong&gt;KSPROPERTY_TIMECODE_READER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-timecode-reader)"><strong>KSPROPERTY_TIMECODE_READER</strong></a></p></td>
<td><p>現在のテープの位置のタイムコードを返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-atn-reader" data-raw-source="[&lt;strong&gt;KSPROPERTY_ATN_READER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-atn-reader)"><strong>KSPROPERTY_ATN_READER</strong></a></p></td>
<td><p>現在のテープの位置の絶対トラック数を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-rtc-reader" data-raw-source="[&lt;strong&gt;KSPROPERTY_RTC_READER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-rtc-reader)"><strong>KSPROPERTY_RTC_READER</strong></a></p></td>
<td><p>現在のテープの位置の相対時間カウンターを返します。</p></td>
</tr>
</tbody>
</table>

 

 

 




