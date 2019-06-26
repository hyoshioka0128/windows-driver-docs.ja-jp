---
title: チューナーのイベント
description: チューナーのイベント
ms.assetid: eb5e0698-2641-4d47-9fa3-d1969a03c795
keywords:
- チューナー イベント WDK ビデオのキャプチャします。
- イベントの WDK ビデオのキャプチャ
- EVENTSETID_TUNER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d3844389ce57a4d65976902f6ae0f2a9a6c252
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377718"
---
# <a name="tuner-events"></a>チューナーのイベント


[EVENTSETID\_チューナー](https://docs.microsoft.com/windows-hardware/drivers/stream/eventsetid-tuner)チューナー イベントがイベント セットに含まれています。 次の表に、イベント、EVENTSETID の一部である\_チューナー イベントのセット。 2 番目のテーブルには、Windows Vista 以降を実行している AVStream ミニドライバーに対して実装されるチューナー イベントについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EVENTSETID_TUNER KS イベント</th>
<th>イベントの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-changed" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_CHANGED&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-changed)"><strong>KSEVENT_TUNER_CHANGED</strong></a></p></td>
<td><p>DirectShow チューナーが変更されたこと、たとえば、新しいテレビ チャンネルにチューニングのために通知します。</p></td>
</tr>
</tbody>
</table>

 

次の表は、EVENTSETID\_チューナー イベントは、Windows Vista の新機能です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EVENTSETID_TUNER KS イベント</th>
<th>イベントの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)"><strong>KSEVENT_TUNER_INITIATE_SCAN</strong></a></p></td>
<td><p>シグナルのスキャンを開始し、スキャンが完了したら、DirectShow を通知します。</p></td>
</tr>
</tbody>
</table>

 

 

 




