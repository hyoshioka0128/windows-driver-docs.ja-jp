---
title: シリアル I/O 要求インターフェイス
description: シリアル コント ローラーで、クライアントのポートに接続されている周辺機器を制御するには、アプリケーションまたは周辺機器のデバイス ドライバーは、ポートに I/O 要求を送信します。
ms.assetid: D536A0EC-2B8B-491B-8A14-656F4B5A3843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e793aa4f33d9f2ee60dc2d5a7f73daa9070d5ab1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356743"
---
# <a name="serial-io-request-interface"></a>シリアル I/O 要求インターフェイス

シリアル コント ローラーで、クライアントのポートに接続されている周辺機器を制御するには、アプリケーションまたは周辺機器のデバイス ドライバーは、ポートに I/O 要求を送信します。 クライアントを使って[ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))と[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))データを送信し、シリアル ポートから受信したデータを要求します。 さらに、Windows では、シリアル ポートを構成するクライアントが使用できるシリアルの I/O 制御要求 (Ioctl) のセットを定義します。

シリアル**IRP\_MJ\_* XXX*** シリアル I/O 要求インターフェイスは、さまざまなデバイスのシリアル コント ローラーでサポートされている要求とシリアル Ioctl 形成します。 SerCx2 または SerCx とシリアル コント ローラーの拡張機能に基づいたドライバーの組み合わせと、以下のようドライバーによって、このインターフェイスはサポートされています。

SerCx2、SerCx、および際に、同じシリアル Ioctl の多くをサポートします。 ただし、SerCx2、SerCx、および以下のように指定された Ioctl のさまざまなサブセットをサポート*シリアル デバイスに対する制御要求*します。 次の表は、Ioctl SerCx2、SerCx、およびスタックでサポートされているのサブセットをまとめたものです。 A**はい**テーブル内のエントリは、シリアル フレームワークの拡張機能またはドライバーが、対応する、IOCTL をサポートしていることを示します、**いいえ**エントリはしないことを示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>シリアル IOCTL</th>
<th>SerCx2</th>
<th>SerCx</th>
<th>スタック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration)"><strong>IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_clear_stats" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLEAR_STATS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_clear_stats)"><strong>IOCTL_SERIAL_CLEAR_STATS</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_clr_dtr" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_DTR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_clr_dtr)"><strong>IOCTL_SERIAL_CLR_DTR</strong></a></p></td>
<td><p>注 1 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_clr_rts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_RTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_clr_rts)"><strong>IOCTL_SERIAL_CLR_RTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_config_size" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CONFIG_SIZE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_config_size)"><strong>IOCTL_SERIAL_CONFIG_SIZE</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_baud_rate" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_BAUD_RATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_baud_rate)"><strong>IOCTL_SERIAL_GET_BAUD_RATE</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_chars" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_CHARS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_chars)"><strong>IOCTL_SERIAL_GET_CHARS</strong></a></p></td>
<td><p>注 2 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_commstatus" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_COMMSTATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_commstatus)"><strong>IOCTL_SERIAL_GET_COMMSTATUS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_dtrrts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_DTRRTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_dtrrts)"><strong>IOCTL_SERIAL_GET_DTRRTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_handflow" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_HANDFLOW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_handflow)"><strong>IOCTL_SERIAL_GET_HANDFLOW</strong></a></p></td>
<td><p>注 1 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_line_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_LINE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_line_control)"><strong>IOCTL_SERIAL_GET_LINE_CONTROL</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_modem_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEM_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_modem_control)"><strong>IOCTL_SERIAL_GET_MODEM_CONTROL</strong> </a> (注 4 を参照)</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_modemstatus" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEMSTATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_modemstatus)"><strong>IOCTL_SERIAL_GET_MODEMSTATUS</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_properties" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_PROPERTIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_properties)"><strong>IOCTL_SERIAL_GET_PROPERTIES</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_stats" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_STATS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_stats)"><strong>IOCTL_SERIAL_GET_STATS</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_timeouts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_TIMEOUTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_timeouts)"><strong>IOCTL_SERIAL_GET_TIMEOUTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_wait_mask" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_WAIT_MASK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_wait_mask)"><strong>IOCTL_SERIAL_GET_WAIT_MASK</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_immediate_char" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_IMMEDIATE_CHAR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_immediate_char)"><strong>IOCTL_SERIAL_IMMEDIATE_CHAR</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_lsrmst_insert" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_LSRMST_INSERT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_lsrmst_insert)"><strong>IOCTL_SERIAL_LSRMST_INSERT</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_purge" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_PURGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_purge)"><strong>IOCTL_SERIAL_PURGE</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_reset_device" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_RESET_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_reset_device)"><strong>IOCTL_SERIAL_RESET_DEVICE</strong> </a> (注 5 を参照)</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_baud_rate" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BAUD_RATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_baud_rate)"><strong>IOCTL_SERIAL_SET_BAUD_RATE</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_break_off" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_OFF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_break_off)"><strong>IOCTL_SERIAL_SET_BREAK_OFF</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_break_on" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_ON&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_break_on)"><strong>IOCTL_SERIAL_SET_BREAK_ON</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_chars" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_CHARS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_chars)"><strong>IOCTL_SERIAL_SET_CHARS</strong></a></p></td>
<td><p>注 2 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_dtr" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_DTR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_dtr)"><strong>IOCTL_SERIAL_SET_DTR</strong></a></p></td>
<td><p>注 1 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_fifo_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_FIFO_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_fifo_control)"><strong>IOCTL_SERIAL_SET_FIFO_CONTROL</strong></a></p></td>
<td><p>注 1 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_handflow" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_HANDFLOW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_handflow)"><strong>IOCTL_SERIAL_SET_HANDFLOW</strong> </a> (注 3 を参照)</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_line_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_LINE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_line_control)"><strong>IOCTL_SERIAL_SET_LINE_CONTROL</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_modem_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_MODEM_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_modem_control)"><strong>IOCTL_SERIAL_SET_MODEM_CONTROL</strong> </a> (注 4 を参照)</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_queue_size" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_QUEUE_SIZE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_queue_size)"><strong>IOCTL_SERIAL_SET_QUEUE_SIZE</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_rts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_RTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_rts)"><strong>IOCTL_SERIAL_SET_RTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_TIMEOUTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts)"><strong>IOCTL_SERIAL_SET_TIMEOUTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_wait_mask" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_WAIT_MASK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)"><strong>IOCTL_SERIAL_SET_WAIT_MASK</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_xoff" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XOFF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_xoff)"><strong>IOCTL_SERIAL_SET_XOFF</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_xon" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XON&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_xon)"><strong>IOCTL_SERIAL_SET_XON</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_wait_on_mask" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_WAIT_ON_MASK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_wait_on_mask)"><strong>IOCTL_SERIAL_WAIT_ON_MASK</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_xoff_counter" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_XOFF_COUNTER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_xoff_counter)"><strong>IOCTL_SERIAL_XOFF_COUNTER</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
</tbody>
</table>


**メモ**

1. SerCx2 は可能性があります。 またはコント ローラーのシリアル ドライバーの実装とシリアル コント ローラーのハードウェアの機能によってこの IOCTL をサポートしていません。

2. SerCx2 は特殊文字をサポートしていません。 SerCx2 が完了すると常に、 **IOCTL\_シリアル\_設定\_CHARS**状態が、要求\_成功の状態のコードはない特殊文字を設定またはその他の操作を実行この要求に応答します。 **IOCTL\_シリアル\_取得\_CHARS** SerCx2 のすべての文字値の設定を要求、 [**シリアル\_CHARS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_chars)を null、構造体であり、状態が、要求が完了すると\_成功状態コード。

3. SerCx2 と SerCx に対して定義されているフラグのサブセットのみをサポート、 **FlowReplace**と**ControlHandShake**のメンバー、**シリアル\_HANDFLOW**構造体。 以下のようには、すべてのこれらのフラグがサポートしています。 詳細については、次を参照してください。 [**シリアル\_HANDFLOW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_handflow)します。

4. **IOCTL\_シリアル\_取得\_モデム\_コントロール**と**IOCTL\_シリアル\_設定\_モデム\_コントロール**要求は、主に、ハードウェアのテストに使用します。 モデムの管理操作を登録する標準的なレイアウトが定義されていません。 モデム コントロール シリアル コント ローラーの特定のハードウェア機能に依存させること自体の Ioctl リスクを使用して、周辺機器のドライバーです。

5. スタックのドライバーが完了すると常に、 **IOCTL\_シリアル\_リセット\_デバイス**状態要求\_成功した場合、演算を実行しないこの要求に応答します。 SerCx2 および SerCx はサポートされません**IOCTL\_シリアル\_リセット\_デバイス**要求し、これらの要求の状態を常に完了\_いない\_実装されていません。

詳細については**IOCTL\_シリアル\_* XXX*** を要求し、読み取りとシリアル コント ローラーの書き込み要求を参照してください、 [ntddser.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ntddser/)ヘッダー。
