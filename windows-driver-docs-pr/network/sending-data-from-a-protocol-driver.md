---
title: プロトコル ドライバーからのデータの送信
description: プロトコル ドライバーからのデータの送信
ms.assetid: f4fa1814-1d8f-49d3-90fb-766b5b17ef28
keywords:
- データの送信 (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d62a59ae9aec083551fd4783a8b0d40f223790f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841974"
---
# <a name="sending-data-from-a-protocol-driver"></a>プロトコル ドライバーからのデータの送信





次の図は、プロトコルドライバー、NDIS、およびドライバースタック内の基になるドライバーを含むプロトコルドライバーの送信操作を示しています。

![プロトコルドライバーの送信操作を示す図 (プロトコルドライバー、ndis、およびドライバースタック内の基になるドライバーが含まれます)](images/protocolsend.png)

プロトコルドライバーは、 [**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)関数を呼び出して、 [**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の一覧に定義されているネットワークデータを送信します。

プロトコルドライバーでは、各 NET\_BUFFER\_LIST 構造体の**Sourcehandle**メンバーを、 *NdisBindingHandle*パラメーターに渡されるのと同じ値に設定する必要があります。 このバインディングハンドルは、基になるミニポートドライバーが[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)を呼び出した後に、NDIS が NET\_BUFFER\_LIST 構造体をプロトコルドライバーに返すために必要な情報を提供します。

**NdisSendNetBufferLists**を呼び出す前に、プロトコルドライバーは、送信要求に付随する情報を、 [**NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロに設定できます。 基になるドライバーは、NET\_BUFFER\_LIST\_INFO マクロを使用してこの情報を取得できます。

プロトコルドライバーが**NdisSendNetBufferLists**を呼び出すと、その直後に、NET\_BUFFER\_リスト構造とすべての関連リソースの所有権が放棄されます。 NDIS は、 [**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)関数を呼び出して、構造体とデータをプロトコルドライバーに返します。 NDIS では、 *ProtocolSendNetBufferListsComplete*にリストを渡す前に、複数の送信要求の構造とデータを、NET\_BUFFER\_リスト構造の1つのリンクリストに収集できます。

NDIS が*ProtocolSendNetBufferListsComplete*を呼び出すまでは、プロトコルドライバーで開始された送信の現在の状態は不明です。 プロトコルドライバーは、 **NdisSendNetBufferLists**を呼び出すときに、送信要求に割り当てられたすべてのリソースの所有権を一時的に解放します。 プロトコルドライバーは、NDIS が構造体を*ProtocolSendNetBufferListsComplete*に返す前に、NET\_BUFFER\_LIST 構造体または関連するデータを調べようとしてはなりません。

*ProtocolSendNetBufferListsComplete*は、送信操作を完了するために必要なすべての後処理を実行します。 たとえば、プロトコルドライバーは、送信操作が完了したことをプロトコルドライバーに要求したことをクライアントに通知できます。

NDIS が*ProtocolSendNetBufferListsComplete*を呼び出すと、プロトコルドライバーは、 *NetBufferLists*パラメーターで指定されている、NET\_BUFFER\_リスト構造に関連付けられているすべてのリソースの所有権を取得します。 *ProtocolSendNetBufferListsComplete*は、これらのリソース (たとえば、 [**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)と[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)を呼び出すことによって) を解放するか、 **NdisSendNetBufferLists**への後続の呼び出しで再利用できるように準備することができます。

NDIS では、プロトコルによって提供されるネットワークデータを、プロトコルによって指定された順序で、 **NdisSendNetBufferLists**に渡された順序で常に送信しますが、基になるドライバーは、ランダムな順序で送信要求を完了できます。 つまり、すべてのバインドされたプロトコルドライバーは、プロトコルドライバーが**NdisSendNetBufferLists**に渡すネットワークデータを、基になるドライバーに対して FIFO の順序で送信するように NDIS に依存できます。 ただし、プロトコルドライバーは、基になるドライバーを使用して同じ順序で**NdisMSendNetBufferListsComplete**を呼び出すことはできません。

 

 





