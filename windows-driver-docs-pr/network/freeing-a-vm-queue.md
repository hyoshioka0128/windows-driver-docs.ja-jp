---
title: VM キューの解放
description: VM キューの解放
ms.assetid: 32679638-eeef-4e11-bf56-c96f047e4de7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c17deb842749d18affe722ba3c7a11fda793128d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382767"
---
# <a name="freeing-a-vm-queue"></a>VM キューの解放





上にある、ドライバーの問題を受信キューを解放する、 [OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue) OID 要求のセット。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_キュー\_FREE\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)の種類のキュー id を使用した構造**NDIS\_受信\_キュー\_ID**します。

[OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)を使用して、上にあるドライバーが割り当てられている受信キューの解放、 [OID\_受信\_フィルター\_割り当てる\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue) OID。 受信キューの割り当てに関する詳細については、次を参照してください。 [VM キューを割り当てる](allocating-a-vm-queue.md)します。

**注**  キューの識別子を持つ既定のキューの**NDIS\_既定\_受信\_キュー\_ID**、常に割り当てられているし、することはできません解放されます。

 

上にある、ドライバーは、キューを解放する前にキューに設定するすべてのフィルターを解放する必要があります。 また、上にある、ドライバーを呼び出す前に、ネットワーク アダプターに割り当てられた、すべての受信キューを解放する必要があります、 [ **NdisCloseAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)ネットワーク アダプターへのバインドを閉じます。 NDIS ミニポート ドライバーを呼び出す前に、ネットワーク アダプターに割り当てられているすべてのキューの解放[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数。

ミニポート ドライバーでは、無料のキューに要求を受信したときに、次は。

-   キューに関連付けられている共有メモリのリソースに DMA をすぐに停止する必要があります。

-   DMA が停止したことを示す状態表示を生成します。

-   未処理のすべての待機[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体は、返される、キューに関連付けられています。

-   関連付けられている共有メモリとハードウェア リソースを解放します。

ミニポート ドライバーが受信すると、 [OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)セットの要求キューは、DMA の停止の状態を入力する必要があります、queue とミニポート、DMA が停止しますドライバーを使用して状態の変更を示す必要があります、 [ **NDIS\_状態\_受信\_キュー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)状態を示す値。 キューの状態の詳細については、次を参照してください。[キューの状態と操作](queue-states-and-operations.md)します。

ミニポート ドライバーの問題の後、 [ **NDIS\_状態\_受信\_キュー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)状態を示す値、すべてを待機する、保留中関連付けられている共有メモリを解放できる前に完了する兆候が表示されます。 共有メモリを解放する方法の詳細については、次を参照してください。[共有メモリ リソース割り当て](shared-memory-resource-allocation.md)します。

 

 





