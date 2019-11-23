---
title: フィルター ドライバーからのデータの送信
description: フィルター ドライバーからのデータの送信
ms.assetid: 09189010-d12c-43d6-ac9b-8fc7424edfd5
keywords:
- データの送信 (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b0ccd217f5c26cd82b4a31e5d9bc8980696b6af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841980"
---
# <a name="sending-data-from-a-filter-driver"></a>フィルター ドライバーからのデータの送信





フィルタードライバーは、送信要求を開始したり、それ以降のドライバーが開始する送信要求をフィルター処理したりすることができます。 プロトコルドライバーが[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)関数を呼び出すと、NDIS は、指定された[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体をドライバースタック内の最上位のフィルターモジュールに送信します。

### <a name="send-requests-initiated-by-a-filter-driver"></a>フィルタードライバーによって開始された要求を送信する

次の図は、フィルタードライバーによって開始される送信操作を示しています。

![フィルタードライバーによって開始された送信操作を示す図](images/filtersend.png)

フィルタードライバーは、 [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)関数を呼び出して、 [**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の一覧に定義されているネットワークデータを送信します。

フィルタードライバーは、 **NdisFSendNetBufferLists**の*NdisFilterHandle*パラメーターに渡されるのと同じ値に、作成する各 NET\_BUFFER\_LIST 構造体の**sourcehandle**メンバーを設定する必要があります。 NDIS ドライバーでは、ドライバーが生成されなかった\_リスト構造体の NET\_BUFFER の**Sourcehandle**メンバーを変更しないでください。

**NdisFSendNetBufferLists**を呼び出す前に、フィルタードライバーは、送信要求に付随する情報を、 [**NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロに設定できます。 基になるドライバーは、NET\_BUFFER\_LIST\_INFO マクロを使用してこの情報を取得できます。

フィルタードライバーは、 **NdisFSendNetBufferLists**を呼び出すとすぐに、NET\_BUFFER\_LIST 構造体と、関連付けられているすべてのリソースの所有権を放棄します。 NDIS は、送信要求を処理するか、基になるドライバーに要求を渡すことができます。

NDIS は、 [*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)関数を呼び出して、構造体とデータをフィルタードライバーに返します。 NDIS では、 *FilterSendNetBufferListsComplete*にリストを渡す前に、複数の送信要求の構造とデータを、NET\_BUFFER\_リスト構造の1つのリンクリストに収集できます。

NDIS が*FilterSendNetBufferListsComplete*を呼び出すまでは、送信要求の現在の状態は不明です。 フィルタードライバーは、NDIS が構造体を*FilterSendNetBufferListsComplete*に返す前に、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体または関連するデータを調べようとしてはなり*ません*。

*FilterSendNetBufferListsComplete*は、送信操作を完了するために必要なすべての後処理を実行します。

NDIS が*FilterSendNetBufferListsComplete*を呼び出すと、フィルタードライバーは、 *NetBufferLists*パラメーターで指定されている、NET\_BUFFER\_リスト構造に関連付けられているすべてのリソースの所有権を取得します。 *FilterSendNetBufferListsComplete*は、これらのリソース (たとえば、 [**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)関数と[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)関数を呼び出して) を解放するか、 **NdisFSendNetBufferLists**への後続の呼び出しで再利用できるように準備することができます。

NDIS は、フィルターによって指定されたネットワークデータを、 **NdisFSendNetBufferLists**に渡されたフィルタードライバーによって決まる順序で、基になるドライバーに常に送信します。 ただし、指定された順序でデータを送信した後は、基になるドライバーが任意の順序でバッファーを返すことができます。

フィルタードライバーは、送信元の送信要求に対してループバックを要求できます。 ループバックを要求するために、ドライバーは、 [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)の*sendflags*パラメーターで\_ループバックフラグの\_\_\_フラグを\_送信するように NDIS を設定します。 NDIS は、送信データを含む受信パケットを示します。

フィルタードライバーは、送信元の送信要求を追跡し、そのような要求が完了したときに[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数が呼び出されないようにする必要があることに  **注意**してください。

 

### <a name="filtering-send-requests"></a>送信要求のフィルター処理

次の図は、その後のドライバーによって開始される送信要求をフィルター処理する方法を示しています。

![前のドライバーによって開始される送信要求のフィルター処理を示す図](images/sendfilter.png)

NDIS は、フィルタードライバーの[*Filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)関数を呼び出して、後続のドライバーの送信要求をフィルター処理します。

フィルタードライバーは、他のドライバーから受信する NET\_BUFFER\_リスト構造の**Sourcehandle**メンバーを変更することはできません。

フィルタードライバーは、データをフィルター処理し、フィルター処理されたデータを基になるドライバーに送信できます。 *Filtersendnetbufferlists*に送信された各 NET\_BUFFER 構造体に対して、フィルタードライバーは次の操作を実行できます。

-   [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)関数を呼び出して、次に基になるドライバーにバッファーを渡します。 NDIS では、コンテキスト空間の可用性が保証されます (フィルタードライバーについては、「 [NET\_BUFFER\_LIST\_context structure](net-buffer-list-context-structure.md))」を参照してください。 フィルタードライバーは、 **NdisFSendNetBufferLists**を呼び出す前にバッファーの内容を変更できます。 フィルター処理されたデータの処理は、フィルタードライバーによって開始された送信操作と同様に続行されます。

-   [**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数を呼び出してバッファーを削除します。

-   後で処理するために、ローカルデータ構造でバッファーをキューに格納します。 フィルタードライバーの設計により、ドライバーがキューに格納されたバッファーを処理する原因が決まります。 例としては、特定のバッファーを受信した後の、タイムアウトまたは処理後の処理などがあります。

    **注**  後で処理するためにドライバーが要求を送信する場合は、キャンセル要求の送信をサポートする必要があります。 キャンセル要求の送信の詳細については、「[フィルタードライバーでの送信要求の取り消し](canceling-a-send-request-in-a-filter-driver.md)」を参照してください。

     

-   バッファーをコピーし、そのコピーを使用して送信要求を開始します。 送信操作は、フィルタードライバーによって開始された送信要求に似ています。 この場合、ドライバーは[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数を呼び出すことによって、元のバッファーを前のドライバーに返す必要があります。

送信要求が完了すると、ドライバースタックが処理されます。 ミニポートドライバーが[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出すと、NDIS は、最も低いフィルターモジュールの[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)関数を呼び出します。

送信操作が完了すると、フィルタードライバーは、フィルタードライバーが*Filtersendnetbufferlists*で行った前のドライバーのバッファー記述子に変更を戻します。 ドライバーは、 [**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数を呼び出して、NET\_BUFFER\_list 構造体のリンクリストをその後のドライバーに返し、送信要求の最終状態を返します。

最上位のフィルターモジュールが**NdisFSendNetBufferListsComplete**を呼び出すと、NDIS は発信元のプロトコルドライバーの[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)関数を呼び出します。

*Filtersendnetbufferlists*関数を提供しないフィルタードライバーでも、送信要求を開始できます。 このようなドライバーが送信要求を開始する場合は、 *FilterSendNetBufferListsComplete*関数を提供する必要があり、完全なイベントをドライバースタックに渡すことはできません。

フィルタードライバーは、後続のドライバーのループバック要求に対して、パススルーまたはフィルター処理を行うことができます。 ループバック要求を渡す場合は、NDIS set NDIS\_によって\_フラグ\_送信されます。 *Filtersendnetbufferlists*の*sendflags*パラメーターで\_ループバックの\_を確認します。フィルタードライバーは、 **NdisFSendNetBufferLists**を呼び出すときに、 *sendflags*パラメーターの\_ループバックに対して、\_の\_を確認\_に送信\_フラグを設定します。 NDIS は、送信データを含む受信パケットを示します。

一般に、NDIS が標準サービス (ループバックなど) を提供できないような方法でフィルタードライバーが動作を変更した場合、フィルタードライバーは NDIS 用にそのサービスを提供する必要があります。 たとえば、ハードウェアアドレスの要求を変更するフィルタードライバー ( [OID\_802\_3\_現在の\_アドレス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address)) は、新しいハードウェアアドレスに送られるバッファーのループバックを処理する必要があります。 この場合、NDIS は、フィルターによってアドレスが変更されたため、通常提供するループバックサービスを提供できません。 また、フィルタードライバーで無作為検出モードが設定されている場合 (「 [OID\_GEN\_現在の\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter))」を参照してください。これにより、その後のドライバーに受信する追加のデータを渡すことはできません。

 

 





