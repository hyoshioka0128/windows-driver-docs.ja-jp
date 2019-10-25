---
title: CoNDIS WAN ミニポート ドライバーからの受信データの表示
description: CoNDIS WAN ミニポート ドライバーからの受信データの表示
ms.assetid: d49ea741-df5c-4b65-b899-a751cb2b9929
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、受信データ
- データを受信する WDK ネットワーク
- WDK CoNDIS WAN を示す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e36610b937f19664b53cc33ecfef15582e82edc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824634"
---
# <a name="indicating-received-data-from-a-condis-wan-miniport-driver"></a>CoNDIS WAN ミニポート ドライバーからの受信データの表示





CoNDIS WAN ミニポートドライバーがネットワークデータパケットを受信すると、次の操作が行われます。

1.  このドライバーは、必要に応じて、ネットワークデータパケットからドライバー固有のカプセル化を削除します。その前に、 [**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)を呼び出して、NET\_BUFFER\_LIST 構造体で受信したデータを示します。 たとえば、ドライバーは、PPPoE カプセル化を削除できます。 ただし、ミニポートドライバーは、PPP ヘッダーやペイロードなど、カプセル化されたデータをそのまま残しておく必要があります。

2.  ドライバーは**NdisMCoIndicateReceiveNetBufferLists**関数を呼び出し、パケットが到着したことを NDISWAN に指示します。

3.  NDISWAN はパケットを処理し、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出してパケットが到着したことを示します。

4.  パケットを転送するために、NDIS はプロトコルドライバーにバインドされた[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)関数を呼び出します。

 

 





