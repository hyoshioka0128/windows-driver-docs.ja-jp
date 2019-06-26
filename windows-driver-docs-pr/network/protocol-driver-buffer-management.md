---
title: プロトコル ドライバー バッファー管理
description: プロトコル ドライバー バッファー管理
ms.assetid: 1f91b58e-d432-46c8-994e-d95c3aadfe43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3b9e1cdaf9051879bda926f5049038dafc8309b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385462"
---
# <a name="protocol-driver-buffer-management"></a>プロトコル ドライバー バッファー管理





プロトコル ドライバーを管理する必要があります[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)プール構造体と[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)の構造体のプールは、操作を送信します。 これらのプールを作成するには、ドライバーは、次の関数を呼び出します。

[**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistpool)

[**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferpool)

プロトコル ドライバーでは、次の関数を使用して、構造体をプールから割り当てます。

[**NdisAllocateNetBufferAndNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)

[**NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlist)

[**NdisAllocateNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbuffer)

呼び出す**NdisAllocateNetBufferAndNetBufferList**呼び出しよりも効率的です**NdisAllocateNetBufferList**続けて**NdisAllocateNetBuffer**します。 ただし、 **NdisAllocateNetBufferAndNetBufferList** 1 つのネットワークを作成するだけ\_ネット上のバッファーの構造体\_バッファー\_リスト構造体。 使用する**NdisAllocateNetBufferAndNetBufferList**、ドライバーを設定する必要があります、 *AllocateNetBuffer*パラメーターを**TRUE**呼び出し時に**NdisAllocateNetBufferListPool**します。

プロトコル ドライバーでは、OID 要求を使用して、基になるドライバーの補充とコンテキストの領域の要件をクエリします。 プロトコル ドライバーが補充し、コンテキスト内でバインディング要件を決定する必要があります、*開く*または*再起動*状態。 ドライバーでは、スタック全体のための十分な補充とコンテキストの領域を割り当てる必要があります。 かどうか、必要に応じてプロトコル ドライバーは、解放、プールおよびに再割り当て、*再起動*状態。

プロトコル ドライバーでは、空き、プールに、次の関数を使用します。

[**NdisFreeNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlistpool)

[**NdisFreeNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferpool)します。

プロトコル ドライバーでは、次の関数を使用して、プールから割り当てられている構造体を解放します。

[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlist)

[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbuffer)

ドライバーは、NET を解放する必要があります\_で割り当てられたバッファーの構造体**NdisAllocateNetBuffer**関連付けられている NET を解放する前に\_バッファー\_リスト構造体。 NET\_で割り当てられたバッファーの構造体**NdisAllocateNetBufferAndNetBufferList** 、ドライバーは呼び出し時に解放されます**NdisFreeNetBufferList**関連付けられているネットワークに\_バッファー\_リスト構造体。

 

 





