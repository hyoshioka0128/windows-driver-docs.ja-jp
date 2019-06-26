---
title: ネットワーク データの送信
description: ネットワーク データの送信
ms.assetid: d3b960a7-bd2e-463c-b08b-5c3e4ecc36d0
keywords:
- ネットワーク、WDK のデータを送信します。
- WDK のデータ ネットワーク、送信します。
- WDK のパケットを送信するネットワークを
- WDK ネットワークのデータを送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6853384772288d9c45592d8c518f61cf4feb5fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386841"
---
# <a name="sending-network-data"></a>ネットワーク データの送信





次の図では、プロトコル ドライバー、NDIS、およびミニポート ドライバーは、基本的な送信操作を示しています。

![送信操作の基本的な ndis を示す図](images/netbuffersend.png)

プロトコルのドライバーの呼び出し、 [ **NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists)を送信する関数[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)バインディングで構造体。 NDIS ミニポート ドライバーの呼び出す[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)ネットを転送するように関数\_バッファー\_ミニポート ドライバーの基になるリストの構造体。

すべての NET\_バッファーに基づく送信操作は非同期です。 ミニポート ドライバーの呼び出し、 [ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数は、そのときの適切な状態コード。 各ネットの送信\_バッファー\_リスト構造は個別に完了することができます。 NDIS 呼び出しプロトコル ドライバーの[ **ProtocolSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)関数を各時間、ミニポート ドライバー呼び出し**NdisMSendNetBufferListsComplete**します。

NET の所有権を再利用できるプロトコル ドライバー\_バッファー\_リストの構造体と関連付けられているすべての構造とデータ、NDIS 呼び出しプロトコル ドライバーのようになります*ProtocolSendNetBufferListsComplete*関数。

ミニポート ドライバーまたは NDIS を返すことができます、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)任意の順序で構造体。 プロトコル ドライバーが保証されている一連の[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体は、各ネットワークに接続されている\_バッファー\_リスト構造が変更されていません。

NDIS ドライバーは、NET を分離できます\_バッファーの構造体で、NET\_バッファー\_リスト構造体。 NDIS ドライバーでは、NET で MDLs を区切ることができますも\_バッファーの構造体。 ただし、ドライバーには、NET が返す必要があります常に\_バッファー\_、NET でリストの構造体\_バッファーの構造と元のフォームで MDLs します。 中間のドライバーなど、NET の個別可能性があります\_バッファー\_一覧に 2 つの新しい NET\_バッファー\_構造体を一覧表示し、次のドライバーに、元のデータの一部で渡します。 ただし、中間のドライバーが元 NET の処理を完了する\_バッファー\_一覧の完全な NET を返す必要があります\_バッファー\_元 NET で一覧\_バッファーの構造とMDLs します。

プロトコルのドライバー セット、 **SourceHandle**ネット メンバー\_バッファー\_リスト構造体を*NdisBindingHandle* NDIS がへの呼び出しで提供される、 [ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)関数。 NDIS を使用して、 **SourceHandle**ネットを返すメンバー\_バッファー\_ネット送信プロトコル ドライバーにリストの構造体\_バッファー\_リストの構造体。

中間ドライバーの設定も、 **SourceHandle**ネット メンバー\_バッファー\_リスト構造体を*NdisBindingHandle* への呼び出しで提供されるそのNDIS値**NdisOpenAdapterEx**します。 中間のドライバーでは、送信要求を転送する場合、ドライバーを保存する必要があります、 **SourceHandle**値に書き込みを行う前に提供される上にあるドライバー、 **SourceHandle**メンバー。 NDIS に転送された NET が返されるときに\_バッファー\_中間のドライバーでは、中間のドライバーをリストの構造を復元する必要があります、 **SourceHandle**保存することです。

 

 





