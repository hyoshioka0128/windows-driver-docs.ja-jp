---
title: VMQ のフィルターの列挙
description: VMQ のフィルターの列挙
ms.assetid: 6d5d8cb6-7bdf-488b-8fcd-7c6e78c4fb24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bbb976e7217d5926460bfcd411bca4a9cdc0282
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834786"
---
# <a name="enumerating-filters-on-a-vmq"></a>VMQ のフィルターの列挙





受信キューに設定されているすべてのフィルターの一覧を取得するには、その後のドライバーとアプリケーションが Oid を使用して、ENUM\_フィルターメソッドオブジェクト識別子 (OID) 要求を[受信\_フィルター\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)できます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初に、 [ **\_フィルター\_情報\_配列構造を受け取る ndis\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)を指すポインターが含まれています。 **\_フィルター\_情報\_配列**構造を受け取るように NDIS\_フォーマットするときに、そのドライバーまたはアプリケーションは、 **queueid**メンバーを受信キューの識別子 (id) に設定する必要があります。 受信キュー ID は、次の方法で取得されます。

-   これまでのドライバーは、以前の oid メソッドの Oid 要求から受信キュー ID の値を取得し、\_キューまたは Oid を割り当て\_[列挙型\_キューを受け取る\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)を受け取る[\_フィルターを\_受け取り](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)ます。\_\_ また、ドライバーは、既定の受信キューの **\_キュー\_ID を受け取るように NDIS\_既定\_** 指定することもできます。

-   アプリケーションは、以前の OID メソッドの Oid 要求から receive queue ID 値を取得し、[列挙型\_キュー\_受信\_フィルターを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)します。 アプリケーションでは、既定の受信キューの **\_キュー\_ID を受け取るように NDIS\_既定\_** 指定することもできます。

Oid の OID メソッド要求から正常に返された後[\_フィルター\_列挙\_フィルターを受け取る\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)、 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、更新された NDIS [ **\_receive\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info) [**filter\_info\_ARRAY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体へのポインターが含まれます。\_\_\_ 各**NDIS\_受信\_フィルター\_情報**構造は、指定された受信キューに設定されているフィルターの ID を指定します。

それ以降のドライバーまたはアプリケーションでは、 [oid\_受信\_フィルター\_parameters](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters) oid メソッド要求を使用して、受信キューの特定のフィルターのパラメーターを取得できます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初は[**ndis\_RECEIVE\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体へのポインターが含まれています。 前のドライバーまたはアプリケーションは、 **Filterid**メンバーを、パラメーターが返されるフィルターの0以外の id 値に設定することによって、 **NDIS\_受信\_フィルター\_パラメーター**構造を受け取ります。

これまでのドライバーでは、以前の OID メソッドの Oid 要求からフィルター ID を取得した  [\_受信\_フィルター\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)\_フィルターまたは[OID\_列挙型\_フィルター\_受信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)\_フィルターを設定する**ことに注意**してください。 アプリケーションでフィルター ID を取得できるのは、以前の oid メソッドの OID の要求からだけで、列挙\_フィルター\_列挙型の\_フィルターを受け取る\_です。

 

NDIS は、 [\_フィルター\_列挙型\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)フィルターおよび OID を受け取る oid\_、ミニポートドライバーに対して\_パラメーターメソッド oid 要求を[受信\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)処理します。\_ NDIS は、oid から受信したデータの内部キャッシュから情報を取得し、 [\_フィルター\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)して oid 要求\_フィルター処理\_ます。

 

 





