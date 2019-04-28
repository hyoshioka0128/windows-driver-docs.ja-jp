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
ms.openlocfilehash: 276342417ba8ab8697c83eec3a4304c0c5035bb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363913"
---
# <a name="dvd-decoder-related-ks-events"></a>DVD デコーダー関連の KS イベント





次の表では、イベントのセットとその対応する DVD デコーダーのハードウェアに関連するイベントをストリーミングするカーネルについて説明します。

[KSEVENTSETID\_VPNotify](https://msdn.microsoft.com/library/windows/hardware/ff561780)イベントはすべてのカーネルがチューナー イベントに関連するイベントのストリーミングをグループに設定します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561933" data-raw-source="[&lt;strong&gt;KSEVENT_VPNOTIFY_FORMATCHANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561933)"><strong>KSEVENT_VPNOTIFY_FORMATCHANGE</strong></a></p></td>
<td><p>DirectShow、480 x 720 640 x 480 の解像度の変更など、ビデオ ポート構成での変更を通知します。</p></td>
</tr>
</tbody>
</table>

 

 

 




