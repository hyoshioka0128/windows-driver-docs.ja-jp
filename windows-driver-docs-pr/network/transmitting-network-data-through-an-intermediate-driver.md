---
title: 中間ドライバー経由のネットワーク データの転送
description: 中間ドライバー経由のネットワーク データの転送
ms.assetid: 90759322-810b-47fd-896c-465c96be4cdd
keywords:
- 中間ドライバー WDK ネットワーク、データの送信
- NDIS 中間ドライバー WDK、データの送信
- ネットワーク データを送信
- WDK NDIS 中間のデータを転送します。
- WDK NDIS 中間のデータを転送します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62ac6cad007a0af7fc8f9d836207369250e3764b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368452"
---
# <a name="transmitting-network-data-through-an-intermediate-driver"></a>中間ドライバー経由のネットワーク データの転送





説明したよう[ミニポート ドライバーとして中間のドライバーを登録する](registering-an-intermediate-driver-as-a-miniport-driver.md)、中間のドライバーを提供する必要があります、 [ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)関数と、登録[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)します。 *MiniportSendNetBufferLists*関数は、着信を転送できる[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)呼び出して構造[**NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists)場合、ドライバーはコネクションレスの下端。 *MiniportSendNetBufferLists* NET の一覧を送信できる\_バッファー\_リストの構造体を受け取る**NdisSendNetBufferLists**基になるミニポートの機能に関係なくドライバー。

*MiniportSendNetBufferLists* NET の一覧を受信\_バッファー\_リストの構造体の後続の呼び出し元によって定義された順序で配置された**NdisSendNetBufferLists**します。 ほとんどの場合、中間のドライバーが保持この順序 NET の受信の配列が渡されます\_バッファー\_基になるミニポート ドライバーにリストの構造体。 基になるドライバーに渡す前に、ネットワーク データでデータを変更する中間のドライバーでは、一覧を並べ替えることができます。

NDIS の順序を常に維持[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)ポインターへのリンク リストとして渡された構造体**NdisSendNetBufferLists**. 基になるミニポート ドライバーは、そのリストに渡されるも想定しています。 その*MiniportSendNetBufferLists*関数では、同じ順序でネットワーク データを送信する必要があることを意味します。

 

 





