---
title: フィルター モジュールの一時停止
description: フィルター モジュールの一時停止
ms.assetid: da75b92d-b662-416a-b350-e5384b870b7f
keywords:
- フィルターモジュール WDK ネットワーク、一時停止
- フィルターモジュールの一時停止
- フィルタードライバーの WDK ネットワーク、一時停止フィルターモジュール
- NDIS フィルタードライバー WDK、一時停止フィルターモジュール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39eb86805043c4020ee254ed9df8fb8fbc746782
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843697"
---
# <a name="pausing-a-filter-module"></a>フィルター モジュールの一時停止





実行中のフィルターモジュールを一時停止するために、NDIS はフィルタードライバーの[*Filterpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)関数を呼び出します。 フィルターモジュールは、 *Filterpause*関数での実行の開始時に*一時停止*状態になります。

NDIS は、ドライバースタックを一時停止するために、プラグアンドプレイ操作の一部としてフィルターモジュールを一時停止します。 ドライバースタックの一時停止の概要については、「[ドライバースタックの一時停止](pausing-a-driver-stack.md)」を参照してください。

*一時停止*中の状態にあるフィルターモジュールに代わって、フィルタードライバーは次のようになります。

-   は、新しい受信表示を開始することはできません。

    送信操作と受信操作の詳細については、「[フィルターモジュールの送受信操作](filter-module-send-and-receive-operations.md)」を参照してください。

-   フィルタードライバーによって生成された受信操作があり、その NDIS が完了していない場合、フィルタードライバーは NDIS がこのような操作を完了するまで待機する必要があります。 すべての未処理の受信通知に対して、NDIS が[*Filterreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)関数を呼び出すまで、一時停止操作は完了しません。

-   基になるドライバーがすぐに NDIS に由来する未処理の受信通知を返す必要があります。 一時停止操作が完了しないのは、ドライバーが未処理の受信通知に対して[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)関数を呼び出したときです。 ドライバーが基になるドライバーから受信したバッファーをキューに配置する場合、これらの未処理の受信通知が存在する可能性があります。

-   では、 **NdisFReturnNetBufferLists**関数を呼び出すことにより、基になるドライバーがすぐに NDIS に送信されるという新しい受信通知が返されます。 必要に応じて、ドライバーは受信の表示をコピーし、それを返す前にキューに保存できます。

    **注**  [**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)は、対応する[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)呼び出しで設定された\_フラグ\_リソースフラグを受け取るように、\_NDIS によって指定された NBLs に対しては呼び出さないでください。 このような NBLs は、 *FilterReceiveNetBufferLists*ルーチンからを返すことによって、NDIS に同期的に返されます。

     

-   新しい送信要求を開始することはできません。

-   フィルタードライバーによって生成された送信操作があり、その NDIS が完了していない場合、フィルタードライバーは NDIS がこのような操作を完了するまで待機する必要があります。 すべての未処理の送信要求に対して NDIS が[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)関数を呼び出すまで、一時停止操作は完了しません。

-   では、 [**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数を呼び出すことによって、 [*filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)関数に対して行われたすべての新しい送信要求を直ちに返す必要があります。 フィルタードライバーは、各 NET\_BUFFER\_LIST 構造体の**status**メンバーを NDIS\_status\_一時停止状態に設定する必要があります。

-   では、 [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)関数を使用して状態を示すことができます。

    ステータスの表示の詳細については、「[フィルターモジュールの状態](filter-module-status-indications.md)の表示」を参照してください。

-   では、 [*Filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数の状態を処理する必要があります。

-   は、 [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)関数で OID 要求を処理する必要があります。

    OID 要求の詳細については、「[フィルターモジュール OID 要求](filter-module-oid-requests.md)」を参照してください。

-   OID 要求を開始できます。

-   アタッチ操作中にドライバーによって割り当てられたリソースを解放しないでください。

-   送信と受信の操作を停止するために必要な場合は、タイマーをキャンセルする必要があります。

    タイマーの詳細については、「 [NDIS 6.0 Timer Services](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

フィルタードライバーは、送信操作と受信操作を正常に一時停止した後、一時停止操作を完了する必要があります。 フィルタードライバーは、NDIS\_STATUS\_SUCCESS または NDIS\_\_STATUS をそれぞれ[*Filterpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)から返すことで、同期または非同期的に一時停止操作を完了できます。

ドライバーが NDIS\_STATUS\_PENDING を返した場合、一時停止操作の完了後に[**NdisFPauseComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfpausecomplete)関数を呼び出す必要があります。

*一時停止*状態にあるフィルターモジュールの代わりに、フィルタードライバーは次のようになります。

-   新しい受信表示を開始することはできません。

-   では、 [**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)関数を呼び出すことにより、基になるドライバーがすぐに NDIS に送信されるという新しい受信通知が返されます。 必要に応じて、ドライバーは受信の表示をコピーし、それを返す前にキューに保存できます。

-   新しい送信要求を開始することはできません。

-   では、 [**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数を呼び出すことによって、 [*filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)関数に対して行われたすべての新しい送信要求を直ちに返す必要があります。 フィルタードライバーは、各 NET\_BUFFER\_LIST 構造体の**status**メンバーを NDIS\_status\_一時停止状態に設定する必要があります。

-   では、 [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)関数を使用して状態を示すことができます。

-   では、 [*Filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数の状態を処理する必要があります。

-   は、 [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)関数で OID 要求を処理する必要があります。

-   OID 要求を開始できます。

NDIS は、フィルタードライバーが*一時停止*状態にある間、他のプラグアンドプレイ操作 (アタッチ、デタッチ、再起動要求など) を開始しません。 NDIS は、フィルタードライバーが*一時停止*状態になった後に、デタッチまたは再起動要求を開始できます。 フィルターモジュールをデタッチする方法の詳細については、「[フィルターモジュールのデタッチ](detaching-a-filter-module.md)」を参照してください。 フィルターモジュールを再起動する方法の詳細については、「[フィルターモジュールを開始](starting-a-filter-module.md)する」を参照してください。

 

 





