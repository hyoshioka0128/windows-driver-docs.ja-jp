---
title: ミニポート ドライバー バッファー管理
description: ミニポート ドライバー バッファー管理
ms.assetid: 3b8844e0-9b38-4030-9aec-b713643de523
keywords:
- バッファー WDK NDIS ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec22e69bb4b068aba0959651d54a80a67626bc81
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844239"
---
# <a name="miniport-driver-buffer-management"></a>ミニポート ドライバー バッファー管理





ミニポートドライバーは、通常、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)から[**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)を呼び出して、 [**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のプールを作成します。 ミニポートドライバーは、これらの構造体を使用して受信したデータを示します。

通常、ネットワーク\_バッファー\_リスト構造を割り当てるミニポートドライバーは、その NET\_BUFFER\_LIST 構造体に1つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体を割り当て、キューに入れます。 Net\_BUFFER\_LIST 構造体と NET\_BUFFER 構造体を別々に割り当てるよりも、net\_バッファー\_リスト構造のプールを割り当てるときは、NET\_バッファー構造を事前に割り当てることをお勧めします。

ミニポートドライバーは**NdisAllocateNetBufferListPool**を呼び出し、 *Allocatenetbuffer*パラメーターを**TRUE**に設定して、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造が事前に割り当てられていることを示すことができます。 この場合、ネットワーク\_のバッファー構造は、ドライバーがプールから割り当てた各 NET\_BUFFER\_LIST 構造体で事前に割り当てられます。 このようなドライバーは、 [**NdisAllocateNetBufferAndNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)を呼び出して、このプールから構造体を割り当てる必要があります。

通常、ミニポートドライバーは、 *MiniportInitializeEx*から**NdisAllocateNetBufferAndNetBufferList**を呼び出して、後続の受信操作に必要な数だけバッファーを割り当てます。 この場合、ドライバーは空きバッファーの内部リストを管理します。

[*Miniportreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)関数は、返された NET\_BUFFER\_LIST 構造体を準備して、後続の受信通知で再利用することができます。 *Miniportreturnnetbufferlists*は、NET\_BUFFER\_LIST 構造体をプールに返すことができますが (たとえば、 [**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)を呼び出すことができます)、構造体を再利用する方が効率的です。プール。

NDIS がアダプターを停止すると、ミニポートドライバーは、すべての NET\_バッファー\_リスト構造および関連データを解放する必要があります。 ドライバーは、 **NdisFreeNetBufferList**を呼び出して構造体を解放し、 [**NdisFreeNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistpool)関数を呼び出して、NET\_BUFFER\_LIST プールを解放できます。

 

 





