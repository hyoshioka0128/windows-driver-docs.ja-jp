---
title: 送信操作のキャンセル
description: 送信操作のキャンセル
ms.assetid: 5bd7a815-4e4d-4259-b322-f4f8d07f2e1a
keywords:
- ネットワーク、WDK のデータを送信します。
- WDK のデータ ネットワーク、送信します。
- WDK のパケットを送信するネットワークを
- WDK ネットワークのデータを送信します。
- NDIS_SET_NET_BUFFER_LIST_CANCEL_ID
- 送信操作の WDK ネットワー キングのキャンセル
- キャンセル Id WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a296150091801eae0b99bee5448427550018c33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382801"
---
# <a name="canceling-a-send-operation"></a>送信操作のキャンセル





次の図は、送信操作の取り消しを示します。

![送信操作のキャンセルを示す図](images/netbuffercancelsend.png)

ドライバーを呼び出し、 [ **NDIS\_設定\_NET\_バッファー\_一覧\_キャンセル\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-set-net-buffer-list-cancel-id)各用のマクロ[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)伝送の下位レベルのドライバーに渡される構造体。 NDIS\_設定\_NET\_バッファー\_一覧\_キャンセル\_ID 関数は、キャンセルの識別子を持つ指定されたパケットをマークします。

パケットにキャンセル Id を割り当てる前に、ドライバーを呼び出す必要があります[ **NdisGeneratePartialCancelId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgeneratepartialcancelid)各キャンセル ID を割り当てることの高位のバイトを取得します。 これにより、ドライバーに取り消しシステム内の他のドライバーによって割り当てられた Id が重複していないこと。 ドライバーを呼び出す通常**NdisGeneratePartialCancelId**から 1 回、 **DriverEntry**ルーチンは呼び出すことで、ドライバーが 1 つ以上の部分取り消し識別子を取得するただし、 **NdisGeneratePartialCancelId** 2 回以上。

マークされたネットワーク内のデータの保留中の転送をキャンセルする\_バッファー\_リスト構造では、ドライバーにキャンセル ID に渡す、 [ **NdisCancelSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscancelsendnetbufferlists)関数。 ドライバーとして使用できるは、NET\_バッファー\_リスト構造体のキャンセルの ID を呼び出して、 [ **NDIS\_取得\_NET\_バッファー\_一覧\_キャンセル\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)マクロ。

場合、ドライバーはすべて[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)同じキャンセル識別子を持つ構造体、を単一の呼び出しで伝送保留中のすべてキャンセルことできます**NdisCancelSendNetBufferLists**します。 場合、ドライバーはすべて NET\_バッファー\_NET のサブグループ リスト構造\_バッファー\_リストの一意の識別子を持つ構造体、保留中のすべての単一の呼び出しでは、そのサブグループ内で伝送キャンセルができます**NdisCancelSendNetBufferLists**します。

NDIS 呼び出し、 [ *MiniportCancelSend* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_send)バインドで適切な下位レベルのドライバーの機能です。 保留中の転送を中止後、基になるミニポート ドライバーを呼び出して、 [ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)を NET を返す関数\_バッファー\_一覧構造体と NDIS の完了ステータス\_状態\_送信\_中止されました。 NDIS、さらに、適切なドライバーの[ **ProtocolSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)関数。

その*ProtocolSendNetBufferListsComplete*関数の場合、プロトコル ドライバーには、NDIS が呼び出すことができます\_設定\_NET\_バッファー\_一覧\_キャンセル\_ID*CancelId*設定**NULL**します。 これにより、NET\_バッファー\_から古いキャンセル ID に置き換えますもう一度使用されている誤って一覧。

 

 





