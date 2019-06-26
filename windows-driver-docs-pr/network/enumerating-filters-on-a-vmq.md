---
title: VMQ のフィルターの列挙
description: VMQ のフィルターの列挙
ms.assetid: 6d5d8cb6-7bdf-488b-8fcd-7c6e78c4fb24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee885b6a1b57ea1e2bb8bb58014590c9c0c2981e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354587"
---
# <a name="enumerating-filters-on-a-vmq"></a>VMQ のフィルターの列挙





受信キューに設定されているすべてのフィルターの一覧を取得する関連ドライバーおよびアプリケーション使用できます、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)メソッド オブジェクト識別子 (OID) 要求します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体。 書式設定すると、 **NDIS\_受信\_フィルター\_情報\_配列**構造、上にあるドライバーまたはアプリケーションを設定する必要があります、 **QueueId**受信キューの識別子 (ID) のメンバー。 次の方法で受信キューの ID を取得します。

-   上にあるドライバーを以前の OID メソッド要求の受信キューの ID 値を取得した[OID\_受信\_フィルター\_ALLOCATE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)または[OID\_受信\_フィルター\_ENUM\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)します。 ドライバーを指定できますも**NDIS\_既定\_受信\_キュー\_ID**既定のキューを受信します。

-   アプリケーションの以前の OID メソッド要求から受信したキューの ID 値を取得した[OID\_受信\_フィルター\_ENUM\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)します。 アプリケーションを指定できますも**NDIS\_既定\_受信\_キュー\_ID**既定のキューを受信します。

OID メソッド要求から正常に戻った後[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造には、更新されたへのポインターが含まれる[ **NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体が 1 つまたは複数続く[ **NDIS\_受信\_フィルター\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info)構造体。 各**NDIS\_受信\_フィルター\_情報**構造体を指定された受信キューが設定されているフィルターの ID を指定します。

使用できるドライバーやアプリケーションが重なって、 [OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters) OID メソッド要求の受信キューで特定のフィルターのパラメーターを取得します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体。 上にあるドライバーまたはアプリケーションの形式、 **NDIS\_受信\_フィルター\_パラメーター**構造体を設定して、 **FilterId**メンバーを 0 以外の IDパラメーターが返されるフィルターの値。

**注**  上にあるドライバーの以前の OID メソッド要求から、フィルター ID を取得した[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)または[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 アプリケーションは、OID の以前の OID メソッド要求からのみ、フィルター ID を取得できます\_受信\_フィルター\_ENUM\_フィルター。

 

NDIS ハンドル、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)と[OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)メソッド OID は、ミニポート ドライバーを要求します。 NDIS から受信したデータの内部キャッシュからの情報の取得、 [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter) OID 要求。

 

 





