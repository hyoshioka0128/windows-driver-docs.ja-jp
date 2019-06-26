---
title: フィルター モジュールの一時停止
description: フィルター モジュールの一時停止
ms.assetid: da75b92d-b662-416a-b350-e5384b870b7f
keywords:
- WDK のモジュールをフィルター処理ネットワーク、一時停止
- フィルター モジュールが一時停止
- フィルター ドライバー WDK ネットワークは、フィルター モジュールを一時停止
- NDIS フィルター ドライバー WDK、フィルター モジュールを一時停止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b6670906e5fbaa536b81adcbc6682e537b93c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384545"
---
# <a name="pausing-a-filter-module"></a>フィルター モジュールの一時停止





NDIS フィルター ドライバーの呼び出しを実行中のフィルター モジュールを一時停止する[ *FilterPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_pause)関数。 フィルター モジュールが入力、*一時停止中*状態での実行の開始時、 *FilterPause*関数。

NDIS は、ドライバー スタックを一時停止するプラグ アンド プレイ操作の一部としてフィルター モジュールを一時停止します。 ドライバー スタックを一時停止の概要については、次を参照してください。[ドライバー スタックを一時停止](pausing-a-driver-stack.md)します。

内にあるフィルター モジュールの代わり、*一時停止中*状態では、フィルター ドライバー。

-   いずれかが引かれていない新しいインジケーターを受信します。

    送信し、受信操作についての詳細についてを参照してください。[フィルター モジュールの送信と受信操作](filter-module-send-and-receive-operations.md)します。

-   受信フィルター ドライバーを開始した操作が存在し、NDIS に完了しなかった場合、フィルター ドライバーはこのような操作を完了する NDIS を待つ必要があります。 NDIS 呼び出されるまでは一時停止操作が完了しない、 [ *FilterReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)関数のようなすべての保留状態インジケーターを受信します。

-   未解決の戻り値が表示されますがない NDIS をすぐに発生したその基になるドライバー。 ドライバー呼び出されるまでは一時停止操作が完了しない、 [ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)関数のような未処理受信表示します。 これらの未処理の受信がない場合は、ドライバーは、基になるドライバーから受信するバッファーをキューに存在できます。

-   戻り値の新しい受信呼び出してすぐに、基になるドライバーが発信する NDIS 表示をする必要があります、 **NdisFReturnNetBufferLists**関数。 かどうか、必要に応じて、ドライバーをコピーできますインジケーターを受信し、それらを返す前にキューに登録します。

    **注**  [**NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists) NDIS で提示されている NBLs を呼び出されません\_受信\_フラグ\_リソース フラグが設定で、対応する[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)呼び出します。 このような NBLs が返されます NDIS を同期的にから返すことによって、 *FilterReceiveNetBufferLists*ルーチン。

     

-   新しい送信要求を元にする必要があります。

-   送信操作、フィルター ドライバーが発生したこと、および NDIS が完了していない場合は、フィルター ドライバーはこのような操作を完了する NDIS を待つ必要があります。 NDIS 呼び出されるまでは一時停止操作が完了しない、 [ *FilterSendNetBufferListsComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists_complete)関数のようなすべての保留状態要求を送信します。

-   すべて新規に対して行われた要求の送信を返す必要があります、 [ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)関数を呼び出すことによってすぐに、 [ **NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数。 フィルター ドライバーを設定する必要があります、**状態**各ネットワーク内のメンバー\_バッファー\_NDIS にリスト構造\_状態\_一時停止します。

-   状態インジケーターを提供することができます、 [ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)関数。

    状態インジケーターの詳細については、次を参照してください。[フィルター モジュールの状態インジケーター](filter-module-status-indications.md)します。

-   状態インジケーターを処理する必要があります、 [ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)関数。

-   OID の要求を処理する必要があります、 [ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)関数。

    OID 要求の詳細については、次を参照してください。[フィルター モジュールの OID 要求](filter-module-oid-requests.md)します。

-   OID の要求を開始できます。

-   ドライバー、アタッチ操作中に割り当てられたリソースを解放する必要があります。

-   送信を停止し、受信操作に必要な場合、タイマーをキャンセルする必要があります。

    タイマーの詳細については、次を参照してください。 [NDIS 6.0 タイマー サービス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

フィルター ドライバーは正常に送信を一時停止し、受信操作で後、一時停止操作を完了する必要があります。 フィルター ドライバー操作を完了できる一時停止同期または非同期で NDIS を返すことによって\_状態\_成功または NDIS\_状態\_からそれぞれ PENDING [ *FilterPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_pause)します。

ドライバーは、NDIS を返す場合\_状態\_保留中、呼び出す必要があります、 [ **NdisFPauseComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfpausecomplete)一時停止操作が完了した後に機能します。

内にあるフィルター モジュールの代わり、 *Paused*状態では、フィルター ドライバー。

-   基にする必要があります新しいインジケーターを受信します。

-   戻り値の新しい受信呼び出してすぐに、基になるドライバーが発信する NDIS 表示をする必要があります、 [ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)関数。 かどうか、必要に応じて、ドライバーをコピーできますインジケーターを受信し、それらを返す前にキューに登録します。

-   新しい送信要求を元にする必要があります。

-   すべて新規に対して行われた要求の送信を返す必要があります、 [ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)関数を呼び出すことによってすぐに、 [ **NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数。 フィルター ドライバーを設定する必要があります、**状態**各ネットワーク内のメンバー\_バッファー\_NDIS にリスト構造\_状態\_一時停止します。

-   状態インジケーターを提供することができます、 [ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)関数。

-   状態インジケーターを処理する必要があります、 [ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)関数。

-   OID の要求を処理する必要があります、 [ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)関数。

-   OID の要求を開始できます。

NDIS が他のプラグ アンド プレイ操作を開始していないなどのアタッチ、デタッチ、または再起動を要求するときに、フィルター ドライバーは、*一時停止中*状態。 NDIS を開始できるデタッチまたはフィルター ドライバーが、後の再起動要求、 *Paused*状態。 フィルター モジュールを切断する方法の詳細については、次を参照してください。[フィルター モジュールをデタッチ](detaching-a-filter-module.md)します。 フィルター モジュールを再起動する方法の詳細については、次を参照してください。[フィルター モジュールの開始](starting-a-filter-module.md)します。

 

 





