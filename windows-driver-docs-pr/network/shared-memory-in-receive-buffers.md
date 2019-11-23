---
title: 受信バッファー内の共有メモリ
description: 受信バッファー内の共有メモリ
ms.assetid: 3e4d0534-3cbd-40df-b7c1-4f2c15bcd757
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5d917d8e0397f3ebddd0537ec1d30b6ed1936ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841926"
---
# <a name="shared-memory-in-receive-buffers"></a>受信バッファー内の共有メモリ





ここでは、VMQ 受信バッファーの共有メモリのレイアウトについて説明します。受信インジケーターでバッファーを使用する方法の詳細については、「 [VMQ 受信パス](vmq-receive-path.md)」を参照してください。

前のプロトコルドライバーが\_\_\_キューを受け取るように\_設定されている場合は、ndis [ **\_receive\_queue\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体の**Flags**メンバーで、受信したパケットを、要求された先読みサイズ以上のオフセットで分割する必要があります。また、DMA を使用して、別の共有メモリセグメントに先読みデータを転送します。\_\_

ミニポートドライバーは、共有メモリが割り当てられるときに、先読みの種類 (**NdisSharedMemoryUsageReceiveLookahead**) またはその他の共有メモリの種類の設定を指定します。 たとえば、ミニポートドライバーは[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)関数を呼び出し、 [**NDIS\_SHARED\_MEMORY\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)構造体の**Usage**メンバーを**NdisSharedMemoryUsageReceiveLookahead**に設定します。 ミニポートドライバーは、キューの割り当てが完了すると、キューの共有メモリを割り当てる必要があります。 キューの共有メモリリソースの割り当てと解放の詳細については、「[共有メモリリソースの割り当て](shared-memory-resource-allocation.md)」を参照してください。

次の図は、受信データが2つの共有メモリバッファーに分割された場合のネットワークデータの関係を示しています。

![受信データが2つの共有メモリバッファーに分割された場合のネットワークデータの関係を示す図](images/vmqpacket.png)

[**NET\_BUFFER\_共有\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)構造は、共有メモリ情報を指定します。 [**NET\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造に関連付けられている共有メモリバッファーのリンクリストを使用できます。

[**Net\_buffer\_共有\_メモリ\_次の\_セグメント**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-next-segment)、 [**net\_buffer\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-flags)共有\_メモリ\_HANDLE、net\_buffer\_shared\_mem\_[**HANDLE**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-handle)、net\_buffer\_shared\_mem\_HANDLE、net\_BUFFER\_shared\_mem\_[**OFFSET**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-offset)、NET\_buffer\_shared @no__t mem [**LENGTH**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-length)マクロを使用して、net buffer にアクセスしNET\_のバッファー構造内のメモリ (_c)。\_ NET\_バッファー構造の**Sharedmemoryinfo**メンバーには、リンクリスト内の最初の NET\_BUFFER\_共有\_メモリ構造が含まれています。

**注**  NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。 Windows Server 2012 以降では、このプロトコルドライバーでは、ndis **\_receive\_queue\_\_parameters**を設定しません。このフラグは、 [**ndis\_receive\_queue\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体の**Flags**メンバーで、\_を分割\_必要があります。

 

 

 





