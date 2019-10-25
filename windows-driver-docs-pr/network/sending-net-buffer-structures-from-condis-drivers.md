---
title: CoNDIS ドライバーからの NET_BUFFER 構造の送信
description: CoNDIS ドライバーからの NET_BUFFER 構造の送信
ms.assetid: 63bca3f0-b598-4006-bfd0-6df32ab2cbe7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 565b0d2191098af0b3ea667979c32ea65d60379d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841970"
---
# <a name="sending-net_buffer-structures-from-condis-drivers"></a>CoNDIS ドライバーからの NET\_バッファー構造の送信





次の図は、プロトコルドライバー、NDIS、およびミニポートドライバーを含む基本的な CoNDIS 操作を示しています。

![プロトコルドライバー、ndis、およびミニポートドライバーを含む基本的な condis send 操作を示す図](images/netbuffercosend.png)

上の図に示すように、プロトコルドライバーは[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)関数を呼び出して、仮想接続 (VC) で[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を送信します。 次に、NDIS はミニポートドライバーの[**Miniportcosendnetbufferlists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)関数を呼び出して、NET\_BUFFER\_LIST 構造体を基になるミニポートドライバーに転送します。

すべての NET\_バッファーベースの送信操作は非同期です。 したがって、ミニポートドライバーは、常に[**NdisMCoSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcosendnetbufferlistscomplete)関数を呼び出し、データの送信が終了したときに適切な状態コードを提供します。 ミニポートドライバーは、他の NET\_BUFFER\_リスト構造に依存しない、各 NET\_BUFFER\_リスト構造の送信操作を完了できます。 ミニポートドライバーが**NdisMCoSendNetBufferListsComplete**を呼び出すたびに、NDIS はプロトコルドライバーの[**ProtocolCoSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_send_net_buffer_lists_complete)関数を呼び出します。

プロトコルドライバーは、NDIS がプロトコルドライバーの*ProtocolCoSendNetBufferListsComplete*関数を呼び出すとすぐに、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体と、関連するすべての構造およびデータの所有権を再利用できます。

ミニポートドライバーまたは NDIS は、NET\_BUFFER\_LIST 構造体を任意の順序で返すことができます。 ただし、プロトコルドライバーは、各 NET\_バッファー\_の一覧構造にアタッチされている[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造の一覧が変更されていないことが保証されます。

プロトコルドライバーは、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**sourcehandle**メンバーを、 **NdisCoSendNetBufferLists**の*NdisVcHandle*パラメーターと同じ値に設定します。 NDIS は、 **Sourcehandle**メンバーを使用して、NET\_BUFFER\_リスト構造を送信したプロトコルドライバーに、NET\_BUFFER\_list 構造体を返します。

また、中間ドライバーは、NET\_BUFFER\_LIST 構造体の**Sourcehandle**メンバーを*NdisVcHandle*値に設定します。 中間ドライバーが送信要求を転送する場合、ドライバーは、 **sourcehandle**メンバーに書き込む前に、そのドライバーによって提供された**sourcehandle**値を保存する必要があります。 NDIS が転送された NET\_BUFFER\_LIST 構造体を中間ドライバーに返す場合、中間ドライバーは、保存した**Sourcehandle**を復元する必要があります。

プロトコルドライバは、コネクションレスドライバと同じメカニズムを使用して、送信要求を取り消すことができます。 送信要求のキャンセルの詳細については、「[送信操作のキャンセル](canceling-a-send-operation.md)」を参照してください。

 

 





