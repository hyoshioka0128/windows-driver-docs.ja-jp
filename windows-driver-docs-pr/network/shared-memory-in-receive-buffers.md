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

それより前のプロトコルドライバーが\_\_キューを受け取るように設定されている場合は\_先読み\_、Ndis の**Flags**メンバーで\_REQUIRED フラグを分割\_\_を[**受信\_キューに\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造では、ネットワークアダプターは、受信したパケットを、要求された先読みサイズ以上のオフセットで分割し、DMA を使用して先読みデータと先読み後のデータを別々の共有メモリセグメントに転送する必要があります。

ミニポートドライバーは、共有メモリが割り当てられるときに、先読みの種類 (**NdisSharedMemoryUsageReceiveLookahead**) またはその他の共有メモリの種類の設定を指定します。 たとえば、ミニポートドライバーは[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)関数を呼び出し、 [**NDIS\_SHARED\_MEMORY\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)構造体の**Usage**メンバーをに**設定します。NdisSharedMemoryUsageReceiveLookahead**。 ミニポートドライバーは、キューの割り当てが完了すると、キューの共有メモリを割り当てる必要があります。 キューの共有メモリリソースの割り当てと解放の詳細については、「[共有メモリリソースの割り当て](shared-memory-resource-allocation.md)」を参照してください。

次の図は、受信データが2つの共有メモリバッファーに分割された場合のネットワークデータの関係を示しています。

![受信データが2つの共有メモリバッファーに分割された場合のネットワークデータの関係を示す図](images/vmqpacket.png)

[**NET\_BUFFER\_共有\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)構造は、共有メモリ情報を指定します。 [**NET\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造に関連付けられている共有メモリバッファーのリンクリストを使用できます。

[**Net\_buffer\_共有\_メモリ\_次の\_セグメント**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-next-segment)、 [**net\_buffer\_共有\_メモリ\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-flags)、 [**net\_buffer\_共有\_メモリ @no__t_ を使用します。18_ ハンドル**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-handle)、 [**NET\_BUFFER\_共有\_メモリ\_オフセット**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-offset)、および[**net\_BUFFER\_共有\_メモリ\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-length)バッファーにアクセスするために、共有されている\_の\_@noNET\_のバッファー構造に含まれるメモリの __。 NET\_バッファー構造の**Sharedmemoryinfo**メンバーには、リンクリスト内の最初の NET\_BUFFER\_共有\_メモリ構造が含まれています。

**注**  NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。 Windows Server 2012 以降のプロトコルドライバーでは、ndis の**Flags**メンバーで **\_キュー\_パラメーター\_先読み\_分割\_必要**フラグが\_設定されません[ **@no__ _\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体を受け取ります。

 

 

 





