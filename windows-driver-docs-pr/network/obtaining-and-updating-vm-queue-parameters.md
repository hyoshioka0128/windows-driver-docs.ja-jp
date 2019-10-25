---
title: VM キュー パラメーターの取得と更新
description: VM キュー パラメーターの取得と更新
ms.assetid: 42beceec-95ae-48e3-985f-b6ee8a84d68b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83b49e4639050abe1cdf8e2b1dbf1c385110ef9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837746"
---
# <a name="obtaining-and-updating-vm-queue-parameters"></a>VM キュー パラメーターの取得と更新





後続のドライバーは、割り当てられた後に VM キューの構成パラメーターを設定できます。 また、その後のドライバーまたはアプリケーションは、キューの現在のパラメーターと、キューに設定されているフィルターのパラメーターを取得できます。

キューの現在の構成パラメーターを変更するには、その後のドライバーが Oid を使用して[\_キュー\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters)設定 oid 要求を受信\_フィルターを\_ことができます。 このドライバーは、ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバー内の[ **\_キュー\_パラメーターの構造を受け取る ndis\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)を指すポインターを提供します。

NDIS\_RECEIVE\_QUEUE\_PARAMETERS 構造体を使用して\_キュー oid の[割り当て\_フィルター\_\_を受け取る oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue) 、および[oid\_フィルター\_キューを受信\_\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters) OID。 キューの割り当ての詳細については、「 [VM キューの割り当て](allocating-a-vm-queue.md)」を参照してください。

キューの現在の構成パラメーターを取得するために、後続のドライバーは、\_QUEUE\_PARAMETERS メソッド OID 要求を受信\_フィルター処理\_OID を使用できます。 Ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初に NDIS [ **\_RECEIVE\_queue\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体へのポインターが含まれています。t_10_ は\_キュー\_ID を受信します。 OID メソッド要求から正常に戻った後、NDIS\_OID\_要求構造の**Informationbuffer**メンバーには、 **ndis\_RECEIVE\_QUEUE\_PARAMETERS**構造体へのポインターが含まれています。

NDIS は、ミニポートドライバーのメソッド要求を処理します。 そのため、OID\_受信\_フィルター\_QUEUE\_PARAMETERS メソッド OID 要求がミニポートドライバーに要求されていません。 NDIS は、OID から受信したデータの内部キャッシュから情報を取得し、\_QUEUE および OID を割り当てる\_キューと OID を割り当てることによって、\_\_パラメーター OID 要求を受信\_フィルター処理するように\_フィルターを\_受け取ります。

受信キューのフィルターの現在の構成パラメーターを取得するには、その後のドライバーが[oid\_受信\_フィルター\_parameters](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)メソッド oid 要求を使用できます。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初は[**ndis\_RECEIVE\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体へのポインターが含まれています。 NDIS では、入力構造の**Filterid**メンバーを使用してフィルターを識別します。 メソッド要求から正常に戻った後、NDIS\_OID\_要求構造の**Informationbuffer**メンバーには、更新された NDIS\_RECEIVE\_FILTER\_PARAMETERS 構造体へのポインターが含まれています。

NDIS は、ミニポートドライバーに対する\_フィルター\_PARAMETERS メソッド OID 要求を受信\_OID を処理します。 NDIS は、oid から受信したデータの内部キャッシュから情報を取得し、 [\_フィルター\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)して oid 要求\_フィルター処理\_ます。

それまでのドライバーでは、OID\_受信\_フィルター\_PARAMETERS メソッド OID 要求を使用して、受信キューのフィルターの構成パラメーターを取得できます。

先行するドライバーは、以前の OID からフィルター識別子を取得し、フィルターメソッドの OID 要求\_\_設定するか、 [oid から受信\_フィルター\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)\_フィルター oid によって\_フィルターを\_します。申請. \_フィルター\_設定\_フィルター要求の OID\_使用できるのは、ドライバーのみです。

アプリケーションは Oid からフィルター識別子を取得[\_、列挙型\_フィルター oid 要求を受信\_フィルター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。

 

 





