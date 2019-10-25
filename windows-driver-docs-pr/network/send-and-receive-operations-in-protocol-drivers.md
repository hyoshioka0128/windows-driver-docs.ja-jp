---
title: プロトコル ドライバーの送信および受信操作
description: プロトコル ドライバーの送信および受信操作
ms.assetid: 4759725b-ed0b-4345-9cdc-9411ee29ebdb
keywords:
- プロトコルドライバー WDK ネットワーク, 受信操作
- NDIS プロトコルドライバー WDK、受信操作
- プロトコルドライバー WDK ネットワーク, 送信操作
- NDIS プロトコルドライバー WDK、send 操作
- 送信操作 WDK NDIS プロトコル
- 受信操作 WDK NDIS プロトコル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b02fab051dc6d3c7b1b50a84bff672b54924c52
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841986"
---
# <a name="send-and-receive-operations-in-protocol-drivers"></a>プロトコル ドライバーの送信および受信操作





NDIS プロトコルドライバーでは、送信操作と受信操作に対して2つの異なるインターフェイスがあります。 コネクションレスエッジがあるプロトコルドライバーは、 [**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)関数を呼び出してネットワークデータを送信します。 コネクションレスプロトコルドライバーは、 [**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)関数を提供する必要があります。 基になるコネクションレスなミニポートドライバーが[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を呼び出して受信ネットワークデータを示す場合、NDIS は*ProtocolReceiveNetBufferLists*を呼び出します。 コネクションレスプロトコルドライバーでのデータの送受信の詳細については、「[プロトコルドライバーの送信および受信操作](protocol-driver-send-and-receive-operations.md)」を参照してください。

接続指向 NDIS (CoNDIS プロトコルドライバーは、ネットワークデータを送信するために[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)関数を呼び出します。 CoNDIS プロトコルドライバーは、 [**ProtocolCoReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)関数を提供する必要があります。 基になる*Condis*ドライバーが[**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)関数を呼び出して受信ネットワークデータを示す場合、NDIS はを呼び出します。 接続指向プロトコルドライバーの送信と操作の詳細については、「[接続指向の操作](connection-oriented-operations.md)」を参照してください。

送信操作と受信操作の概要については、「[送信と受信の操作](send-and-receive-operations.md)」を参照してください。

 

 





