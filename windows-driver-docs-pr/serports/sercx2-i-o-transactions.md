---
title: SerCx2 の I/O トランザクション
description: SerCx2 には、読み取り (IRP_MJ_READ) と、コント ローラーのシリアル ドライバーの書き込み (IRP_MJ_WRITE) 要求の処理が簡略化します。
ms.assetid: C1B3F059-A445-4224-8316-DBF194CE6A80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c6d54870ac9a93ece45d465619404cc88add825
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349203"
---
# <a name="sercx2-io-transactions"></a>SerCx2 の I/O トランザクション


SerCx2 読み取りの処理を簡略化 ([**IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff546883)) と書き込み ([**IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff546904)) には、コント ローラーのシリアル ドライバーの要求。 読み取りまたは書き込み要求に応答して、SerCx2 シリアル コント ローラーのドライバーを 1 つまたは複数の I/O トランザクションを発行します。 ドライバーの観点からは、各トランザクションは、単純、完全な I/O 操作です。

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
<td><p><a href="overview-of-sercx2-i-o-transactions.md" data-raw-source="[Overview of SerCx2 I/O Transactions](overview-of-sercx2-i-o-transactions.md)">SerCx2 I/O トランザクションの概要</a></p></td>
<td><p>SerCx2 シリアル コント ローラーのドライバーを 1 つまたは複数の I/O トランザクションを発行して、クライアントからの読み取りまたは書き込み要求を処理します。 各トランザクションは、このドライバーは、シリアル コント ローラーと、要求のデータ バッファー間でデータを転送する I/O 操作を自己完結型として扱います。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-pio-receive-transactions.md" data-raw-source="[SerCx2 PIO-Receive Transactions](sercx2-pio-receive-transactions.md)">SerCx2 PIO 受信トランザクション</a></p></td>
<td><p>SerCx2 すべてシリアル コント ローラーを必要とドライバーのサポートを実装するトランザクションの使用が I/O (PIO) をプログラムを受信します。 SerCx2 PIO 受信トランザクションを開始するには、ドライバーが呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/dn265214" data-raw-source="[&lt;em&gt;EvtSerCx2PioReceiveReadBuffer&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265214)"> <em>EvtSerCx2PioReceiveReadBuffer</em> </a>イベント コールバック関数と、読み取りバッファーのパラメーターとして提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-pio-transmit-transactions.md" data-raw-source="[SerCx2 PIO-Transmit Transactions](sercx2-pio-transmit-transactions.md)">SerCx2 PIO 送信トランザクション</a></p></td>
<td><p>SerCx2 すべてシリアル コント ローラーを必要とドライバーのサポートを実装するトランザクションの使用が I/O (PIO) をプログラムを送信します。 SerCx2 PIO 送信トランザクションを開始するには、ドライバーが呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/dn265223" data-raw-source="[&lt;em&gt;EvtSerCx2PioTransmitWriteBuffer&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265223)"> <em>EvtSerCx2PioTransmitWriteBuffer</em> </a>イベント コールバック関数と書き込みをバッファーをパラメーターとして提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-system-dma-receive-transactions.md" data-raw-source="[SerCx2 System-DMA-Receive Transactions](sercx2-system-dma-receive-transactions.md)">SerCx2 DMA 受信システム トランザクション</a></p></td>
<td><p>一部のコント ローラーのシリアル ドライバーのサポートを実装するシステムの DMA コント ローラーを使用するトランザクションを受信します。 このようなサポートは任意ですが、長い形式のデータ転送に下手順 I/O (PIO) を使用する必要があるメイン プロセッサを削減してパフォーマンスを向上させることができます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-system-dma-transmit-transactions.md" data-raw-source="[SerCx2 System-DMA-Transmit Transactions](sercx2-system-dma-transmit-transactions.md)">SerCx2 DMA 送信システム トランザクション</a></p></td>
<td><p>一部のコント ローラーのシリアル ドライバーのサポートを実装するシステムの DMA コント ローラーを使用するトランザクションを送信します。 このようなサポートは任意ですが、長い形式のデータ転送に下手順 I/O (PIO) を使用する必要があるメイン プロセッサを削減してパフォーマンスを向上させることができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-custom-receive-transactions.md" data-raw-source="[SerCx2 Custom-Receive Transactions](sercx2-custom-receive-transactions.md)">SerCx2 カスタム受信トランザクション</a></p></td>
<td><p>シリアル コント ローラーの一部のハードウェア シリアル コント ローラーからデータを読み取る PIO またはシステム DMA 以外のデータ転送メカニズムを実装できます。 シリアル コント ローラー ドライバーがサポートできるカスタム受信トランザクションがこのデータ転送メカニズム SerCx2 で使用できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-custom-transmit-transactions.md" data-raw-source="[SerCx2 Custom-Transmit Transactions](sercx2-custom-transmit-transactions.md)">SerCx2 カスタム送信トランザクション</a></p></td>
<td><p>シリアル コント ローラーの一部のハードウェアでは、PIO またはシステム DMA 以外シリアル コント ローラーにデータを書き込むためのデータ転送メカニズムを実装できます。 シリアル コント ローラー ドライバーがサポートできるトランザクションが SerCx2 で使用できるようにこのデータ転送メカニズムをカスタム送信します。</p></td>
</tr>
</tbody>
</table>

 

 

 




