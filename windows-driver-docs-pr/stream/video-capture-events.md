---
title: ビデオ キャプチャ イベント
description: ビデオ キャプチャ イベント
ms.assetid: 9d40b9f7-41c1-4410-afc7-9b4ff1c2fe7e
keywords:
- イベントの WDK ビデオのキャプチャ
- KSEVENTSETID_VIDCAPNotify
- ビデオ キャプチャ イベント WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3094178fd038d734f0f4e28c95c535023ba0fab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539659"
---
# <a name="video-capture-events"></a>ビデオ キャプチャ イベント


[KSEVENTSETID\_VIDCAPNotify](https://msdn.microsoft.com/library/windows/hardware/ff561773)チューナー イベントに関連するイベントがイベント セットに含まれています。 次の表は、KSEVENTSETID の一部となるイベント\_VIDCAPNotify イベントのセット。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561912" data-raw-source="[&lt;strong&gt;KSEVENT_VIDCAPTOSTI_EXT_TRIGGER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561912)"><strong>KSEVENT_VIDCAPTOSTI_EXT_TRIGGER</strong></a></p></td>
<td><p>ビデオ キャプチャ デバイス上のボタンがトリガーされたときに、登録されているクライアントに通知します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561916" data-raw-source="[&lt;strong&gt;KSEVENT_VIDCAP_AUTO_UPDATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561916)"><strong>KSEVENT_VIDCAP_AUTO_UPDATE</strong></a></p></td>
<td><p>プロパティが変更されたときに、登録されているクライアントに通知します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561923" data-raw-source="[&lt;strong&gt;KSEVENT_VIDCAP_SEARCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561923)"><strong>KSEVENT_VIDCAP_SEARCH</strong></a></p></td>
<td><p>検索が完了すると、登録されているクライアントに通知します。</p></td>
</tr>
</tbody>
</table>

 

 

 




