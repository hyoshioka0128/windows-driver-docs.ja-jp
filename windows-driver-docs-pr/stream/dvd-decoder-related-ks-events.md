---
title: DVD デコーダー関連の KS イベント
description: DVD デコーダー関連の KS イベント
ms.assetid: 19fd2c88-72f4-4742-8c96-74be250dd59d
keywords:
- DVD デコーダー ミニドライバー WDK、KS イベント
- デコーダー ミニドライバー WDK DVD、KS イベント
- KS イベント WDK DVD デコーダー
- イベントの WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51595a2596dd53cb34821e23439a6f1e1bfa64f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387163"
---
# <a name="dvd-decoder-related-ks-events"></a>DVD デコーダー関連の KS イベント





次の表では、イベントのセットとその対応する DVD デコーダーのハードウェアに関連するイベントをストリーミングするカーネルについて説明します。

[KSEVENTSETID\_VPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vpnotify)イベントはすべてのカーネルがチューナー イベントに関連するイベントのストリーミングをグループに設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSEVENTSETID_VPNotify KS イベント</th>
<th>イベントの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vpnotify-formatchange" data-raw-source="[&lt;strong&gt;KSEVENT_VPNOTIFY_FORMATCHANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vpnotify-formatchange)"><strong>KSEVENT_VPNOTIFY_FORMATCHANGE</strong></a></p></td>
<td><p>DirectShow、480 x 720 640 x 480 の解像度の変更など、ビデオ ポート構成での変更を通知します。</p></td>
</tr>
</tbody>
</table>

 

 

 




