---
title: CoNDIS ドライバーでの NET_BUFFER 構造の受信
description: CoNDIS ドライバーでの NET_BUFFER 構造の受信
ms.assetid: b3bbd3ef-9206-4edc-8f7a-4ce896d77150
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8132c97999a461e57d70d9fa128fb3c810fb7a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385425"
---
# <a name="receiving-netbuffer-structures-in-condis-drivers"></a>NET の受信\_いる CoNDIS ドライバーにバッファーの構造体





次の図は、基本的ないる CoNDIS 受信操作で、プロトコル ドライバーには、NDIS、ミニポート ドライバーが含まれます。

![基本的ないる condis を示す図の受信操作で、プロトコル ドライバーには、ndis、ミニポート ドライバーが含まれます](images/netbuffercoreceive.png)

ミニポート ドライバーを呼び出す前の図に示すよう、 [ **NdisMCoIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)関数を示す[ **NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)ドライバーに関連する構造体。 ほとんどのミニポート ドライバーで各 NET\_バッファーの構造体が、個別に接続されている[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)プロトコル ドライバーがサブセットを作成できるように、構造体NET の元のリストの\_バッファー\_構造体を一覧表示し、それらを異なるクライアントに転送します。 ただし、NET 数\_正味にアタッチされているバッファーの構造体\_バッファー\_一覧は、ドライバーによって異なります。

ドライバーがすべてのネットワークをリンクするミニポート後\_バッファー\_リストの構造体、ミニポート ドライバーの最初の NET にポインターを渡します\_バッファー\_リスト構造の一覧で、 **NdisMCoIndicateReceiveNetBufferLists**関数。 NDIS 調べ、NET\_バッファー\_リストの構造体と呼び出し、 [ **ProtocolCoReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)に関連付けられているプロトコル ドライバーの機能、仮想接続 (VC) を指定します。 NDIS NET のみを含むリストのサブセットを通過する\_バッファー\_プロトコル ドライバーごとに、正しいバインディングに関連付けられているリストの構造体。

場合は、NDIS\_受信\_フラグ\_状態\_リソース フラグに設定されて、 *CoReceiveFlags*プロトコル ドライバーのパラメーター *ProtocolCoReceiveNetBufferLists*関数、NDIS を再度獲得の所有権、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)後すぐに構造体*ProtocolCoReceiveNetBufferLists*を返します。

場合は、NDIS\_受信\_フラグ\_状態\_リソースのフラグが設定されていない、 *CoReceiveFlags*プロトコル ドライバーのパラメーター [ **ProtocolCoReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)関数の場合、プロトコル ドライバーには、NET の所有権を保持できます\_バッファー\_リストの構造体。 この場合、プロトコル ドライバーには、NET を返す必要があります\_バッファー\_呼び出すことによってリストの構造体、 [ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)関数。

リソース受信ミニポート ドライバーが不足している場合は、NDIS を設定できます\_受信\_フラグ\_状態\_リソース フラグ、 *CoReceiveFlags* パラメーター[ **NdisMCoIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)関数。 ドライバーが、指定されたすべての所有権を解放する場合、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体し、埋め込み[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体とすぐに**NdisMCoIndicateReceiveNetBufferLists**を返します。 ミニポート ドライバーには、NET が示されている場合\_バッファー構造体、NDIS\_受信\_フラグ\_リソース フラグを設定、NDIS を使用しないように、プロトコル ドライバーは、データをコピーする必要があります\_受信\_フラグ\_この方法でリソース。 ミニポート ドライバーが低いリソースを受信し、このような状況を回避するために必要なすべての手順を完了する必要がある時を検出する必要があります。

NDIS ミニポート ドライバーを呼び出す[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)関数プロトコル ドライバーの呼び出し後**NdisReturnNetBufferLists**します。

**注**  ミニポート ドライバーを示している場合、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)特定ステータスは、NDIS 構造体は、NET を指定する必要はありません\_バッファー\_リスト構造を上にあるドライバーに同じ状態にします。 たとえば、NDIS はコピー、NET\_バッファー\_の構造と、NDIS\_受信\_フラグ\_リソースは、フラグが設定と、このフラグがオフで上にあるドライバーへのコピーを示します。

 

NDIS は、NET を返すことができます\_バッファー\_ミニポート ドライバーと任意の組み合わせで、任意の順序にリストの構造体。 NET のリンクのリストは、\_バッファー\_NDIS を呼び出すことによって、ミニポート ドライバーに返すリスト構造[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists) NETを持つことができます\_バッファー\_以前別の呼び出しからリスト構造[ **NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)します。

ミニポート ドライバーを設定する必要があります、 **SourceHandle**内のメンバー、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造、と同じ値を*NdisVcHandle*パラメーターの**NdisMCoIndicateReceiveNetBufferLists**します。 NDIS は、NET を返せるように\_バッファー\_正しいミニポート ドライバーにリストの構造体。

中間ドライバーの設定も、 **SourceHandle**ネット メンバー\_バッファー\_リスト構造体を*NdisVcHandle*値。 中間のドライバーでは、受信を示す値を転送する場合、ドライバーを保存する必要があります、 **SourceHandle**値に書き込みを行う前に提供される基になるドライバー、 **SourceHandle**メンバー。 NDIS に転送された NET が返されるときに\_バッファー\_中間のドライバーでは、中間のドライバーをリストの構造を復元する必要があります、 **SourceHandle**保存することです。

 

 





