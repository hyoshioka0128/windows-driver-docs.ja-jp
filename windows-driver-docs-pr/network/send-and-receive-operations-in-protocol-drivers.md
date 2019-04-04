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
ms.openlocfilehash: 388e2e6910487cbf05a992a2a35584c901352048
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575092"
---
# <a name="send-and-receive-operations-in-protocol-drivers"></a>プロトコル ドライバーの送信および受信操作





2 つの異なるインターフェイスの送信し、NDIS プロトコル ドライバーで受信操作があります。 コネクションレスの低い edge 呼び出しでドライバーをプロトコル、 [ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)ネットワーク データを送信する関数。 コネクションレスのプロトコルのドライバーを指定する必要があります、 [ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267)関数。 NDIS 呼び出し*ProtocolReceiveNetBufferLists*基になるコネクションレス ミニポート ドライバーを呼び出すと、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)関数受信したネットワーク データを示します。 コネクションレスのプロトコルのドライバーでのデータの送受信の詳細については、[プロトコル ドライバーの送信と受信操作](protocol-driver-send-and-receive-operations.md)を参照してください。

接続指向の NDIS (いる CoNDIS) プロトコルのドライバーの呼び出し、 [ **NdisCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561728)ネットワーク データを送信する関数。 いる CoNDIS プロトコルのドライバーを指定する必要があります、 [ **ProtocolCoReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570256)関数。 NDIS 呼び出し*ProtocolCoReceiveNetBufferLists*を基になるいる CoNDIS ミニポート ドライバーを呼び出すと、 [ **NdisMCoIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563561)を示すために関数受信したネットワーク データ。 送信と、接続指向プロトコル ドライバーには操作の詳細については、[Connection-Oriented 操作](connection-oriented-operations.md)を参照してください。

送信し、受信操作の概要については、[送信および受信操作](send-and-receive-operations.md)を参照してください。

 

 





