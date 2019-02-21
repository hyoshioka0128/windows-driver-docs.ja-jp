---
title: SerCx2 で管理されたシリアル ポートを開く
description: 周辺機器は、ドライバーが SerCx2 とシリアル コント ローラーのドライバーによって共同で管理されているシリアル ポート上のデバイスを管理している場合には、ドライバーはこのポートへの論理接続を開くし、ポートを介してデバイスに I/O 要求を送信します。
ms.assetid: CBFE1789-0D60-480A-B467-4690DFF88AAC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a68d07a9106363dd2f126630059d6b875076770c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530229"
---
# <a name="opening-a-sercx2-managed-serial-port"></a>SerCx2 で管理されたシリアル ポートを開く


Windows 8.1、シリアル フレームワークの拡張機能のバージョン 2 で (SerCx2) はシリアル コント ローラーのシリアル ポートを管理するためのシリアル コント ローラー ドライバーと連携して機能を開始します。 周辺機器は、ドライバーが SerCx2 とシリアル コント ローラーのドライバーによって共同で管理されているシリアル ポート上のデバイスを管理している場合には、ドライバーはこのポートへの論理接続を開くし、ポートを介してデバイスに I/O 要求を送信します。

シリアル コント ローラーは、互換性のあるデバイスまたは 16550 ユニバーサル非同期受信側/送信元 (UART) です。 詳細については、次を参照してください。[シリアル コント ローラーのドライバーの概要](serial-drivers-overview.md)します。

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
<td><p><a href="connection-ids-for-serially-connected-peripheral-devices.md" data-raw-source="[Connection IDs for Serially Connected Peripheral Devices](connection-ids-for-serially-connected-peripheral-devices.md)">接続 Id を逐次的に周辺機器を接続</a></p></td>
<td><p>SerCx2 によって管理されているシリアル ポートに接続されている周辺機器のデバイスのドライバーを記述する場合、ドライバーを受信するハードウェア リソースの一覧が含まれています、<em>接続 ID</em>デバイスの接続情報をカプセル化します。プラットフォーム ファームウェア。</p></td>
</tr>
<tr class="even">
<td><p><a href="connecting-a-umdf-peripheral-device-driver-to-a-serial-port.md" data-raw-source="[Connecting a UMDF Peripheral Driver to a Serial Port](connecting-a-umdf-peripheral-device-driver-to-a-serial-port.md)">周辺機器の UMDF ドライバーをシリアル ポートに接続します。</a></p></td>
<td><p>SerCx2 で管理されたシリアル ポートに周辺機器のデバイスの UMDF ドライバーでは、デバイスを操作する特定のハードウェア リソースが必要です。 これらのリソースに含まれるは、ドライバーは、シリアル ポートへの論理接続を開く必要がある情報です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="connecting-a-kmdf-peripheral-device-driver-to-a-serial-port.md" data-raw-source="[Connecting a KMDF Peripheral Driver to a Serial Port](connecting-a-kmdf-peripheral-device-driver-to-a-serial-port.md)">KMDF 周辺のドライバーをシリアル ポートに接続します。</a></p></td>
<td><p>SerCx2 で管理されたシリアル ポート周辺機器の KMDF ドライバーでは、デバイスを操作する特定のハードウェア リソースが必要です。 これらのリソースに含まれるは、ドライバーは、シリアル ポートへの論理接続を開く必要がある情報です。</p></td>
</tr>
</tbody>
</table>

 

 

 




