---
title: 受信バッファー内の共有メモリ
description: 受信バッファー内の共有メモリ
ms.assetid: 3e4d0534-3cbd-40df-b7c1-4f2c15bcd757
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0b6d69a3c10a96fcd5f1404ee20dcaa81853555
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384911"
---
# <a name="shared-memory-in-receive-buffers"></a>受信バッファー内の共有メモリ





このセクションでは、共有のレイアウトを記述 VMQ のメモリ バッファーを受信します。受信表示でバッファーの使用の詳細についてを参照してください[VMQ 受信パス](vmq-receive-path.md)します。

上位のプロトコル ドライバーの設定、NDIS 場合\_受信\_キュー\_パラメーター\_先読み\_分割\_で必須フラグ、**フラグ**のメンバー[ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造、ネットワーク アダプターを分割受信パケットのオフセットに等しいまたは先読みアサーションが要求されたサイズと使用 DMA 先読みデータと post 先読みのデータを別の共有メモリ セグメントに転送するよりも大きい。

ミニポート ドライバー先読み型の設定の指定 (**NdisSharedMemoryUsageReceiveLookahead**) または共有メモリを割り当てるときにその他の共有メモリ型。 たとえば、ミニポート ドライバーが呼び出す、 [ **NdisAllocateSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatesharedmemory)関数とセット、**使用状況**内のメンバー、 [ **NDIS\_共有\_メモリ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_shared_memory_parameters)構造体を**NdisSharedMemoryUsageReceiveLookahead**します。 ミニポート ドライバーは、キューの割り当てが完了すると、キューの共有メモリを割り当てる必要があります。 割り当てとキューの共有メモリ リソースの解放については、次を参照してください。[共有メモリ リソース割り当て](shared-memory-resource-allocation.md)します。

次の図は、受信データは 2 つの共有メモリ バッファーに分割するときに、ネットワーク データのリレーションシップを示します。

![受信データは 2 つの共有メモリ バッファーに分割するときは、ネットワーク データのリレーションシップを示す図](images/vmqpacket.png)

[ **NET\_バッファー\_SHARED\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_shared_memory)構造体は、共有メモリ情報を指定します。 関連付けられているこのような共有メモリ バッファーのリンク リストがあります、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。

使用して、 [ **NET\_バッファー\_共有\_MEM\_次\_セグメント**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-next-segment)、 [ **NET\_バッファー\_SHARED\_MEM\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-flags)、 [ **NET\_バッファー\_SHARED\_をメモリ最適化\_処理**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-handle)、 [ **NET\_バッファー\_SHARED\_MEM\_オフセット**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-offset)、および[**NET\_バッファー\_共有\_MEM\_長さ**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-shared-mem-length) NET へのアクセスにマクロ\_バッファー\_SHARED\_、NET メモリ\_バッファーの構造体。 **SharedMemoryInfo** net メンバー\_バッファーの構造体には、最初のネットワークが含まれています。\_バッファー\_SHARED\_リンク リスト内のメモリ構造体。

**注**  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。 Windows Server 2012 以降では、上位のプロトコル ドライバーは未設定、 **NDIS\_受信\_キュー\_パラメーター\_先読み\_分割\_必要な作業**フラグ、**フラグ**のメンバー、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体。

 

 

 





