---
title: フィルター ドライバー バッファー管理
description: フィルター ドライバー バッファー管理
ms.assetid: 92b38710-056d-4853-b266-ca86cee298b6
keywords:
- フィルタードライバーの WDK ネットワーク、バッファー
- NDIS フィルタードライバー WDK、バッファー
- バッファー管理 WDK NDIS フィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc005aed82bcccddb48598e810d85312f1708db9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834731"
---
# <a name="filter-driver-buffer-management"></a>フィルター ドライバー バッファー管理





フィルタードライバーは、他のドライバーから取得したネットワークデータをコピーしたり、送信操作または受信操作を開始したりするためのバッファーを作成します。

フィルタードライバーがバッファーを作成しない場合、ドライバーはバッファープールを管理しません。 このようなドライバーは、他のドライバーから受け取ったバッファーを単に渡すだけです。

送信操作または受信操作をサポートするバッファーを作成するフィルタードライバーは、 [**net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造プールと[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造プールを管理する必要があります。

これらのプールを作成するために、ドライバーは次の関数を呼び出します。

[**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)

[**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferpool)

フィルタードライバーは、次の関数を使用して、プールから構造を割り当てることができます。

[**NdisAllocateNetBufferAndNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)

[**NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlist)

[**NdisAllocateNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer)

**NdisAllocateNetBufferAndNetBufferList**の呼び出しは、 **NdisAllocateNetBufferList**の後に**NdisAllocateNetBuffer**を呼び出すよりも効率的です。 ただし、 **NdisAllocateNetBufferAndNetBufferList**では、NET\_BUFFER\_LIST 構造体に1つの NET\_バッファー構造だけが作成されます。 **NdisAllocateNetBufferAndNetBufferList**を使用するには、ドライバーが**NdisAllocateNetBufferListPool**を呼び出すときに*allocatenetbuffer*パラメーターを**TRUE**に設定する必要があります。

送信要求を発信するフィルタードライバーは、基になるドライバーのコンテキストとバックフィル領域の要件を決定する必要があります。 フィルタードライバーは、再起動属性を使用して、基になるドライバーのバックフィル要件を決定します。 フィルタードライバーは、*再起動*状態のバックフィルとコンテキストの要件を決定する必要があります。 ドライバーは、スタック全体に対して十分なバックフィルとコンテキスト空間を割り当てる必要があります。 必要に応じて、フィルタードライバーはプールを解放し、*再起動*中の状態に再割り当てすることができます。

フィルタードライバーは、次の機能を使用してプールを解放します。

[**NdisFreeNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistpool)

[**NdisFreeNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferpool)

フィルタードライバーは、次の関数を使用して、プールから割り当てられた構造体を解放します。

[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)

[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)

関連する NET\_BUFFER\_LIST 構造体を解放する前に、 **NdisAllocateNetBuffer**で割り当てられた NET\_バッファー構造体を解放する必要があります。 **NdisAllocateNetBufferAndNetBufferList**で割り当てられた NET\_バッファー構造は、関連付けられている NET\_BUFFER\_LIST 構造体に対してドライバーが**NdisFreeNetBufferList**を呼び出すと解放されます。

 

 





