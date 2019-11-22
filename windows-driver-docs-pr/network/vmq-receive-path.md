---
title: VMQ 受信パス
description: VMQ 受信パス
ms.assetid: e59907fc-94dc-45c4-943d-1628c63961dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 449ee68618e1e53d2fd0195f66bd7026db57dbf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842944"
---
# <a name="vmq-receive-path"></a>VMQ 受信パス





ネットワークアダプターは、キューに設定されているフィルターのすべてのフィルターフィールドテストに合格した場合にのみ、受信パケットがキューにあることを示します。 フィルターテストの詳細については、「 [VMQ フィルター操作](vmq-filter-operations.md)」を参照してください。

前のプロトコルドライバーが **\_キューに\_\_パラメーターを受け取る**ように\_設定している場合、 [**ndis\_receive\_queue\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体の**Flags**メンバーで\_表示フラグを受信します。この場合、ミニポートドライバーは、このキューの**net\_buffer\_リスト**構造を使用して、他の受信キューに対して[**net\_buffer\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) list 構造体を混在さ[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を呼び出します。\_\_ また、ドライバーは、 **NdisMIndicateReceiveNetBufferLists**関数の*receiveflags*パラメーターで、 **NDIS\_RECEIVE\_FLAGS\_SINGLE\_QUEUE**フラグを設定する必要があります。

**NDIS\_が\_queue\_パラメーターを受信**した場合\_キューごとに\_のパラメーターが設定されていないと、ミニポートドライバーは、フレームに対して[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体をリンクできます。VM キューが異なる場合は、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)の1回の呼び出しで指定します。\_\_ この場合、指定された**NET\_BUFFER\_リスト**構造のリンクリストは、キュー番号で並べ替える必要はありません。 異なるキューの **\_の\_バッファー**をグループ化する必要はありません。

プロトコルドライバーが\_NDIS を設定すると、 **1 つの\_キュー\_\_フラグが返さ**れ、受信バッファー*が返され*ます。このとき、すべての[**NET\_BUFFER\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)関数は、同じ VM キューに属している必要があります。 ただし、 **NdisReturnNetBufferLists**の1回の呼び出しで、 [**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)関数の1回の呼び出しで示されたすべての**NET\_BUFFER\_LIST**構造体を返すためにプロトコルドライバーは必要ありません。 また、返された一覧には、同じ VM キューに属している場合、複数の受信通知からの**NET\_BUFFER\_list**構造を含めることができます。

プロトコルドライバーは、返されたすべての NET\_BUFFER を示すために、 [**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)の*returnflags*パラメーターで **\_フラグ\_1 つの\_QUEUE**ビットを返すように NDIS\_設定し[ **\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造は同じ VM キューに属しています。

VMQ の受信確認には、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**NetBufferListInfo**メンバーに次の帯域外 (OOB) 情報が含まれている必要があります。

-   **NetBufferListFilteringInfo**情報でキュー識別子を指定します。

-   **NetBufferListFilteringInfo**情報のフィルター識別子を0に設定します。

**NetBufferListFilteringInfo**情報は、 [**NDIS\_NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)で指定され、\_INFO 構造体のフィルター選択\_ます。 NDIS\_NET\_バッファー\_一覧にアクセスするには\_[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)内の\_INFO 構造をフィルター処理して、OOB データを一覧表示する\_、NDIS ドライバーは[**net\_buffer\_list を呼び出し\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロおよび**NetBufferListFilteringInfo**情報の種類を指定します。

フィルター識別子とキュー識別子に直接アクセスするには、 [**net\_buffer\_list を使用して\_フィルター\_id**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-id)と[**net\_BUFFER\_list\_receive\_queue\_ID を受け取る\_ます。** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)マクロ。

VMQ 受信インジケーターは、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造の**sharedmemoryinfo**メンバーで共有メモリ情報を定義する必要があります。

**  、** VMQ が削除されたとき (たとえば、VM ライブマイグレーション中) に、無効な**queueid**値を含む NBL がミニポートドライバーによって受信される可能性があります。 この場合、ミニポートは無効なキュー ID を無視し、代わりに 0 (既定のキュー) を使用します。 **Queueid**は NBL の OOB データの**NetBufferListFilteringInfo**部分にあり、 [**NET\_BUFFER\_LIST\_RECEIVE\_QUEUE\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)マクロを使用して取得されます。

 

**Sharedmemoryinfo**の[**NET\_BUFFER\_shared\_MEMORY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)ポインターが有効であることを示すには、ミニポートドライバーで、NDIS\_受信\_フラグ\_共有\_メモリ\_情報を受け取るように設定する必要があり @no_[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数の*receiveflags*パラメーターに _t_11_ 有効なフラグが指定されています。\_ VMQ 受信バッファーの共有メモリバッファーのレイアウトの詳細については、「[受信バッファーの共有メモリ](shared-memory-in-receive-buffers.md)」を参照してください。

受信を示すには、 [**NET\_BUFFER\_共有\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)構造に次の情報が含まれている必要があります。

<a href="" id="nextsharedmemorysegment"></a>**NextSharedMemorySegment**  
このような構造体の**NULL**で終わるリンクリストにある、次の[**NET\_バッファー\_共有\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_shared_memory)構造体へのポインター。

<a href="" id="sharedmemoryhandle"></a>**SharedMemoryHandle**  
[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)が返す NDIS 共有メモリハンドル。

<a href="" id="sharedmemoryoffset"></a>**SharedMemoryOffset**  
共有メモリバッファーの先頭からのデータの開始位置を示すバイト単位のオフセット。

<a href="" id="sharedmemorylength"></a>**SharedMemoryLength**  
共有メモリセグメントの長さ (バイト単位)。

前のプロトコルドライバーが **\_\_\_キューを受け取る**ように設定されている場合は、\_受信\_キューの\_[**パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造の**Flags**メンバーで\_REQUIRED フラグを分割して、各[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)に次のように入力します。\_\_

-   2つの MDLs および対応する**Sharedmemoryinfo**構造体。

-   バックフィル領域を含む事後先読みバッファー。

必要に応じて、プロトコルドライバーは先読みバッファーの内容をバックフィル領域にコピーします。 ただし、パケットがすべて先読みバッファー内にある場合でも、バックフィル領域が存在している必要があります。

追加されたドライバーが**NDIS\_RECEIVE\_\_QUEUE**を設定していない場合\_必要なフラグを分割\_には、各[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体に1つの MDL と1つ**が含まれます。SharedMemoryInfo**構造体。\_

MDL を使用しないドライバーに設定されている場合と同じ方法で、MDL のバイト数とバイトオフセット、および[ **\_バッファー\_のデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)構造の**DataLength**および**DataOffset**メンバーが設定されます。 **Sharedmemorylength**構造体の**sharedmemorylength**メンバーと**sharedmemorylength**メンバーは、初期化中に1回設定できます。 ミニミニデバイスドライバーと NDIS は[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) **DataLength**を使用できるため、受信されるすべてのパケットに対して、 **Sharedmemorylength**および**sharedmemorylength**メンバーを更新する必要はありません。メンバーと MDL バイト数を調べて、パケットの開始とサイズを決定します。

**注**  NDIS 6.30 および Windows Server 2012 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。 前のプロトコルドライバーでは、 **\_キュー\_\_パラメーターを受け取るように NDIS\_** 設定されません。このフラグは、必要に応じて\_を分割\_ます。

 

 

 





