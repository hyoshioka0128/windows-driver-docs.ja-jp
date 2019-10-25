---
title: VMQ 送信パス
description: VMQ 送信パス
ms.assetid: a34f0708-e477-4acc-b854-f00f752be423
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f14901e5e93603019447c4afe9a08435cc07d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842939"
---
# <a name="vmq-transmit-path"></a>VMQ 送信パス





送信要求の場合、このドライバーは[**NET\_BUFFER\_LIST を使用して\_queue\_ID マクロを受信\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id) 、送信データの発信キューのキュー識別子を設定します **。** OOB 情報を NetBufferListFilteringInfo します。 **NetBufferListFilteringInfo**情報は、 [**NDIS\_NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)で指定され、\_INFO 構造体のフィルター選択\_ます。

NDIS ドライバーでは、 [**net\_buffer\_list\_受信\_queue\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)マクロを使用して、 [**net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体のキュー識別子を設定または取得できます。 キューグループに複数の VM キューが含まれている場合は、送信パケットのキュー識別子が、グループ内の任意の VM キューのキュー識別子に設定されている可能性があります。

プロトコルドライバーは、 [**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)関数の*sendflags*パラメーターで\_フラグ\_1 つの\_QUEUE ビットに送信するように NDIS\_設定し、すべての送信 NET\_BUFFER\_LIST を示すように設定します。呼び出しの構造体は、同じ送信キューを対象としています。

ミニポートドライバーは、すべての NET\_を示すために、 [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数の*sendcompleteflags*パラメーターで\_完全な\_フラグ\_1 つの\_キュービットを送信するように NDIS\_設定します。呼び出しのバッファー\_リストが同じ送信キューに送信されました。

フィルターテストの詳細については、「 [VMQ フィルター操作](vmq-filter-operations.md)」を参照してください。

**  、** VMQ が削除されたとき (たとえば、VM ライブマイグレーション中) に、無効な**queueid**値を含む NBL がミニポートドライバーによって受信される可能性があります。 この場合、ミニポートは無効なキュー ID を無視し、代わりに 0 (既定のキュー) を使用します。 **Queueid**は NBL の OOB データの**NetBufferListFilteringInfo**部分にあり、 [**NET\_BUFFER\_LIST\_RECEIVE\_QUEUE\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)マクロを使用して取得されます。

 

 

 





