---
title: リセット
description: リセット
ms.assetid: 5f37eca3-08b6-4bac-9d02-8a8ebd8c1904
keywords:
- 接続指向の NDIS WDK、Nic のリセット
- ネットワーク、Nic のリセット
- NIC WDK ネットワークをリセットしています
- Nic WDK ネットワーク、リセット
- ネットワークインターフェイスカード WDK ネットワーク、リセット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b764236031721dcbbff8d3e9be5d621b96bd44d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842029"
---
# <a name="reset"></a>リセット





NDIS は、ミニポートドライバーまたは MCM ドライバーの[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数を呼び出して NIC をリセットする場合があります。

リセットがアクティブになり、リセット後に有効になる前に、有効で有効な AF、SAP、および VC ハンドル  に**注意**してください。

 

次の図は、ミニポートドライバーにリセット要求を発行するクライアントを示しています。

![ミニポートドライバーにリセット要求を発行しているクライアントを示す図](images/cm-27.png)

次の図は、MCM ドライバーにリセット要求を発行するクライアントを示しています。

![mcm ドライバーにリセット要求を発行しているクライアントを示す図](images/fig1-26.png)

基になる接続指向ドライバーによって NIC がリセットされると、ndis は、プロトコルの[**Protocolcostatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)関数を NDIS\_STATUS を使用して呼び出し、\_リセット\_開始することで、各プロトコルに通知します。

ミニポートドライバーまたは MCM ドライバーの NIC がリセットされている間、NDIS は、ミニポートドライバーまたは MCM ドライバーへのプロトコルで開始された送信と要求を受け入れません。 リセットの実行中は、プロトコルドライバーが[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)を使用してミニポートドライバーにパケットを送信したり、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を使用してミニポートドライバーから情報を要求したりすることはできません。

*Miniportresetex*は、NIC をリセットするために必要なデバイスに依存するアクションを実行します。 *Miniportresetex*は同期的に完了できます。または、 [**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)の呼び出しで非同期に完了できます。

-   リセットが同期的に完了した場合、NDIS は、バインドされたプロトコルの*Protocolcostatusex*関数を NDIS\_STATUS で呼び出し、\_の終了\_リセットします。

-   リセットが非同期に完了した場合、NDIS は、バインドされたプロトコルの*Protocolcostatusex*関数を NDIS\_STATUS を使用して呼び出し、\_の終了\_リセットします。

 

 





