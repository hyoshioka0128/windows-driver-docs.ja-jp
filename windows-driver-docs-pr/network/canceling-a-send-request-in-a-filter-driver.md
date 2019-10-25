---
title: フィルター ドライバーでの送信要求のキャンセル
description: フィルター ドライバーでの送信要求のキャンセル
ms.assetid: afa9c8d3-b30b-4009-8428-d31719885154
keywords:
- 送信操作の取り消し (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56476fcc95135bddfbe23ec4e9476e53efa69201
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835279"
---
# <a name="canceling-a-send-request-in-a-filter-driver"></a>フィルター ドライバーでの送信要求のキャンセル





フィルタードライバーは、フィルタードライバーによって送信された、またはそれ以降のドライバーによって生成された送信要求をキャンセルできます。

### <a name="canceling-filter-driver-send-requests"></a>フィルタードライバーの送信要求をキャンセルしています

次の図は、フィルタードライバーによって送信された送信要求を取り消す方法を示しています。

![フィルタードライバーによって送信された送信要求の取り消しを示す図](images/filtercancelsend.png)

フィルタードライバーは、送信操作用に作成する各[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体に対して、 [**net\_buffer\_list\_CANCEL\_ID マクロ\_設定**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-set-net-buffer-list-cancel-id)されている NDIS\_を呼び出します。 NDIS\_SET\_NET\_BUFFER\_LIST\_CANCEL\_ID 関数は、指定されたデータをキャンセル識別子でマークします。

ネットワークデータにキャンセル Id を割り当てる前に、フィルタードライバーは[**NdisGeneratePartialCancelId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid)を呼び出して、割り当てられた各キャンセル id の上位バイトを取得する必要があります。 これにより、ドライバーがシステム内の他のドライバーによって割り当てられたキャンセル Id と重複しないようにすることができます。 ドライバーは通常、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンから**NdisGeneratePartialCancelId**を1回呼び出します。 ただし、ドライバーは**NdisGeneratePartialCancelId**を複数回呼び出すことによって、複数の部分取り消し識別子を取得できます。

マークされた NET\_BUFFER\_リスト構造内のデータの保留中の転送を取り消すには、フィルタードライバーがキャンセル ID を[**NdisFCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcancelsendnetbufferlists)関数に渡します。 ドライバーは、 [**NDIS\_GET\_net\_BUFFER\_LIST\_CANCEL\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)マクロを呼び出すことによって、NET\_バッファー\_リスト構造のキャンセル ID を取得できます。

フィルタードライバーによって、すべての NET\_BUFFER\_リスト構造が同じキャンセル識別子でマークされている場合、 **NdisFCancelSendNetBufferLists**を1回呼び出すだけで保留中のすべての送信を取り消すことができます。 フィルタードライバーによって、NET\_\_BUFFER のサブグループ内の\_すべての\_リスト構造が一意の識別子でマークされている場合、そのサブグループ内のすべての保留中の送信を取り消すことができます。これには、を**1 回呼び出します。NdisFCancelSendNetBufferLists**。

NDIS は、基になるドライバーの cancel send 関数を呼び出します。 保留中の転送を中止すると、基になるドライバーは send complete 関数 (たとえば、 [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)) を呼び出して、NET\_BUFFER\_LIST 構造体を、NDIS の完了ステータスと共に返し\_ステータス\_送信\_中止されました。 さらに、NDIS はフィルタードライバーの[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)関数を呼び出します。

*FilterSendNetBufferListsComplete*では、フィルタードライバーは、\_NET\_BUFFER\_リストに設定されている\_を呼び出し、 *Cancelid*を**NULL**に設定して\_ID を取り消すことができます。 これにより、古いキャンセル ID を使用して、NET\_BUFFER\_リストが誤って誤って使用されるのを防ぐことができます。

### <a name="canceling-send-requests-originated-by-overlying-drivers"></a>他のドライバーによって発生した送信要求のキャンセル

次の図は、前のドライバーによって送信された送信要求を取り消す方法を示しています。

![前のドライバーによって送信された送信要求の取り消しを示す図](images/cancelfiltersend.png)

後続のドライバーは、キャンセル送信機能 ( [**NdisFCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcancelsendnetbufferlists)または[**NdisCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscancelsendnetbufferlists)) を呼び出して、未処理の送信要求を取り消します。 これらのドライバーは、送信要求を行う前に、キャンセル ID を使用してデータの送信をマークする必要があります。

NDIS は、フィルタードライバーの[*Filtercancelsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)関数を呼び出して、指定されたキャンセル識別子でマークされているすべての[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の転送を取り消します。

*Filtercancelsendnetbufferlists*は、次の操作を実行します。

1.  フィルタードライバーのキューに\_格納されている、指定したフィルターモジュールの\_リスト構造体の一覧を走査し、NDIS を呼び出します。 [ **\_NET\_buffer\_list\_\_を取得**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)するには、\_キャンセル ID マクロを取得します。各構造体のキャンセル識別子。 フィルタードライバーは、NDIS が\_NET\_\_BUFFER\_取得するキャンセル ID を比較します。キャンセル\_ID は、NDIS が*Filtercancelsendnetbufferlists*に渡したキャンセル id と共に返されます。

2.  キャンセル識別子が指定したキャンセル id と一致するすべての NET\_BUFFER\_LIST 構造体を、送信キューから削除します。

3.  構造体を返すために、リンクされていないすべての NET\_BUFFER\_LIST 構造体に対して[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数を呼び出します。 フィルタードライバーは、NET\_BUFFER\_LIST 構造体の status フィールドを NDIS\_STATUS に設定し\_送信\_中止されます。

4.  **NdisFCancelSendNetBufferLists**関数を呼び出して、基になるドライバーにキャンセル送信要求を渡します。 フィルタードライバーは、後続のドライバーから受け取ったキャンセル識別子を渡します。 取り消し操作は、ドライバーから送信されたキャンセルの送信操作と同様に処理を続行します。

 

 





