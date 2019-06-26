---
title: 外部トランスポートのプロパティ
description: 外部トランスポートのプロパティ
ms.assetid: e57e6c13-dfa3-4bec-9136-0e2bb2ffdd56
keywords:
- 外部のトランスポートのプロパティ WDK ビデオのキャプチャします。
- トランスポートのプロパティの WDK ビデオ キャプチャ
- PROPSETID_EXT_TRANSPORT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11321e9e89c46cf09eeb3cf24619d45f01eaf3f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384101"
---
# <a name="external-transport-properties"></a>外部トランスポートのプロパティ


[PROPSETID\_EXT\_トランスポート](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-ext-transport)プロパティ セットには検索するためと送信シグナルの種類など、外部ソースから、コントロールとデータの転送に関連するプロパティが含まれています、特定の場所またはソースのメディアのタイムコードします。 次の表に、プロパティ、PROPSETID の一部である\_EXT\_トランスポートのプロパティ セット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_EXT_TRANSPORT KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-capabilities)"><strong>KSPROPERTY_EXTXPORT_CAPABILITIES</strong></a></p></td>
<td><p>など、外部データ トランスポートの機能に関する情報を返すかどうか、デバイスのメディアを取り出すことができます、またはデバイスが後方に再生できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-input-signal-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-input-signal-mode)"><strong>KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>525 線、60 ヘルツ (NTSC) 標準定義 SD-DV、または MPEG2 トランスポート ストリームなど、トランスポートの入力信号のモードを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-output-signal-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-output-signal-mode)"><strong>KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>50 ヘルツ (PAL) MPEG 625 線など、トランスポートの出力シグナル モードを制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-load-medium" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_LOAD_MEDIUM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-load-medium)"><strong>KSPROPERTY_EXTXPORT_LOAD_MEDIUM</strong></a></p></td>
<td><p>読み込み中の制御オープンのトレイなどの外部のデバイスの閉じるトレイ、または取り出します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-medium-info" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_MEDIUM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-medium-info)"><strong>KSPROPERTY_EXTXPORT_MEDIUM_INFO</strong></a></p></td>
<td><p>カセット テープまたはディスク、および書き込み保護が有効になっているかどうかなどの外部のデバイスのメディアに関する情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state)"><strong>KSPROPERTY_EXTXPORT_STATE</strong></a></p></td>
<td><p>外部のデバイスのトランスポート モードと状態を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state-notify" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE_NOTIFY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-state-notify)"><strong>KSPROPERTY_EXTXPORT_STATE_NOTIFY</strong></a></p></td>
<td><p>外部のデバイスのトランスポート モードの変更、またはその状態の変更の通知を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-timecode-search" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_TIMECODE_SEARCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-timecode-search)"><strong>KSPROPERTY_EXTXPORT_TIMECODE_SEARCH</strong></a></p></td>
<td><p>2 つ目のフレームを含む、検索、分、および 1 時間にタイムコードを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-atn-search" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_ATN_SEARCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-atn-search)"><strong>KSPROPERTY_EXTXPORT_ATN_SEARCH</strong></a></p></td>
<td><p>テープ上に検索する絶対追跡番号を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-rtc-search" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RTC_SEARCH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extxport-rtc-search)"><strong>KSPROPERTY_EXTXPORT_RTC_SEARCH</strong></a></p></td>
<td><p>テープ上に検索する相対時間カウンターを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-raw-avc-cmd" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RAW_AVC_CMD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-raw-avc-cmd)"><strong>KSPROPERTY_EXTXPORT_RAW_AVC_CMD</strong></a></p></td>
<td><p>外部のデバイスに送信する生 AV/C コードを制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




