---
title: SerCx2 の I/O トランザクション
description: SerCx2 は、シリアルコントローラードライバーに対する読み取り (IRP_MJ_READ) と書き込み (IRP_MJ_WRITE) 要求の処理を簡略化します。
ms.assetid: C1B3F059-A445-4224-8316-DBF194CE6A80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 871d1dc2c10ae946d77e03909d2f13164e3c83ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845405"
---
# <a name="sercx2-io-transactions"></a>SerCx2 の I/O トランザクション

SerCx2 は、シリアルコントローラードライバーに対する読み取り ([**irp\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))) 要求と書き込み ([**irp\_MJ\_書き込み**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))) 要求の処理を簡略化します。 SerCx2 は、読み取りまたは書き込み要求に応答して、1つ以上の i/o トランザクションをシリアルコントローラードライバーに発行します。 ドライバーの観点から見ると、各トランザクションは単純で完全な i/o 操作です。

## <a name="in-this-section"></a>このセクションの内容

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="overview-of-sercx2-i-o-transactions.md" data-raw-source="[Overview of SerCx2 I/O Transactions](overview-of-sercx2-i-o-transactions.md)">SerCx2 i/o トランザクションの概要</a></p></td>
<td><p>SerCx2 は、1つ以上の i/o トランザクションをシリアルコントローラードライバーに発行することによって、クライアントからの読み取り要求または書き込み要求を処理します。 このドライバーは、要求内のシリアルコントローラーとデータバッファーとの間でデータを転送する自己完結型の i/o 操作として各トランザクションを処理します。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-pio-receive-transactions.md" data-raw-source="[SerCx2 PIO-Receive Transactions](sercx2-pio-receive-transactions.md)">SerCx2 PIO-トランザクションを受信する</a></p></td>
<td><p>SerCx2 では、プログラム i/o (PIO) を使用する受信トランザクションのサポートを実装するために、すべてのシリアルコントローラードライバーが必要です。 PIO 受信トランザクションを開始するために、SerCx2 はドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer" data-raw-source="[&lt;em&gt;EvtSerCx2PioReceiveReadBuffer&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer)"><em>EvtSerCx2PioReceiveReadBuffer</em></a>イベントコールバック関数を呼び出し、パラメーターとして読み取りバッファーを提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-pio-transmit-transactions.md" data-raw-source="[SerCx2 PIO-Transmit Transactions](sercx2-pio-transmit-transactions.md)">SerCx2 PIO-送信トランザクション</a></p></td>
<td><p>SerCx2 では、プログラムによる i/o (PIO) を使用する送信トランザクションのサポートを実装するために、すべてのシリアルコントローラードライバーが必要です。 PIO 送信トランザクションを開始するために、SerCx2 はドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer" data-raw-source="[&lt;em&gt;EvtSerCx2PioTransmitWriteBuffer&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)"><em>EvtSerCx2PioTransmitWriteBuffer</em></a>イベントコールバック関数を呼び出し、パラメーターとして書き込みバッファーを提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-system-dma-receive-transactions.md" data-raw-source="[SerCx2 System-DMA-Receive Transactions](sercx2-system-dma-receive-transactions.md)">SerCx2-DMA-トランザクションの受信</a></p></td>
<td><p>一部のシリアルコントローラードライバーでは、システム DMA コントローラーを使用する receive トランザクションのサポートが実装されています。 このようなサポートは省略可能ですが、長時間のデータ転送のためにプログラミング i/o (PIO) を使用する必要がある主なプロセッサを削減することで、パフォーマンスを向上させることができます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-system-dma-transmit-transactions.md" data-raw-source="[SerCx2 System-DMA-Transmit Transactions](sercx2-system-dma-transmit-transactions.md)">SerCx2-送信トランザクション</a></p></td>
<td><p>一部のシリアルコントローラードライバーでは、システム DMA コントローラーを使用する転送トランザクションのサポートが実装されています。 このようなサポートは省略可能ですが、長時間のデータ転送のためにプログラミング i/o (PIO) を使用する必要がある主なプロセッサを削減することで、パフォーマンスを向上させることができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-custom-receive-transactions.md" data-raw-source="[SerCx2 Custom-Receive Transactions](sercx2-custom-receive-transactions.md)">SerCx2 カスタム-Receive トランザクション</a></p></td>
<td><p>シリアルコントローラーハードウェアによっては、シリアルコントローラーからデータを読み取るために PIO やシステム DMA 以外のデータ転送機構を実装している場合があります。 シリアルコントローラードライバーは、カスタム受信トランザクションをサポートして、このデータ転送メカニズムを SerCx2 で使用できるようにすることができます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-custom-transmit-transactions.md" data-raw-source="[SerCx2 Custom-Transmit Transactions](sercx2-custom-transmit-transactions.md)">SerCx2 カスタム送信トランザクション</a></p></td>
<td><p>シリアルコントローラーハードウェアによっては、シリアルコントローラーにデータを書き込むための PIO やシステム DMA 以外のデータ転送機構を実装する場合があります。 シリアルコントローラードライバーは、カスタム送信トランザクションをサポートして、このデータ転送メカニズムを SerCx2 で使用できるようにすることができます。</p></td>
</tr>
</tbody>
</table>
