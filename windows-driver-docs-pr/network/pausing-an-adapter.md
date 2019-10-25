---
title: アダプターの一時停止
description: アダプターの一時停止
ms.assetid: e24a9886-a1d7-4ca5-bed8-85db4a49ed9c
keywords:
- ミニポートアダプター WDK ネットワーク、一時停止
- WDK ネットワークのアダプター、一時停止
- 状態 WDK ネットワークの一時停止
- 一時停止状態 WDK ネットワーク
- MiniportPause
- ミニポートアダプターの一時停止
- ミニポートアダプターの停止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 844dfce6909bd237e14c7f16d34df157a5a55d30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843695"
---
# <a name="pausing-an-adapter"></a>アダプターの一時停止





NDIS は、ミニポートドライバーの[*Miniportpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)関数を呼び出して、一時停止操作を開始します。 一時停止操作が完了するまで、アダプターは一時停止状態のままになります。

一時停止中の状態では、ミニポートドライバーは未処理の受信操作を完了する必要があります。 また、ドライバーは未処理の送信操作を完了する必要があり、新しい送信要求をすべて拒否する必要があります。

受信操作を完了するために、ドライバーは[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数へのすべての呼び出しが返されるまで待機し、NDIS はすべての未処理の[**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体をミニポートドライバーの[*に返す必要があります。MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)関数。

未処理の送信操作を完了するには、ミニポートドライバーが、未処理のすべての NET\_BUFFER\_LIST 構造体に対して[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出す必要があります。 ドライバーは、 [*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数に対して行われた新しい送信要求を直ちに拒否する必要があります。

ミニポートドライバーがすべての未処理の送信および受信操作を完了した後、ドライバーは、同期または非同期のいずれかの方法で一時停止要求を完了する必要があります。 一時停止操作が非同期に完了した場合、ドライバーは[**NdisMPauseComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismpausecomplete)を呼び出して一時停止要求を完了します。 一時停止要求を完了すると、ミニポートドライバーが一時停止状態になります。

ミニポートドライバーが一時停止状態にある間、NDIS は、停止、初期化、電源変更、再起動などのプラグアンドプレイ操作を開始しません。 ミニポートドライバーが一時停止状態になった後、NDIS はこれらのプラグアンドプレイ操作を開始できます。

 

 





