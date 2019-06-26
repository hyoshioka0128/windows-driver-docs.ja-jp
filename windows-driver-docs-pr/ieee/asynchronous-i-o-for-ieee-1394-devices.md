---
title: IEEE 1394 デバイスの非同期 I/O
description: IEEE 1394 デバイスの非同期 I/O
ms.assetid: 36ca83d9-83ed-4366-81e7-63c5337f8643
keywords:
- IEEE 1394 WDK バス、非同期 I/O
- 1394 WDK バス、非同期 I/O
- 非同期 I/O WDK の IEEE 1394 バス
- I/O WDK の IEEE 1394 バス
- I/O 要求パケット WDK IEEE 1394 バス
- Irp WDK IEEE 1394 バス
- WDK の IEEE 1394 のデータを転送します。
- Pdo WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8222213d51492d3df6b3910a885a424a50deb5b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385787"
---
# <a name="asynchronous-io-for-ieee-1394-devices"></a>IEEE 1394 デバイスの非同期 I/O





IEEE 1394 バス上のデバイス通信、非同期モードのパケットを送受信します。 デバイスは、送信、読み取り、書き込み、および別のデバイスのアドレス空間内の特定のアドレスへの要求をロックします。 受信側のデバイスには、要求が完了すると、サービスの品質を提供するには、応答の受信確認を送信し、送信元デバイスに戻す応答パケットを送信します。

ドライバーは、デバイスに非同期 I/O 要求を送信することによって、そのデバイスに通信できます。 ドライバーは、ホスト コンピューターの IEEE 1394 のアドレス空間のアドレスの範囲を割り当てるし、これらのアドレスに要求を受信することができますも。 次のセクションでは、両方に記載されています。

[IEEE 1394 バス上の非同期 I/O 要求パケットの送信](https://docs.microsoft.com/windows-hardware/drivers/ieee/sending-asynchronous-i-o-request-packets-on-the-ieee-1394-bus)

[IEEE 1394 バス上の非同期 I/O 要求パケットの受信](https://docs.microsoft.com/windows-hardware/drivers/ieee/receiving-asynchronous-i-o-request-packets-on-the-ieee-1394-bus)

 

 




