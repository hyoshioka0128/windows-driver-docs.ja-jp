---
title: CoNDIS WAN ミニポート ドライバーからの受信データの表示
description: CoNDIS WAN ミニポート ドライバーからの受信データの表示
ms.assetid: d49ea741-df5c-4b65-b899-a751cb2b9929
keywords:
- データを受信している CoNDIS WAN のドライバー WDK ネットワーク
- 受信側のデータの WDK ネットワーク
- WDK いる CoNDIS WAN の問題
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf90153d19af7a177a0fc67c123a2e85993ebc0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380900"
---
# <a name="indicating-received-data-from-a-condis-wan-miniport-driver"></a>CoNDIS WAN ミニポート ドライバーからの受信データの表示





次の操作は、いる CoNDIS WAN ミニポート ドライバー ネットワーク データ パケットを受信するときに発生します。

1.  ドライバーは、呼び出す前に必要な場合、ネットワーク データ パケットからドライバー固有のカプセル化を削除[ **NdisMCoIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists) NETで受信したデータを示す\_バッファー\_リスト構造体。 たとえば、ドライバーは、PPPoE カプセル化を削除できます。 ただし、ミニポート ドライバーままようになど、PPP ヘッダーとペイロードのカプセル化されたデータ。

2.  ドライバーの呼び出し、 **NdisMCoIndicateReceiveNetBufferLists** NDISWAN にパケットが届いたことを示す関数。

3.  パケットと呼び出しを処理する NDISWAN [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)をパケットの到着を示すためにします。

4.  パケット、NDIS 呼び出しを転送するように、 [ **ProtocolReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)上にあるバインドのプロトコル ドライバーの関数。

 

 





