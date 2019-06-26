---
title: パケット結合受信フィルターのクエリ
description: パケット結合受信フィルターのクエリ
ms.assetid: D0B41718-37B9-4FB4-BA10-20765F836214
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c1250e4b0dce86c68d4a8a90eb5c74bb8e9583f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379198"
---
# <a name="querying-packet-coalescing-receive-filters"></a>パケット結合受信フィルターのクエリ





上位のドライバーとアプリケーションのクエリは、次の手順に従って、ミニポート ドライバーにダウンロードされているフィルターが表示されるパケットを結合できます。

-   OID メソッド要求を発行して、ミニポート ドライバーでの受信フィルターの一覧の列挙を要求[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 詳細については、次を参照してください。[ミニポート ドライバーでの受信フィルターを列挙する](#enumerating-the-receive-filters-on-a-miniport-driver)します。

-   受信フィルター ミニポート ドライバーのテスト条件のパラメーターを要求の OID メソッド要求を発行して[OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)します。 詳細については、次を参照してください[ミニポート ドライバーでの受信フィルターのクエリを実行する。](#querying-the-parameters-of-a-receive-filters-on-a-miniport-driver)

NDIS ハンドル、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)と[OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)メソッド OID は、ミニポート ドライバーを要求します。 NDIS から受信したデータの内部キャッシュからの情報の取得、 [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter) OID 要求。

## <a name="enumerating-the-receive-filters-on-a-miniport-driver"></a>ミニポート ドライバーでの受信フィルターを列挙します。


ミニポート ドライバーにダウンロードされているフィルターをすべての受信パケットの結合の一覧を取得する上位のドライバーとアプリケーションでの OID メソッド要求が発行[OID\_受信\_フィルター\_列挙型\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体。

**注**  上にあるドライバーまたはアプリケーションを初期化するときに、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)に設定する必要があります、構造、 **QueueId** NDIS メンバー\_既定\_受信\_キュー\_id。

 

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体バッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)で現在構成されている受信フィルターの一覧を指定する構造体、ミニポート ドライバー。

-   配列の[ **NDIS\_受信\_フィルター\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info)ミニポート ドライバーで現在構成されている受信フィルターに関する構造体。

## <a name="querying-the-parameters-of-a-receive-filters-on-a-miniport-driver"></a>ミニポート ドライバーでの受信フィルターのパラメーターのクエリを実行します。


特定のパケットの結合のパラメーターを取得するには、受信のフィルター ドライバーが重なって、ミニポート ドライバーにダウンロードされた、またはアプリケーションの OID メソッド要求を発行する[OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体。 上にあるドライバーまたはアプリケーションの初期化、 **NDIS\_受信\_フィルター\_パラメーター**構造体を設定して、 **FilterId**メンバーを 0 以外の IDパラメーターが返されるフィルターの値。

**注**  上にあるドライバーの以前の OID メソッド要求から、フィルター ID を取得した[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)または[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 アプリケーションは、フィルター ID を OID の以前の OID メソッド要求から取得できますのみ\_受信\_フィルター\_ENUM\_フィルター。

 

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体バッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) NDIS のパラメーターを指定する構造体は、フィルターを受信します。

-   配列の[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)フィルターを指定する構造体は、フィールドを 1 つの条件をテストします。ネットワーク パケットのヘッダー。

 

 





