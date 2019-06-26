---
title: VMQ 受信パス
description: VMQ 受信パス
ms.assetid: e59907fc-94dc-45c4-943d-1628c63961dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca63b811e512e002e6146920d0c608d6082f25e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384353"
---
# <a name="vmq-receive-path"></a>VMQ 受信パス





ネットワーク アダプターは、そのキューに設定されているフィルターのすべてのフィルター フィールドのテストに合格した場合にのみ、キューで受信したパケットを示します。 フィルターの条件の詳細については、次を参照してください。 [VMQ フィルター操作](vmq-filter-operations.md)します。

上位のプロトコル ドライバーに設定する場合、 **NDIS\_受信\_キュー\_パラメーター\_1 秒あたり\_キュー\_受信\_INDICATION**フラグ、**フラグ**のメンバー、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体、ミニポートドライバーを組み合わせる必要がない[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)他の構造を持つキューの受信、 **NET\_バッファー\_一覧**構造体がこのキューに 1 回の呼び出しで、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数。 また、ドライバーを設定する必要があります、 **NDIS\_受信\_フラグ\_単一\_キュー**フラグ、 *ReceiveFlags*のパラメーター、 **NdisMIndicateReceiveNetBufferLists**関数。

場合**NDIS\_受信\_キュー\_パラメーター\_1 秒あたり\_キュー\_受信\_INDICATION**がセットされていなかった、ミニポート ドライバーをリンクできます[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)異なる VM キューからのフレームの構造し、それらを 1 つの呼び出しを示す[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)します。 この場合、指定されたリンク リストの**NET\_バッファー\_一覧**構造体は、キューの数によって並べ替えする必要はありません。 **NET\_バッファー\_一覧**構造の異なるキューは、一緒にグループ化する必要はありません。

プロトコル ドライバーの設定と**NDIS\_返す\_フラグ\_単一\_キュー**し、返しますが、すべてのバッファーを受信、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)内の構造体、 *NetBufferLists*のパラメーター、 [ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)関数は、同じ VM のキューに属している必要があります。 ただし、プロトコルのドライバーをすべて返す必要はありません、 **NET\_バッファー\_一覧**に 1 回の呼び出しで指定された構造体、 [ **ProtocolReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)関数に 1 回の呼び出しで**NdisReturnNetBufferLists**します。 また、返されるリストを含めることができます**NET\_バッファー\_一覧**複数からの構造は受信が同じ VM のキューに属している場合に表示します。

プロトコルのドライバー セット、 **NDIS\_返す\_フラグ\_単一\_キュー**ビットを*ReturnFlags*パラメーターの[ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)ことを示すために、返されたすべて[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)に構造体が属している、同じ VM のキューです。

VMQ 受信表示でバンド (OOB) の情報から、次を含める必要があります、 **NetBufferListInfo**のメンバー、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

-   キューの識別子を指定、 **NetBufferListFilteringInfo**情報。

-   フィルター id の設定、 **NetBufferListFilteringInfo**情報をゼロにします。

**NetBufferListFilteringInfo**で指定されている、 [ **NDIS\_NET\_バッファー\_一覧\_フィルター\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)構造体。 NDIS へのアクセスに\_NET\_バッファー\_一覧\_フィルター\_情報構造、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) OOB データ、NDIS ドライバーの呼び出し、 [ **NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロを指定し、 **NetBufferListFilteringInfo**情報の種類。

フィルターの識別子とキューの id に直接アクセスするには、使用、 [ **NET\_バッファー\_一覧\_受信\_フィルター\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-id)と[ **NET\_バッファー\_一覧\_受信\_キュー\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)マクロ。

VMQ 受信表示の共有メモリ情報を定義する必要があります、 **SharedMemoryInfo**のメンバー、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。

**注**  ときに、VMQ は (たとえば、VM のライブ マイグレーション) 中に削除すると、ミニポート ドライバーを含む無効な NBL を受信する可能性があります**QueueId**値。 この場合、ミニポートする必要があります無効なキューの ID を無視して、0 (既定のキュー) を使用して、代わりにします。 **QueueId**は、 **NetBufferListFilteringInfo** 、NBL の部分の OOB のデータとを使用して取得されて、 [ **NET\_バッファー\_一覧\_受信\_キュー\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)マクロ。

 

いることを示す、 [ **NET\_バッファー\_SHARED\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_shared_memory)ポインターに**SharedMemoryInfo**が有効で、ミニポートドライバーは、NDIS を設定する必要があります\_受信\_フラグ\_SHARED\_メモリ\_情報\_有効なフラグ、 *ReceiveFlags*のパラメーター、[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数。 共有メモリのレイアウトの詳細については、VMQ のバッファーは受信バッファーを参照してください[受信バッファー内の共有メモリ](shared-memory-in-receive-buffers.md)します。

受信の表示では、次の情報を含める必要があります、 [ **NET\_バッファー\_SHARED\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_shared_memory)構造体。

<a href="" id="nextsharedmemorysegment"></a>**NextSharedMemorySegment**  
ポインター [ **NET\_バッファー\_SHARED\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_shared_memory)構造体、 **NULL**-このようなリンクのリストを終了しました構造体。

<a href="" id="sharedmemoryhandle"></a>**SharedMemoryHandle**  
NDIS 共有メモリを処理する[ **NdisAllocateSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatesharedmemory)が返されます。

<a href="" id="sharedmemoryoffset"></a>**SharedMemoryOffset**  
データの共有メモリ バッファーの先頭から開始するバイトのオフセット。

<a href="" id="sharedmemorylength"></a>**SharedMemoryLength**  
共有メモリ セグメントの長さ、(バイト単位)。

上位のプロトコル ドライバーに設定する場合、 **NDIS\_受信\_キュー\_パラメーター\_先読み\_分割\_REQUIRED** フラグ**フラグ**のメンバー、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造、各[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)が含まれています。

-   2 つの MDLs と対応する**SharedMemoryInfo**構造体。

-   バックフィル領域を持つポスト lookahead バッファー。

必要に応じて、プロトコル ドライバーはバックフィル領域に lookahead バッファーの内容をコピーします。 ただし、場合でも、lookahead バッファー全体ではバックフィル領域が存在する必要があります。

上にあるドライバーが設定されていない場合、 **NDIS\_受信\_キュー\_パラメーター\_先読み\_分割\_REQUIRED**フラグ、各[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造には、1 つの MDL と 1 つが含まれます。 **SharedMemoryInfo**構造体。

MDL 内のバイト数とバイト オフセットと**DataLength**と**DataOffset**内のメンバー、 [ **NET\_バッファー\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_data) VMQ を使用していないドライバーの場合と同じ方法で構造が設定されます。 **SharedMemoryLength**と**SharedMemoryOffset**内のメンバー、 **SharedMemoryInfo**構造体を初期化中に 1 回設定することができます。 ミニポート ドライバーを更新する必要はありません、 **SharedMemoryLength**と**SharedMemoryOffset**メンバー上にあるドライバーおよび NDIS、を使用できるため、受信したすべてのパケットを[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer) **DataLength**メンバーと MDL バイト カウントのパケットの開始とサイズを決定します。

**注**  以降 NDIS 6.30 および Windows Server 2012 では、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。 上位のプロトコルのドライバーが設定されていない、 **NDIS\_受信\_キュー\_パラメーター\_先読み\_分割\_REQUIRED**フラグ。

 

 

 





