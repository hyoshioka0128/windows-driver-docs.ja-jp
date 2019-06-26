---
title: DVD デコーダー関連のクロック イベント
description: DVD デコーダー関連のクロック イベント
ms.assetid: c3ed0ee4-95a3-4596-9f29-86397b0d8753
keywords:
- DVD デコーダー ミニドライバー WDK、マスターのクロック
- デコーダー ミニドライバー WDK DVD、マスターのクロック
- マスターのクロックの WDK DVD デコーダー
- WDK DVD デコーダーをクロックします。
- イベントの WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c842733a2c820ae76c10e3bb35e8f7721c008c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358425"
---
# <a name="dvd-decoder-related-clock-events"></a>DVD デコーダー関連のクロック イベント





DVD の再生にマスター クロックをサポートしている DVD デコーダー ミニドライバー ストリームでは、次の 2 つのクロック イベントもサポートする必要があります。[**KSEVENT\_クロック\_位置\_マーク**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-position-mark)と[ **KSEVENT\_クロック\_間隔\_マーク**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-interval-mark). これらのイベントは、DVD の再生中の任意の時刻を同期する必要がある場合、システムのコンポーネントへの参照情報を提供します。 イベントのセットの GUID は[ **KSEVENTSETID\_クロック**](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-clock)します。

DVD デコーダーのミニドライバーは、未処理のクロック イベントを確認する必要があります。 一般的な実装では、割り込みの各ビデオのスタート コードを生成または割り込みの垂直同期に対して生成されたすべてのクロック イベントを調べる場合があります。 次のイベントが提供されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>event</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSEVENT_CLOCK_POSITION_MARK</p></td>
<td><p>このイベントは、指定したストリームの時間を超過したことを示す通知を提供します。 このイベントが通知を使用して、 <em>SignalStreamEvent</em>パラメーターを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification)"> <strong>StreamClassStreamNotification</strong> </a>関数。 この呼び出しが行われた後、 <strong>KSEVENT_ENTRY</strong>関数呼び出し、以降のすべての呼び出しを含むは構造体を使用することはできません、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassgetnextevent" data-raw-source="[&lt;strong&gt;StreamClassGetNextEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassgetnextevent)"> <strong>StreamClassGetNextEvent</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td><p>KSEVENT_CLOCK_INTERVAL_MARK</p></td>
<td><p>このイベントは、指定した開始時刻に到達した後に、指定された間隔で定期的な通知を提供します。</p></td>
</tr>
</tbody>
</table>

 

 

 




