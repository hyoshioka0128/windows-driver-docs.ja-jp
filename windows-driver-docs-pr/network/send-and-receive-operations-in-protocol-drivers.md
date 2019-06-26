---
title: プロトコル ドライバーの送信および受信操作
description: プロトコル ドライバーの送信および受信操作
ms.assetid: 4759725b-ed0b-4345-9cdc-9411ee29ebdb
keywords:
- ドライバー WDK ネットワーク プロトコル、受信操作
- NDIS は、ドライバー WDK のプロトコル、受信操作
- プロトコル ドライバー WDK ネットワー キング、送信操作
- NDIS は、ドライバー WDK のプロトコル、送信操作
- 送信操作の WDK NDIS プロトコル
- 受信操作の WDK NDIS プロトコル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4495d69d6a7ac2265ed488a484356c8f7cfd7c2d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382105"
---
# <a name="send-and-receive-operations-in-protocol-drivers"></a>プロトコル ドライバーの送信および受信操作





2 つの異なるインターフェイスの送信し、NDIS プロトコル ドライバーで受信操作があります。 コネクションレスの低い edge 呼び出しでドライバーをプロトコル、 [ **NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists)ネットワーク データを送信する関数。 コネクションレスのプロトコルのドライバーを指定する必要があります、 [ **ProtocolReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)関数。 NDIS 呼び出し*ProtocolReceiveNetBufferLists*基になるコネクションレス ミニポート ドライバーを呼び出すと、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数受信したネットワーク データを示します。 コネクションレスのプロトコルのドライバーでのデータの送受信の詳細については、次を参照してください。[プロトコル ドライバーの送信と受信操作](protocol-driver-send-and-receive-operations.md)します。

接続指向の NDIS (いる CoNDIS) プロトコルのドライバーの呼び出し、 [ **NdisCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)ネットワーク データを送信する関数。 いる CoNDIS プロトコルのドライバーを指定する必要があります、 [ **ProtocolCoReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)関数。 NDIS 呼び出し*ProtocolCoReceiveNetBufferLists*を基になるいる CoNDIS ミニポート ドライバーを呼び出すと、 [ **NdisMCoIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)を示すために関数受信したネットワーク データ。 送信と、接続指向プロトコル ドライバーには操作の詳細については、次を参照してください。 [Connection-Oriented 操作](connection-oriented-operations.md)します。

送信し、受信操作の概要については、次を参照してください。[送信および受信操作](send-and-receive-operations.md)します。

 

 





