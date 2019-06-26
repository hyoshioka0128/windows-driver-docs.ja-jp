---
title: ミニポート ドライバー バッファー管理
description: ミニポート ドライバー バッファー管理
ms.assetid: 3b8844e0-9b38-4030-9aec-b713643de523
keywords:
- バッファーの WDK NDIS ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 769e83f5650b687262ecf47da8944de31c2eacdc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373940"
---
# <a name="miniport-driver-buffer-management"></a>ミニポート ドライバー バッファー管理





通常、ミニポート ドライバーを呼び出す[ **NdisAllocateNetBufferListPool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistpool)から[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize) のプールを作成するには[**NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 ミニポート ドライバーでは、これらの構造を使用して、受信したデータを示します。

通常、割り当て、NET ミニポート ドライバー\_バッファー\_リスト構造体を割り当て、1 つのキュー [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer) そのネットワーク上の構造\_バッファー\_リスト構造体。 NET を事前に割り当てられる方が効率的です\_NET のプールを割り当てるときにバッファーが構造体\_バッファー\_NET の割り当てをリストは構造\_バッファー\_リストの構造体と NET\_バッファーが個別に構造体します。

ミニポート ドライバーを呼び出すことができます**NdisAllocateNetBufferListPool**設定と、 *AllocateNetBuffer*パラメーターを**TRUE**ことを示す[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造が事前に割り当てられます。 この場合は、NET\_バッファーの構造が各 NET で事前に割り当てられた\_バッファー\_ドライバーはプールから割り当てリスト構造。 このようなドライバーを呼び出す必要があります[ **NdisAllocateNetBufferAndNetBufferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)構造体をこのプールから割り当てることです。

通常、ミニポート ドライバーを呼び出す**NdisAllocateNetBufferAndNetBufferList**から*MiniportInitializeEx*をそれが必要とする多くのバッファーを割り当てる後続受信操作。 この場合、ドライバーは、空きバッファーの内部リストを管理します。

[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)関数は、返された NET を準備できます\_バッファー\_後ろに続くで再利用するためのリストの構造を示す値を受信します。 *MiniportReturnNetBufferLists*ネットを返すことができます\_バッファー\_プールにリストの構造体 (たとえば、呼び出すでした[ **NdisFreeNetBufferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlist))、プールに返すことがなく、構造を再利用する方が効率的であることができます。

ミニポート ドライバーは、すべての NET を解放する必要があります\_バッファー\_リストの構造体と NDIS アダプターの停止時に関連付けられているデータ。 ドライバーを呼び出すことができます**NdisFreeNetBufferList**構造体を解放して、 [ **NdisFreeNetBufferListPool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlistpool)ネットの解放関数\_バッファー\_プールの一覧。

 

 





