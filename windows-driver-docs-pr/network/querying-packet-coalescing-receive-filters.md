---
title: パケット結合受信フィルターのクエリ
description: パケット結合受信フィルターのクエリ
ms.assetid: D0B41718-37B9-4FB4-BA10-20765F836214
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61917538b8948893bc62f95c145c32638c5e74f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844881"
---
# <a name="querying-packet-coalescing-receive-filters"></a>パケット結合受信フィルターのクエリ





その後のドライバーとアプリケーションは、次の手順を実行して、ミニポートドライバーにダウンロードされたパケット合体受信フィルターを照会できます。

-   Oid の OID メソッド要求を発行して、ミニポートドライバーに列挙された受信フィルターの一覧を要求します。 [ENUM\_フィルター\_列挙型フィルターを受け取る\_フィルターを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 詳細については、「[ミニポートドライバーで受信フィルターを列挙](#enumerating-the-receive-filters-on-a-miniport-driver)する」を参照してください。

-   Oid の OID メソッド要求を発行することによって、ミニポートドライバーの受信フィルターのテスト条件パラメーターを要求します。これには、 [\_フィルター\_パラメーターを\_受信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)します。 詳細については、「[ミニポートドライバーでの受信フィルターのクエリ](#querying-the-parameters-of-a-receive-filters-on-a-miniport-driver)」を参照してください。

NDIS は、 [\_フィルター\_列挙型\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)フィルターおよび OID を受け取る oid\_、ミニポートドライバーに対して\_パラメーターメソッド oid 要求を[受信\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)処理します。\_ NDIS は、oid から受信したデータの内部キャッシュから情報を取得し、 [\_フィルター\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)して oid 要求\_フィルター処理\_ます。

## <a name="enumerating-the-receive-filters-on-a-miniport-driver"></a>ミニポートドライバーで受信フィルターを列挙する


ミニポートドライバーにダウンロードされたすべてのパケット合体受信フィルターの一覧を取得するために、その後のドライバーとアプリケーションは oid の OID メソッド要求を発行します。このフィルター [\_列挙\_フィルターを受け取る\_フィルターを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体へのポインターが含まれています。

この後のドライバーまたはアプリケーションが Ndis を初期化し、 [ **\_フィルターの\_情報\_配列構造を受信\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array) **場合  、** **QUEUEID**メンバーを NDIS\_DEFAULT\_receive\_QUEUE\_ID に設定する必要があります。

 

OID メソッド要求から正常に戻った後、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   NDIS\_は、ミニポートドライバーで現在構成されている受信フィルターの一覧を指定する[ **\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体を受け取ります。

-   ミニポートドライバーで現在構成されている受信フィルターについて[ **\_情報構造を受信\_フィルター処理する NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)の配列。

## <a name="querying-the-parameters-of-a-receive-filters-on-a-miniport-driver"></a>ミニポートドライバーで受信フィルターのパラメーターを照会する


ミニポートドライバーにダウンロードされた特定のパケット合体受信フィルターのパラメーターを取得するために、前のドライバーまたはアプリケーションは oid の OID メソッド要求を発行し、 [\_フィルター\_パラメーターを受け取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)ように\_します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_受信\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体へのポインターが含まれています。 前のドライバーまたはアプリケーションは、 **Filterid**メンバーを、パラメーターが返されるフィルターの0以外の id 値に設定することによって、 **NDIS\_受信\_フィルター\_パラメーター**構造を初期化します。

これまでのドライバーでは、以前の OID メソッドの Oid 要求からフィルター ID を取得した  [\_受信\_フィルター\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)\_フィルターまたは[OID\_列挙型\_フィルター\_受信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)\_フィルターを設定する**ことに注意**してください。 アプリケーションで取得できるのは、以前の oid メソッドの OID の要求からフィルター ID を取得することだけで、列挙\_フィルター\_列挙\_フィルターを受け取る\_できます。

 

OID メソッド要求から正常に戻った後、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   Ndis\_は、NDIS 受信フィルターのパラメーターを指定する[ **\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造を受け取ります。

-   ネットワークパケットヘッダー内の1つのフィールドのフィルターテスト条件を指定する、 [ **\_フィルター\_フィールド\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)の配列。

 

 





