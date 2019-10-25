---
title: CoNDIS ドライバーでの NET_BUFFER 構造の受信
description: CoNDIS ドライバーでの NET_BUFFER 構造の受信
ms.assetid: b3bbd3ef-9206-4edc-8f7a-4ce896d77150
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2558990f10e584eeb8af069788a45bd423157846
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844846"
---
# <a name="receiving-net_buffer-structures-in-condis-drivers"></a>CoNDIS での NET\_バッファー構造の受信





次の図は、プロトコルドライバー、NDIS、およびミニポートドライバーを含む基本的な CoNDIS receive 操作を示しています。

![プロトコルドライバー、ndis、およびミニポートドライバーを含む基本的な condis 受信操作を示す図](images/netbuffercoreceive.png)

上の図に示すように、ミニポートドライバーは[**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)関数を呼び出して、その後のドライバーに対して[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を示します。 ほとんどのミニポートドライバーでは、各 NET\_バッファー構造が別の[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体にアタッチされているため、プロトコルドライバーでは、元の net\_\_buffer のリスト構造のサブセットを作成できます。それらを別のクライアントに転送します。 ただし、NET\_バッファー\_一覧にアタッチされている NET\_バッファー構造の数は、ドライバーによって異なります。

ミニポートドライバーは、すべての NET\_BUFFER\_LIST 構造体をリンクした後、リスト内の最初の NET\_BUFFER\_LIST 構造体へのポインターを**NdisMCoIndicateReceiveNetBufferLists**関数に渡します。 NDIS は、NET\_BUFFER\_LIST 構造体を調べて、指定された仮想接続 (VC) に関連付けられているプロトコルドライバーの[**ProtocolCoReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)関数を呼び出します。 NDIS は、各プロトコルドライバーへの適切なバインドに関連付けられている NET\_BUFFER\_LIST 構造のみを含むリストのサブセットを渡します。

プロトコルドライバーの*ProtocolCoReceiveNetBufferLists*関数の*CoReceiveFlags*パラメーターに、NDIS\_受信\_フラグ\_状態\_リソースフラグが設定されている場合、ndis は NET の所有権を取得し[ **@no__t**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) *ProtocolCoReceiveNetBufferLists*が返された直後の\_構造体を列挙します。

プロトコルドライバーの[**ProtocolCoReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)関数の*CoReceiveFlags*パラメーターに、NDIS\_受信\_フラグ\_状態\_リソースフラグが設定されていない場合、プロトコルドライバーは所有権を保持できます。NET\_BUFFER\_LIST 構造体。 この場合、プロトコルドライバーは、 [**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)関数を呼び出すことによって、NET\_BUFFER\_LIST 構造体を返す必要があります。

ミニポートドライバーで受信リソースが不足している場合は、 [**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)関数の*CoReceiveFlags*パラメーターで、NDIS\_RECEIVE\_FLAGS\_STATUS\_resources フラグを設定できます。 この場合、ドライバーは、 **NdisMCoIndicateReceiveNetBufferLists**がを返すとすぐに、指定されたすべての[**net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造と埋め込みの[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体の所有権を再利用できます。 ミニポートドライバーによって、NDIS\_\_フラグ\_リソースフラグが設定された\_のバッファー構造が示されている場合、プロトコルドライバーはデータをコピーする必要があるため、NDIS を使用せずに\_フラグを受け取る必要があり\_この方法でリソースを利用できます。 ミニポートドライバーは、受信リソースが不足していることを検出し、この状況を回避するために必要なすべての手順を完了する必要があります。

NDIS は、プロトコルドライバーが**NdisReturnNetBufferLists**を呼び出すと、ミニポートドライバーの[*Miniportreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)関数を呼び出します。

**注  :** ミニポートドライバーによって、特定の状態を持つ[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造が示されている場合、NDIS では、同じステータスを使用して、それまでのドライバーに対して NET\_buffer\_list 構造を示す必要はありません。 たとえば、NDIS は、NDIS\_RECEIVE\_FLAGS\_RESOURCES フラグが設定された状態で NET\_BUFFER\_LIST 構造をコピーし、このフラグをオフにした後のドライバーへのコピーを示すことができます。

 

NDIS は、任意の順序で任意の組み合わせで、NET\_BUFFER\_LIST 構造体をミニポートドライバーに返すことができます。 つまり、NDIS が[*Miniportreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)を呼び出すことによってミニポートドライバーに返す、NET\_BUFFER\_list 構造体のリンクリストは、前のさまざまな呼び出し[**からのネットワーク\_バッファー\_リスト構造を持つことができます。NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)。

ミニポートドライバーでは、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**sourcehandle**メンバーを、 **NdisMCoIndicateReceiveNetBufferLists**の*NdisVcHandle*パラメーターと同じ値に設定する必要があります。 そのため、NDIS は、NET\_BUFFER\_LIST 構造体を正しいミニポートドライバーに返すことができます。

また、中間ドライバーは、NET\_BUFFER\_LIST 構造体の**Sourcehandle**メンバーを*NdisVcHandle*値に設定します。 中間ドライバーが受信通知を転送する場合、ドライバー**は sourcehandle メンバーに**書き込む前に、基になるドライバーが提供した**sourcehandle**値を保存する必要があります。 NDIS が転送された NET\_BUFFER\_LIST 構造体を中間ドライバーに返す場合、中間ドライバーは、保存した**Sourcehandle**を復元する必要があります。

 

 





