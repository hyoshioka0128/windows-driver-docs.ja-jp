---
title: ミニポート ドライバーでの送信要求のキャンセル
description: ミニポート ドライバーでの送信要求のキャンセル
ms.assetid: 9339e661-b91a-49e1-9924-66c85cc80ee8
keywords:
- NdisCancelSendNetBufferLists
- MiniportCancelSend
- 送信要求の取り消し (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6017c2daa559a47de37ca2a018ca8215dc049322
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838213"
---
# <a name="canceling-a-send-request-in-a-miniport-driver"></a>ミニポート ドライバーでの送信要求のキャンセル





次の図は、ミニポートドライバーの [送信の取り消し] 操作を示しています。

![ミニポートドライバーの送信操作をキャンセルする図](images/miniportcancelsend.png)

プロトコル、フィルター、中間ドライバーは、 [**NdisCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscancelsendnetbufferlists)を呼び出して未処理の送信要求を取り消すことができます。 これらのドライバーは、送信要求を行う前に、キャンセル ID を使用してデータの送信をマークする必要があります。

NDIS は、ミニポートドライバーの[*Miniportcancelsend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_send)関数を呼び出して、指定されたキャンセル識別子でマークされているすべての[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の転送を取り消します。

ミニポートドライバーの*Miniportcancelsend*関数は、次の操作を実行します。

1.  指定されたアダプターに対する未処理の送信要求の一覧を走査し、NDIS を呼び出し[ **\_\_net\_buffer\_リストを取得**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)します。\_ID をキャンセルして、各 NET\_buffer のキャンセル識別子を取得\_t_9_ LIST 構造体。 ミニポートドライバーは、NDIS が\_NET\_\_BUFFER\_取得するキャンセル ID を比較し\_キャンセル\_ID は、NDIS が*Miniportcancelsend*に渡すキャンセル id と共に返されます。

2.  取り消し識別子が、未処理の送信要求の一覧から指定された取り消し id と一致するすべての NET\_BUFFER\_LIST 構造体からを削除します。

3.  すべての取り消された NET\_BUFFER\_のリスト構造体を返すために、 [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出します。ミニポートドライバーは、NET\_BUFFER\_LIST 構造体の status フィールドを NDIS\_STATUS に設定し\_送信\_中止されます。

 

 





