---
title: 外部のトランスポートのプロパティ
description: 外部のトランスポートのプロパティ
ms.assetid: e57e6c13-dfa3-4bec-9136-0e2bb2ffdd56
keywords:
- 外部のトランスポートのプロパティ WDK ビデオのキャプチャします。
- トランスポートのプロパティの WDK ビデオ キャプチャ
- PROPSETID_EXT_TRANSPORT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb48052c694e8e742f8d27133b450946e9e96b09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551109"
---
# <a name="external-transport-properties"></a>外部のトランスポートのプロパティ


[PROPSETID\_EXT\_トランスポート](https://msdn.microsoft.com/library/windows/hardware/ff567797)プロパティ セットには検索するためと送信シグナルの種類など、外部ソースから、コントロールとデータの転送に関連するプロパティが含まれています、特定の場所またはソースのメディアのタイムコードします。 次の表に、プロパティ、PROPSETID の一部である\_EXT\_トランスポートのプロパティ セット。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565160" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565160)"><strong>KSPROPERTY_EXTXPORT_CAPABILITIES</strong></a></p></td>
<td><p>かどうかなど、外部データ トランスポートの機能に関する情報を返しますデバイス&#39;s メディアを取り出すことができます、またはデバイスが後方に再生できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565161" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565161)"><strong>KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>525 線、60 ヘルツ (NTSC) 標準定義 SD-DV、または MPEG2 トランスポート ストリームなど、トランスポートの入力信号のモードを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565165" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565165)"><strong>KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE</strong></a></p></td>
<td><p>50 ヘルツ (PAL) MPEG 625 線など、トランスポートの出力シグナル モードを制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565162" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_LOAD_MEDIUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565162)"><strong>KSPROPERTY_EXTXPORT_LOAD_MEDIUM</strong></a></p></td>
<td><p>読み込み中の制御オープンのトレイなどの外部のデバイスの閉じるトレイ、または取り出します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565163" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_MEDIUM_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565163)"><strong>KSPROPERTY_EXTXPORT_MEDIUM_INFO</strong></a></p></td>
<td><p>外部デバイスに関する情報を返します&#39;s のメディアでは、カセット テープまたはディスク、および書き込み保護が有効になっているかどうか。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565168" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565168)"><strong>KSPROPERTY_EXTXPORT_STATE</strong></a></p></td>
<td><p>外部のデバイスを制御&#39;s トランスポート モードと状態。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565169" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_STATE_NOTIFY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565169)"><strong>KSPROPERTY_EXTXPORT_STATE_NOTIFY</strong></a></p></td>
<td><p>外部デバイスの通知を制御&#39;トランスポート モードの変更またはその状態を変更します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565170" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_TIMECODE_SEARCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565170)"><strong>KSPROPERTY_EXTXPORT_TIMECODE_SEARCH</strong></a></p></td>
<td><p>2 つ目のフレームを含む、検索、分、および 1 時間にタイムコードを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565159" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_ATN_SEARCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565159)"><strong>KSPROPERTY_EXTXPORT_ATN_SEARCH</strong></a></p></td>
<td><p>テープ上に検索する絶対追跡番号を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565166" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RTC_SEARCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565166)"><strong>KSPROPERTY_EXTXPORT_RTC_SEARCH</strong></a></p></td>
<td><p>テープ上に検索する相対時間カウンターを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565214" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_RAW_AVC_CMD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565214)"><strong>KSPROPERTY_EXTXPORT_RAW_AVC_CMD</strong></a></p></td>
<td><p>外部のデバイスに送信する生 AV/C コードを制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




