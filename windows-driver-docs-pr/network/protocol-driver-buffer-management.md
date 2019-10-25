---
title: プロトコル ドライバー バッファー管理
description: プロトコル ドライバー バッファー管理
ms.assetid: 1f91b58e-d432-46c8-994e-d95c3aadfe43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9beede3d57e6f9ef741e036e0b3b7c6bc53c6f6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844915"
---
# <a name="protocol-driver-buffer-management"></a>プロトコル ドライバー バッファー管理





プロトコルドライバーは、送信操作のために、[**ネットワーク\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造プールと[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造プールを管理する必要があります。 これらのプールを作成するために、ドライバーは次の関数を呼び出します。

[**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)

[**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferpool)

プロトコルドライバーは、次の機能を使用して、プールから構造を割り当てることができます。

[**NdisAllocateNetBufferAndNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)

[**NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlist)

[**NdisAllocateNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer)

**NdisAllocateNetBufferAndNetBufferList**の呼び出しは、 **NdisAllocateNetBufferList**の後に**NdisAllocateNetBuffer**を呼び出すよりも効率的です。 ただし、 **NdisAllocateNetBufferAndNetBufferList**では、NET\_BUFFER\_LIST 構造体に1つの NET\_バッファー構造だけが作成されます。 **NdisAllocateNetBufferAndNetBufferList**を使用するには、ドライバーが**NdisAllocateNetBufferListPool**を呼び出すときに*allocatenetbuffer*パラメーターを**TRUE**に設定する必要があります。

プロトコルドライバーは、OID 要求を使用して、基になるドライバーのバックフィルとコンテキスト領域の要件を照会できます。 プロトコルドライバーは、*開始*または*再起動*の状態でバインディングのバックフィルとコンテキストの要件を決定する必要があります。 ドライバーは、スタック全体に対して十分なバックフィルとコンテキスト空間を割り当てる必要があります。 必要に応じて、プロトコルドライバーによってプールが解放され、*再起動*中の状態に再割り当てされる可能性があります。

プロトコルドライバーは、次の機能を使用してプールを解放します。

[**NdisFreeNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistpool)

[**NdisFreeNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferpool)。

プロトコルドライバーは、次の機能を使用して、プールから割り当てられた構造体を解放します。

[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)

[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)

関連する NET\_BUFFER\_LIST 構造体を解放する前に、 **NdisAllocateNetBuffer**で割り当てられた NET\_バッファー構造体を解放する必要があります。 **NdisAllocateNetBufferAndNetBufferList**で割り当てられた NET\_バッファー構造は、関連付けられている NET\_BUFFER\_LIST 構造体に対してドライバーが**NdisFreeNetBufferList**を呼び出すと解放されます。

 

 





