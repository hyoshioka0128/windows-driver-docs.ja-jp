---
title: プロトコル ドライバーからのデータの送信
description: プロトコル ドライバーからのデータの送信
ms.assetid: f4fa1814-1d8f-49d3-90fb-766b5b17ef28
keywords:
- WDK ネットワークのデータを送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cf94038bb0ed6ab4267dee5502c9b7ce1ad5dae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378649"
---
# <a name="sending-data-from-a-protocol-driver"></a>プロトコル ドライバーからのデータの送信





次の図は、プロトコル ドライバー、NDIS、およびドライバー スタック内の基になるドライバーが含まれますプロトコルのドライバーの送信操作を示しています。

![プロトコル ドライバーを示す図は、プロトコル ドライバー、ndis、およびドライバー スタック内の基になるドライバーの操作を送信します。](images/protocolsend.png)

プロトコルのドライバーの呼び出し、 [ **NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists)関数の一覧で定義されているネットワーク データを送信する[ **NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

プロトコル ドライバーに設定する必要があります、 **SourceHandle**各 net メンバー\_バッファー\_リスト構造体に渡されるのと同じ値を*NdisBindingHandle*パラメーター。 バインド ハンドルは、NDIS を NET を返す必要がある情報を提供します\_バッファー\_プロトコル ドライバーに基になるミニポート ドライバー呼び出しの後にリスト構造[  **。NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)します。

呼び出しの前に**NdisSendNetBufferLists**、プロトコル ドライバーの詳細情報を使用して送信要求を設定できます、 [ **NET\_バッファー\_一覧\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロ。 基になるドライバーは、net には、この情報を取得できます\_バッファー\_一覧\_情報マクロ。

プロトコル ドライバーを呼び出すと、すぐ**NdisSendNetBufferLists**、NET の所有権を渡し、\_バッファー\_リストの構造体と関連付けられているすべてのリソース。 NDIS 呼び出し、 [ **ProtocolSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)プロトコル ドライバーに構造とデータを返す関数。 NDIS は、構造体を収集でき、複数のデータは、NET のシングル リンク リストに要求を送信\_バッファー\_構造体のリストにリストを渡す前に*ProtocolSendNetBufferListsComplete*します。

NDIS 呼び出されるまで*ProtocolSendNetBufferListsComplete*プロトコルがドライバーで開始した送信の現在の状態が不明です。 プロトコル ドライバーが一時的に呼び出すときに、送信要求の割り当て済みがすべてのリソースの所有権を解放**NdisSendNetBufferLists**します。 プロトコル ドライバーが、NET の確認を試みる必要があることはありません\_バッファー\_リストの構造体、またはそのいずれかの関連データを保存 NDIS を構造体を返す前に*ProtocolSendNetBufferListsComplete*します。

*ProtocolSendNetBufferListsComplete*送信操作を完了するために必要な後処理を実行します。 ネットワーク データを送信操作が完了した送信プロトコル ドライバーを要求したなどのプロトコル ドライバーがクライアントに通知できます。

NDIS を呼び出すと*ProtocolSendNetBufferListsComplete*、プロトコル ドライバーには、すべてのネットワークに関連付けられているリソースの所有権を再度獲得\_バッファー\_によって指定されたリストの構造体*NetBufferLists*パラメーター。 *ProtocolSendNetBufferListsComplete*これらのリソースを解放できますか (呼び出すことによって、たとえば、 [ **NdisFreeNetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbuffer)と[ **NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlist)) に後続の呼び出しで再利用できるように準備または**NdisSendNetBufferLists**します。

NDIS 常にデータを送信するプロトコルが指定したネットワーク プロトコルにより決定された順序で基になるミニポート ドライバーに渡されたが**NdisSendNetBufferLists**、基になるドライバーがランダムに送信要求を完了できます順序。 プロトコル ドライバーに渡されるネットワーク データを送信する NDIS にバインドされているプロトコルのすべてのドライバーできます依存は、 **NdisSendNetBufferLists**基になるドライバーを FIFO の順序で。 ただし、プロトコル ドライバーできますで使用して設定を呼び出す、基になるドライバー **NdisMSendNetBufferListsComplete**同じ順序で。

 

 





