---
title: 割り当て済みキューの列挙
description: 割り当て済みキューの列挙
ms.assetid: 4566314b-ea6b-49e2-bc85-946ed303bc6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76a20db72c0d3eac0727b51d0b3138545fd6cac6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834774"
---
# <a name="enumerating-the-allocated-queues"></a>割り当て済みキューの列挙





ネットワークアダプターに割り当てられているすべての受信キューの一覧を取得するために、前のドライバーは、列挙\_キュークエリ OID 要求を[受信\_フィルター\_を受け取る oid を\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)します。 OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_RECEIVE\_QUEUE\_INFO\_ARRAY へのポインターが含まれています。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)各キューの[ **\_QUEUE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)構造体を受け取る構造体の後に、NDIS\_によって受信されます。

NDIS は、ENUM\_QUEUE\_列挙型キュー\_フィルターを受け取る OID を処理し、ミニポートドライバーに対するクエリ OID 要求を\_します。 NDIS は、Oid から受信したデータの内部キャッシュから情報を取得し、\_QUEUE と Oid を[割り当てる\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)と OID を割り当てるために、\_フィルターを\_受信します。\_\_[フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters)OID 要求。

それ以降のドライバーやユーザーモードアプリケーションでは、OID\_受信\_フィルター\_列挙型\_キュー OID クエリ要求を使用して、ネットワークアダプターの受信キューを列挙できます。

プロトコルドライバーが要求を発行すると、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の要求の種類が**NdisRequestQueryInformation**に設定され、この OID はプロトコルドライバーが割り当てられているすべての受信キューの配列を返します。ネットワークアダプター。 ユーザーモードアプリケーションが要求を発行した場合、NDIS\_OID\_要求の要求の種類は**NdisRequestQueryStatistics**に設定され、この OID はミニポートアダプターのすべての受信キューに関する情報の配列を返します。

 

 





