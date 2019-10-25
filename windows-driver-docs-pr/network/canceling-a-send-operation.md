---
title: 送信操作のキャンセル
description: 送信操作のキャンセル
ms.assetid: 5bd7a815-4e4d-4259-b322-f4f8d07f2e1a
keywords:
- ネットワークデータ WDK、送信
- データ WDK ネットワーク, 送信
- パケット WDK ネットワーク、送信
- データの送信 (WDK ネットワーク)
- NDIS_SET_NET_BUFFER_LIST_CANCEL_ID
- 送信操作の取り消し (WDK ネットワーク)
- キャンセル Id の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a90fbd3b032a8372f1ec8a8e285fc971f45d3ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838211"
---
# <a name="canceling-a-send-operation"></a>送信操作のキャンセル





次の図は、送信操作の取り消しを示しています。

![送信操作の取り消しを示す図](images/netbuffercancelsend.png)

ドライバーは、送信用に下位レベルのドライバーに渡す各[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体に対して、 [**net\_buffer\_list\_CANCEL\_ID マクロ\_設定**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-set-net-buffer-list-cancel-id)されている NDIS\_を呼び出します。 NDIS\_SET\_NET\_BUFFER\_LIST\_CANCEL\_ID 関数は、指定されたパケットにキャンセル識別子をマークします。

パケットにキャンセル Id を割り当てる前に、ドライバーは[**NdisGeneratePartialCancelId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid)を呼び出して、割り当てられた各キャンセル id の上位バイトを取得する必要があります。 これにより、ドライバーがシステム内の他のドライバーによって割り当てられたキャンセル Id と重複しないようにすることができます。 ドライバーは通常、 **Driverentry**ルーチンから**NdisGeneratePartialCancelId**を1回呼び出します。ただし、ドライバーは**NdisGeneratePartialCancelId**を複数回呼び出すことによって、複数の部分取り消し識別子を取得できます。

マークされた NET\_BUFFER\_LIST 構造体に含まれるデータの保留中の転送を取り消すには、ドライバーは[**NdisCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscancelsendnetbufferlists)関数にキャンセル ID を渡します。 ドライバーは、 [**NDIS\_GET\_net\_BUFFER\_LIST\_CANCEL\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)マクロを呼び出すことによって、NET\_バッファー\_リスト構造のキャンセル ID を取得できます。

ドライバーがすべての[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造を同じキャンセル識別子でマークした場合、 **NdisCancelSendNetBufferLists**を1回呼び出すだけで保留中のすべての送信を取り消すことができます。 ドライバーが、一意の識別子を使用して、NET\_\_BUFFER のサブグループ内のすべての\_バッファー\_リスト構造をマークすると、そのサブグループ**内のすべての保留中の送信を取り消すことができます。NdisCancelSendNetBufferLists**。

NDIS は、適切な下位レベルのドライバーの[*Miniportcancelsend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_send)関数をバインドで呼び出します。 保留中の転送を中止すると、基になるミニポートドライバーは[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出して、NET\_バッファー\_リスト構造と、NDIS\_状態の完了ステータスを返し\_送信\_中止されました。 さらに、NDIS は適切なドライバーの[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)関数を呼び出します。

*ProtocolSendNetBufferListsComplete*関数では、プロトコルドライバーは、\_NET\_BUFFER\_リストに設定された NDIS\_を呼び出し、 *Cancelid*を**NULL**に設定して\_ID を取り消すことができます。 これにより、古いキャンセル ID を使用して、NET\_BUFFER\_リストが誤って再使用されるのを防ぐことができます。

 

 





