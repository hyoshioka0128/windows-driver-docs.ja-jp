---
title: SerCx2 で管理されるシリアル ポート上のデバイスにアクセスする
description: SerCx2 とコント ローラーのシリアル ドライバーの周辺機器が完全に接続されているシリアル ポートを連携して管理します。
ms.assetid: EF7F42D3-21A5-42F8-86AB-897281DF4F18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bd74d551ce37ad4c21aca77b80e67c547c01322
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391414"
---
# <a name="accessing-a-device-on-a-sercx2-managed-serial-port"></a>SerCx2 で管理されるシリアル ポート上のデバイスにアクセスする


SerCx2 とコント ローラーのシリアル ドライバーの周辺機器が完全に接続されているシリアル ポートを連携して管理します。 SerCx2 で管理されたシリアル ポート周辺機器にアクセスするには、周辺機器は、ドライバーは、シリアル ポートへの論理接続を開きをこの接続を表すファイル ハンドルを取得します。 ドライバーは、I/O 要求をポートに送信するのにこのハンドルを使用します。

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
<td><p><a href="peripheral-drivers-for-devices-on-sercx2-managed-serial-ports.md" data-raw-source="[Peripheral Drivers for Devices on SerCx2-Managed Serial Ports](peripheral-drivers-for-devices-on-sercx2-managed-serial-ports.md)">シリアル ポートの SerCx2 管理上のデバイス用の周辺機器のドライバー</a></p></td>
<td><p>通常、SerCx2 によって管理されているシリアル ポートは周辺機器に接続されている永続的にします。 このデバイスは、シリアル ポートへの I/O 要求を送信する周辺ドライバーによって制御されます。 これらの要求は、デバイスとデータの転送し、シリアル ポートの状態を構成します。 周辺機器のドライバーによって送信された I/O 要求は、SerCx2 と関連付けられているシリアル コント ローラー ドライバーによって共同で処理されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="opening-a-sercx2-managed-serial-port.md" data-raw-source="[Opening a SerCx2-Managed Serial Port](opening-a-sercx2-managed-serial-port.md)">SerCx2 で管理されたシリアル ポートを開く</a></p></td>
<td><p>周辺機器は、ドライバーが SerCx2 とシリアル コント ローラーのドライバーによって共同で管理されているシリアル ポート上のデバイスを管理している場合には、ドライバーはこのポートへの論理接続を開くし、ポートを介してデバイスに I/O 要求を送信します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-handling-of-read-and-write-requests.md" data-raw-source="[SerCx2 Handling of Read and Write Requests](sercx2-handling-of-read-and-write-requests.md)">読み取りおよび書き込み要求の処理を SerCx2</a></p></td>
<td><p>周辺機器のドライバーが書き込みを送信します (<a href="https://docs.microsoft.com/previous-versions/ff546904(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))"><strong>IRP_MJ_WRITE</strong></a>) と読み取り (<a href="https://docs.microsoft.com/previous-versions/ff546883(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))"><strong>IRP_MJ_READ</strong></a>) にシリアル コント ローラー上のポートへの要求ポートに接続されている周辺機器とデータを転送します。 SerCx2 がこれらの要求を処理する方法は、要求がタイムアウトまたはが取り消された場合でも、適切に定義されました。</p></td>
</tr>
<tr class="even">
<td><p><a href="reading-data-from-a-sercx2-managed-serial-port.md" data-raw-source="[Reading Data from a SerCx2-Managed Serial Port](reading-data-from-a-sercx2-managed-serial-port.md)">SerCx2 で管理されたシリアル ポートからのデータの読み取り</a></p></td>
<td><p>シリアルのコント ローラー (または UART) 受信 FIFO が通常含まれます。 この FIFO では、シリアル ポートに接続されている周辺機器のデバイスから受信したデータのバッファリング ハードウェア制御を提供します。 このデバイスの周辺機器のドライバーが送信読み取り受信 FIFO からデータを読み取る (<a href="https://docs.microsoft.com/previous-versions/ff546883(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))"><strong>IRP_MJ_READ</strong></a>) のシリアル ポートに要求します。</p></td>
</tr>
</tbody>
</table>

 

 

 




