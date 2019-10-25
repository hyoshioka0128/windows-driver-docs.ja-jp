---
title: RSS 受信データの表示
description: RSS 受信データの表示
ms.assetid: 8d040d7d-3a8a-4d81-8508-8de225e000ab
keywords:
- 受信側のスケーリング WDK ネットワーク (受信データを示す)
- RSS WDK ネットワーク (受信データを示す)
- 受信データの WDK RSS を示す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77d44d54c6165e6440949c8b133292f5f3587fb0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824612"
---
# <a name="indicating-rss-receive-data"></a>RSS 受信データの表示





ミニポートドライバーは、 [*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)関数から[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を呼び出して、受信したデータを示します。

NIC が RSS ハッシュ値を正常に計算した後、ドライバーは、次のマクロを使用して、ハッシュの種類、ハッシュ関数、およびハッシュ値を[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体に格納する必要があります。

[**NET\_BUFFER\_LIST\_\_HASH\_TYPE に設定します。** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-set-hash-type)

[**ハッシュ\_関数\_設定\_NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-set-hash-function)

[**NET\_BUFFER\_LIST\_\_ハッシュ\_値を設定します。** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-set-hash-value)

ハッシュの種類は、ハッシュを計算する必要がある受信パケットの領域を識別します。 ハッシュの種類の詳細については、「 [RSS ハッシュの種類](rss-hashing-types.md)」を参照してください。 ハッシュ関数は、ハッシュ値の計算に使用される関数を識別します。 ハッシュ関数の詳細については、「 [RSS ハッシュ関数](rss-hashing-functions.md)」を参照してください。 プロトコルドライバーは、初期化時にハッシュの種類と機能を選択します。 詳細については、「 [RSS の構成](rss-configuration.md)」を参照してください。

NIC がハッシュの種類によって指定されたパケットの領域を識別できない場合、ハッシュ計算やスケーリングを実行しないようにする必要があります。 この場合、ミニポートドライバーまたは NIC は、受信したデータを既定の CPU に割り当てる必要があります。

NIC で受信バッファーが不足している場合は、元の受信 DPC が返されるとすぐに各バッファーが返される必要があります。 ミニポートドライバーは、NDIS\_STATUS\_リソースの状態で受信したデータを示すことができます。 この場合、それ以降のドライバーは、バッファー記述子をコピーし、元の保っままの所有権を直ちに取得するための低速パスを経由する必要があります。

ネットワークデータの受信の詳細については、「[ネットワークデータの受信](receiving-network-data.md)」を参照してください。

 

 





