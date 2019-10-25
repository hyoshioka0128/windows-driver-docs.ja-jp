---
title: ネットワーク データの送信
description: ネットワーク データの送信
ms.assetid: d3b960a7-bd2e-463c-b08b-5c3e4ecc36d0
keywords:
- ネットワークデータ WDK、送信
- データ WDK ネットワーク, 送信
- パケット WDK ネットワーク、送信
- データの送信 (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47398fa1404040303dd58fbcacd625ccfbbbe705
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841963"
---
# <a name="sending-network-data"></a>ネットワーク データの送信





次の図は、プロトコルドライバー、NDIS、およびミニポートドライバーを含む基本的な送信操作を示しています。

![基本的な ndis 送信操作を示す図](images/netbuffersend.png)

プロトコルドライバーは、 [**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)関数を呼び出して、[**ネットワーク\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体をバインドに送信します。 NDIS は、ミニポートドライバーの[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数を呼び出して、NET\_BUFFER\_LIST 構造体を基になるミニポートドライバーに転送します。

すべての NET\_バッファーベースの送信操作は非同期です。 ミニポートドライバーは、完了時に適切な状態コードを使用して[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出します。 各 NET\_BUFFER\_リスト構造の送信は、個別に完了できます。 ミニポートドライバーが**NdisMSendNetBufferListsComplete**を呼び出すたびに、NDIS はプロトコルドライバーの[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)関数を呼び出します。

プロトコルドライバーは、NDIS がプロトコルドライバーの*ProtocolSendNetBufferListsComplete*関数を呼び出すとすぐに、NET\_BUFFER\_LIST 構造体と、関連するすべての構造およびデータの所有権を再利用できます。

ミニポートドライバーまたは NDIS は、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を任意の順序で返すことができます。 プロトコルドライバーは、各 NET\_バッファー\_リスト構造にアタッチされている[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造の一覧が変更されていないことを保証します。

NDIS ドライバーでは、net\_BUFFER\_LIST 構造体で、NET\_のバッファー構造を分離できます。 また、すべての NDIS ドライバーは、NET\_のバッファー構造で MDLs を分離することもできます。 ただし、ドライバーは常に、net\_BUFFER 構造体と MDLs を元の形式で使用して、NET\_バッファー\_リスト構造を返す必要があります。 たとえば、中間ドライバーでは、NET\_BUFFER\_リストを2つの新しい NET\_BUFFER\_リスト構造に分割し、元のデータの一部を次のドライバーに渡すことができます。 ただし、中間ドライバーが元の NET\_BUFFER\_リストの処理を完了すると、元の NET\_BUFFER 構造と MDLs を使用して、完全な NET\_BUFFER\_リストを返す必要があります。

プロトコルドライバーは、NET\_BUFFER\_LIST 構造体の**Sourcehandle**メンバーを、 [**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)関数の呼び出しで NDIS が提供した*NdisBindingHandle*に設定します。 NDIS は、 **Sourcehandle**メンバーを使用して、NET\_BUFFER\_リスト構造を送信したプロトコルドライバーに、NET\_BUFFER\_list 構造体を返します。

また、中間ドライバーは、NET\_BUFFER\_LIST 構造体の**Sourcehandle**メンバーを、 *NdisBindingHandle*の呼び出しで提供**された**NDIS の値に設定します。 中間ドライバーが送信要求を転送する場合、ドライバーは、 **sourcehandle**メンバーに書き込む前に、そのドライバーによって提供された**sourcehandle**値を保存する必要があります。 NDIS が転送された NET\_BUFFER\_LIST 構造体を中間ドライバーに返す場合、中間ドライバーは、保存した**Sourcehandle**を復元する必要があります。

 

 





