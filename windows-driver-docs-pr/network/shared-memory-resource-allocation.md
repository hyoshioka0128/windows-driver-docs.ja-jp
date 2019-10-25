---
title: 共有メモリ リソース割り当て
description: 共有メモリ リソース割り当て
ms.assetid: cf030a0f-1202-4d10-b9a1-58d031345678
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d3a77bbd9bfa88a1abaf9aba165bd6e1ac9725b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841922"
---
# <a name="shared-memory-resource-allocation"></a>共有メモリ リソース割り当て





VM キューの共有メモリリソースを割り当てるために、ミニポートドライバーは[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)関数を呼び出します。 たとえば、ミニポートドライバーは、Oid を受信したときに共有メモリを割り当て[\_フィルター\_キュー\_割り当て\_完全な](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)oid を\_します。 また、ネットワークアダプターの初期化中に、ミニポートドライバーが既定のキューに共有メモリを割り当てることもできます。 キューの割り当ての詳細については、「 [VM キューの割り当て](allocating-a-vm-queue.md)」を参照してください。

ミニポートドライバーは、キューが解放されるまで、キューに対してより多くのメモリを割り当てることができます。 キューの解放の詳細については、「 [VM キューの解放](freeing-a-vm-queue.md)」を参照してください。

[**NDIS\_shared\_memory\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)構造体は、共有メモリ割り当て要求の共有メモリパラメーターを指定します。 ミニポートドライバーは、この構造体を[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)関数に渡します。 NDIS は、この構造体を[**NetAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-allocate_shared_memory_handler)関数 (つまり、割り当て\_共有\_メモリ\_ハンドラーエントリポイント) に渡します。

ミニポートドライバーは、共有メモリを割り当てるときに次のことを指定します。

-   キューの識別子。

-   共有メモリの長さ。

-   共有メモリの使用方法。 たとえば、受信バッファーに共有メモリを使用する場合、ミニポートドライバーは**NdisSharedMemoryUsageReceive**を指定します。

NDIS\_共有\_メモリ\_パラメーター\_CONTIGOUS フラグが**Flags**メンバーで設定されていない場合は、連続していないメモリに含まれているスキャッター/ギャザーリストで共有メモリを指定できます。

[**NDIS\_shared\_memory\_USAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ne-ndis-_ndis_shared_memory_usage)列挙体は、共有メモリの使用方法を指定します。 Ndis\_SHARED\_MEMORY\_USAGE 列挙型は、Ndis で使用されています。これは、 [ **\_共有\_メモリ\_のパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)と[**NDIS\_\_LIST\_パラメーターを収集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_scatter_gather_list_parameters)します。構成. VMQ での共有メモリパラメーターの詳細については、「[受信バッファーの共有メモリ](shared-memory-in-receive-buffers.md)」を参照してください。

[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)関数は、次のものを呼び出し元に提供します。

-   割り当てられたメモリの仮想アドレス。

-   スキャッター/ギャザーリスト。

-   共有メモリハンドル-受信通知用。

-   割り当てハンドル-後でメモリを識別するために使用されます。

ミニポートドライバーは、 [**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)関数を呼び出して、キューの共有メモリを解放します。 ミニポートドライバーによって、既定以外のキューの共有メモリが割り当てられている場合、キューを解放しているときに[\_キュー oid\_\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)を使用して、共有メモリが oid のコンテキスト\_解放されます。 ミニポートドライバーは、 [*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数のコンテキストで既定のキューに割り当てられた共有メモリを解放します。

 

 





