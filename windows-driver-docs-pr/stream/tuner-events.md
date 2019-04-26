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
ms.openlocfilehash: 32a738879c95cfb3d4654bae447025d87394e1be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354857"
---
# <a name="tuner-events"></a>チューナーのイベント


[EVENTSETID\_チューナー](https://msdn.microsoft.com/library/windows/hardware/ff559566)チューナー イベントがイベント セットに含まれています。 次の表に、イベント、EVENTSETID の一部である\_チューナー イベントのセット。 2 番目のテーブルには、Windows Vista 以降を実行している AVStream ミニドライバーに対して実装されるチューナー イベントについて説明します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561894" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_CHANGED&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561894)"><strong>KSEVENT_TUNER_CHANGED</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561898" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561898)"><strong>KSEVENT_TUNER_INITIATE_SCAN</strong></a></p></td>
<td><p>シグナルのスキャンを開始し、スキャンが完了したら、DirectShow を通知します。</p></td>
</tr>
</tbody>
</table>

 

 

 




