---
title: CoNDIS ドライバーからの NET_BUFFER 構造の送信
description: CoNDIS ドライバーからの NET_BUFFER 構造の送信
ms.assetid: 63bca3f0-b598-4006-bfd0-6df32ab2cbe7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84521d3e0cf646a5720f6d3f2153592fed660708
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386843"
---
# <a name="sending-netbuffer-structures-from-condis-drivers"></a>NET の送信\_いる CoNDIS ドライバーからのバッファーの構造体





次の図は、プロトコル ドライバーには、NDIS、ミニポート ドライバーが含まれますが、基本のいる CoNDIS 送信操作を示しています。

![基本的ないる condis を示す図送信操作で、プロトコル ドライバーには、ndis、ミニポート ドライバーが含まれます](images/netbuffercosend.png)

上記の図に示すプロトコル ドライバー呼び出し、 [ **NdisCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)を送信する関数[ **NET\_バッファー\_ボックスの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)仮想接続 (VC) で構造体。 NDIS を呼び出して、ミニポート ドライバーの[ **MiniportCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)ネットを転送するように関数\_バッファー\_ミニポート ドライバーの基になるリストの構造体。

すべての NET\_バッファーに基づく送信操作は非同期です。 ミニポート ドライバーが常に呼び出し、そのため、 [ **NdisMCoSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcosendnetbufferlistscomplete)関数し、処理が完了したら、適切な状態コードは、データを送信します。 ミニポート ドライバーは、各ネットワークの送信操作を完了できる\_バッファー\_他 NET の独立したリスト構造\_バッファー\_リストの構造体。 NDIS 呼び出しプロトコル ドライバーの[ **ProtocolCoSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_send_net_buffer_lists_complete)関数を各時間、ミニポート ドライバー呼び出し**NdisMCoSendNetBufferListsComplete**します。

プロトコル ドライバーの所有権が再利用できる、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造と関連付けられているすべての構造とデータ NDIS 呼び出しプロトコル ドライバーのようになります*ProtocolCoSendNetBufferListsComplete*関数。

NET を返すことができます、ミニポート ドライバーまたは NDIS\_バッファー\_任意の順序でリストの構造体。 プロトコル ドライバーが保証されているが、一連の[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)各ネットワークに接続されている構造\_バッファー\_リスト構造がされていません。変更します。

プロトコルのドライバー セット、 **SourceHandle**内のメンバー、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体と同じ値を*NdisVcHandle*パラメーターの**NdisCoSendNetBufferLists**します。 NDIS を使用して、 **SourceHandle**ネットを返すメンバー\_バッファー\_ネット送信プロトコル ドライバーにリストの構造体\_バッファー\_リストの構造体。

中間ドライバーの設定も、 **SourceHandle**ネット メンバー\_バッファー\_リスト構造体を*NdisVcHandle*値。 中間のドライバーでは、送信要求を転送する場合、ドライバーを保存する必要があります、 **SourceHandle**値に書き込みを行う前に提供される上にあるドライバー、 **SourceHandle**メンバー。 NDIS に転送された NET が返されるときに\_バッファー\_中間のドライバーでは、中間のドライバーをリストの構造を復元する必要があります、 **SourceHandle**保存することです。

プロトコル ドライバーでは、コネクションレス ドライバーとしてのと同じメカニズムを使用して、送信要求をキャンセルできます。 送信要求をキャンセルする詳細については、次を参照してください。[送信操作のキャンセル](canceling-a-send-operation.md)します。

 

 





