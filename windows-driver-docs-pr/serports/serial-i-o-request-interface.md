---
title: シリアル I/O 要求インターフェイス
description: シリアルコントローラー上のポートに接続されている周辺機器を制御するために、クライアントアプリケーションまたは周辺機器ドライバーが i/o 要求をポートに送信します。
ms.assetid: D536A0EC-2B8B-491B-8A14-656F4B5A3843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce989c4fc56687995620926e66700d6f8747763c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844939"
---
# <a name="serial-io-request-interface"></a>シリアル I/O 要求インターフェイス

シリアルコントローラー上のポートに接続されている周辺機器を制御するために、クライアントアプリケーションまたは周辺機器ドライバーが i/o 要求をポートに送信します。 クライアントは、 [**irp\_MJ\_WRITE**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))および[**irp\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))要求を使用して、シリアルポートとの間でデータを送受信します。 さらに、Windows では、クライアントがシリアルポートを構成するために使用できる一連のシリアル i/o 制御要求 (Ioctl) を定義します。

Serial **IRP\_MJ\_<em>XXX</em>** 要求とシリアル ioctl を組み合わせて、シリアル i/o 要求インターフェイスを形成します。これは、一連のシリアルコントローラーデバイスでサポートされています。 このインターフェイスは、SerCx2 または SerCx と拡張ベースのシリアルコントローラードライバーの組み合わせによって、シリアル .sys ドライバーによってサポートされています。

SerCx2、SerCx、および Serial は、同じシリアル Ioctl の多くをサポートしています。 ただし、SerCx2、SerCx、および Serial .sys では、*シリアルデバイス制御要求*で指定される ioctl の異なるサブセットをサポートしています。 次の表は、SerCx2、SerCx、および Serial .sys でサポートされている Ioctl のサブセットをまとめたものです。 テーブルの **"Yes"** エントリは、シリアルフレームワーク拡張機能またはドライバーが対応する IOCTL をサポートしていることを示し、エントリ**が**ないことを示します。

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
<th>シリアル .sys</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration)"><strong>IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clear_stats" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLEAR_STATS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clear_stats)"><strong>IOCTL_SERIAL_CLEAR_STATS</strong></a></p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clr_dtr" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_DTR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clr_dtr)"><strong>IOCTL_SERIAL_CLR_DTR</strong></a></p></td>
<td><p>メモ1を参照してください。</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clr_rts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_RTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clr_rts)"><strong>IOCTL_SERIAL_CLR_RTS</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_config_size" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CONFIG_SIZE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_config_size)"><strong>IOCTL_SERIAL_CONFIG_SIZE</strong></a></p></td>
<td><p>必須ではない</p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_baud_rate" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_BAUD_RATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_baud_rate)"><strong>IOCTL_SERIAL_GET_BAUD_RATE</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_chars" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_CHARS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_chars)"><strong>IOCTL_SERIAL_GET_CHARS</strong></a></p></td>
<td><p>メモ2を参照してください。</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_commstatus" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_COMMSTATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_commstatus)"><strong>IOCTL_SERIAL_GET_COMMSTATUS</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_dtrrts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_DTRRTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_dtrrts)"><strong>IOCTL_SERIAL_GET_DTRRTS</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_handflow" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_HANDFLOW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_handflow)"><strong>IOCTL_SERIAL_GET_HANDFLOW</strong></a></p></td>
<td><p>メモ1を参照してください。</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_line_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_LINE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_line_control)"><strong>IOCTL_SERIAL_GET_LINE_CONTROL</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_modem_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEM_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_modem_control)"><strong>IOCTL_SERIAL_GET_MODEM_CONTROL</strong></a> (注4を参照)</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_modemstatus" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEMSTATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_modemstatus)"><strong>IOCTL_SERIAL_GET_MODEMSTATUS</strong></a></p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_properties" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_PROPERTIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_properties)"><strong>IOCTL_SERIAL_GET_PROPERTIES</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_stats" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_STATS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_stats)"><strong>IOCTL_SERIAL_GET_STATS</strong></a></p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_timeouts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_TIMEOUTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_timeouts)"><strong>IOCTL_SERIAL_GET_TIMEOUTS</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_wait_mask" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_WAIT_MASK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_wait_mask)"><strong>IOCTL_SERIAL_GET_WAIT_MASK</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_immediate_char" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_IMMEDIATE_CHAR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_immediate_char)"><strong>IOCTL_SERIAL_IMMEDIATE_CHAR</strong></a></p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_lsrmst_insert" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_LSRMST_INSERT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_lsrmst_insert)"><strong>IOCTL_SERIAL_LSRMST_INSERT</strong></a></p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_purge" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_PURGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_purge)"><strong>IOCTL_SERIAL_PURGE</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_reset_device" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_RESET_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_reset_device)"><strong>IOCTL_SERIAL_RESET_DEVICE</strong></a> (注5を参照)</p></td>
<td><p>必須ではない</p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_baud_rate" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BAUD_RATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_baud_rate)"><strong>IOCTL_SERIAL_SET_BAUD_RATE</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_break_off" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_OFF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_break_off)"><strong>IOCTL_SERIAL_SET_BREAK_OFF</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_break_on" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_ON&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_break_on)"><strong>IOCTL_SERIAL_SET_BREAK_ON</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_chars" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_CHARS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_chars)"><strong>IOCTL_SERIAL_SET_CHARS</strong></a></p></td>
<td><p>メモ2を参照してください。</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_dtr" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_DTR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_dtr)"><strong>IOCTL_SERIAL_SET_DTR</strong></a></p></td>
<td><p>メモ1を参照してください。</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_fifo_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_FIFO_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_fifo_control)"><strong>IOCTL_SERIAL_SET_FIFO_CONTROL</strong></a></p></td>
<td><p>メモ1を参照してください。</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_handflow" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_HANDFLOW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_handflow)"><strong>IOCTL_SERIAL_SET_HANDFLOW</strong></a> (注3を参照)</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_line_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_LINE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_line_control)"><strong>IOCTL_SERIAL_SET_LINE_CONTROL</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_modem_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_MODEM_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_modem_control)"><strong>IOCTL_SERIAL_SET_MODEM_CONTROL</strong></a> (注4を参照)</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_queue_size" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_QUEUE_SIZE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_queue_size)"><strong>IOCTL_SERIAL_SET_QUEUE_SIZE</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_rts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_RTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_rts)"><strong>IOCTL_SERIAL_SET_RTS</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_TIMEOUTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)"><strong>IOCTL_SERIAL_SET_TIMEOUTS</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_wait_mask" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_WAIT_MASK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)"><strong>IOCTL_SERIAL_SET_WAIT_MASK</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_xoff" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XOFF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_xoff)"><strong>IOCTL_SERIAL_SET_XOFF</strong></a></p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_xon" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XON&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_xon)"><strong>IOCTL_SERIAL_SET_XON</strong></a></p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_wait_on_mask" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_WAIT_ON_MASK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_wait_on_mask)"><strong>IOCTL_SERIAL_WAIT_ON_MASK</strong></a></p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_xoff_counter" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_XOFF_COUNTER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_xoff_counter)"><strong>IOCTL_SERIAL_XOFF_COUNTER</strong></a></p></td>
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
</tbody>
</table>


**メモ**

1. SerCx2 は、シリアルコントローラードライバーの実装とシリアルコントローラーハードウェアの機能に応じて、この IOCTL をサポートするかどうかによって異なる場合があります。

2. SerCx2 は特殊文字をサポートしていません。 SerCx2 は、常に**IOCTL\_シリアル\_設定され\_CHARS**要求の状態\_成功状態コードを設定しますが、この要求に応答して特殊文字を設定したり、その他の操作を実行したりすることはありません。 **IOCTL\_serial\_GET\_CHARS**要求の場合、SerCx2 は、[**シリアル\_chars**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_chars)構造体のすべての文字値を null に設定し、ステータス\_成功状態コードを使用して要求を完了します。

3. SerCx2 と SerCx は、 **SERIAL\_の FLOWREPLACE**構造の**Flowreplace**および**controlhandshake**メンバーに定義されているフラグのサブセットのみをサポートしています。 Serial .sys は、これらのフラグのすべてをサポートします。 詳細については、「 [**SERIAL\_の配信フロー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_handflow)」を参照してください。

4. **Ioctl\_serial\_GET\_modem\_control**および**ioctl\_serial\_SET\_modem\_control** requests は主にハードウェアテストに使用されます。 モデムの制御操作には、標準レジスタのレイアウトが定義されていません。 モデム制御を使用する周辺機器は、特定のシリアルコントローラーのハードウェア機能に依存している場合に、それ自体を使用します。

5. Serial .sys ドライバーは、常に**IOCTL\_シリアル\_リセット\_デバイス**要求を正常に完了した\_状態でリセットしますが、この要求に対する応答では操作を実行しません。 SerCx2 と SerCx は、**デバイス要求\_のシリアル\_の\_シリアル**の送信をサポートしておらず、常に状態\_\_実装されていない要求を完了します。

**IOCTL\_シリアル\_<em>XXX</em>** 要求の詳細、およびシリアルコントローラーの読み取りおよび書き込み要求の詳細については、 [ntddser](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddser/)ヘッダーを参照してください。
