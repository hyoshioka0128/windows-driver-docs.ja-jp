---
title: DVD デコーダー関連のクロック イベント
description: DVD デコーダー関連のクロック イベント
ms.assetid: c3ed0ee4-95a3-4596-9f29-86397b0d8753
keywords:
- DVD デコーダーミニドライバー WDK、マスタークロック
- デコーダーミニドライバー WDK DVD、マスタークロック
- マスタークロック WDK DVD デコーダー
- 時計 WDK DVD デコーダー
- イベント WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d88d80085b82f2a58f6a690bd86a41b6fd392326
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843218"
---
# <a name="dvd-decoder-related-clock-events"></a>DVD デコーダー関連のクロック イベント





DVD 再生用のマスタークロックをサポートするすべての DVD デコーダーミニドライバーストリームでは、次の2つのクロックイベントもサポートする必要があります。 [**KSEVENT\_clock\_POSITION\_MARK**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-position-mark)および[**KSEVENT\_clock\_INTERVAL\_マーク**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-interval-mark)。 これらのイベントは、DVD の再生中にいつでも同期する必要がある場合に、システム内のコンポーネントに参照情報を提供します。 イベントセットの GUID は、 [**KSEVENTSETID\_Clock**](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-clock)です。

DVD デコーダーミニドライバーは、未処理のクロックイベントを確認する必要があります。 一般的な実装では、ビデオの開始コードごとに生成された割り込み、または垂直同期用に生成された割り込みのすべてのクロックイベントを調べることができます。 次のイベントが提供されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベント</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSEVENT_CLOCK_POSITION_MARK</p></td>
<td><p>このイベントは、指定されたストリーム時間を超えたことを通知します。 このイベントは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)"><strong>Streamclassstreamnotification</strong></a>関数の<em>signalstreamevent</em>パラメーターを使用して通知されます。 この呼び出しが行われた後、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassgetnextevent" data-raw-source="[&lt;strong&gt;StreamClassGetNextEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassgetnextevent)"><strong>StreamClassGetNextEvent</strong></a>関数の呼び出しなど、それ以降の関数呼び出しに<strong>KSEVENT_ENTRY</strong>構造体を使用することはできません。</p></td>
</tr>
<tr class="even">
<td><p>KSEVENT_CLOCK_INTERVAL_MARK</p></td>
<td><p>このイベントは、指定された開始時刻に達した後に、指定した間隔で定期的に通知を提供します。</p></td>
</tr>
</tbody>
</table>

 

 

 




