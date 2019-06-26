---
title: ビデオ キャプチャのイベント
description: ビデオ キャプチャのイベント
ms.assetid: 9d40b9f7-41c1-4410-afc7-9b4ff1c2fe7e
keywords:
- イベントの WDK ビデオのキャプチャ
- KSEVENTSETID_VIDCAPNotify
- ビデオ キャプチャ イベント WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7108bfa1d57e219c5fbf97e1fdb10498d1027250
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385381"
---
# <a name="video-capture-events"></a>ビデオ キャプチャのイベント


[KSEVENTSETID\_VIDCAPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vidcapnotify)チューナー イベントに関連するイベントがイベント セットに含まれています。 次の表は、KSEVENTSETID の一部となるイベント\_VIDCAPNotify イベントのセット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSEVENTSETID_VIDCAPNotify KS イベント</th>
<th>イベントの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcaptosti-ext-trigger" data-raw-source="[&lt;strong&gt;KSEVENT_VIDCAPTOSTI_EXT_TRIGGER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcaptosti-ext-trigger)"><strong>KSEVENT_VIDCAPTOSTI_EXT_TRIGGER</strong></a></p></td>
<td><p>ビデオ キャプチャ デバイス上のボタンがトリガーされたときに、登録されているクライアントに通知します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcap-auto-update" data-raw-source="[&lt;strong&gt;KSEVENT_VIDCAP_AUTO_UPDATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcap-auto-update)"><strong>KSEVENT_VIDCAP_AUTO_UPDATE</strong></a></p></td>
<td><p>プロパティが変更されたときに、登録されているクライアントに通知します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcap-search" data-raw-source="[&lt;strong&gt;KSEVENT_VIDCAP_SEARCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcap-search)"><strong>KSEVENT_VIDCAP_SEARCH</strong></a></p></td>
<td><p>検索が完了すると、登録されているクライアントに通知します。</p></td>
</tr>
</tbody>
</table>

 

 

 




