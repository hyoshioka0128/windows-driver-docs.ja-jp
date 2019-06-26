---
title: VM キュー パラメーターの取得と更新
description: VM キュー パラメーターの取得と更新
ms.assetid: 42beceec-95ae-48e3-985f-b6ee8a84d68b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1910825c7b2f6baaef0feb28b0eae772e37f4cd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354513"
---
# <a name="obtaining-and-updating-vm-queue-parameters"></a>VM キュー パラメーターの取得と更新





上にある、ドライバーに割り当てた後、VM のキューの構成パラメーターを設定できます。 また、上位のドライバーまたはアプリケーションはキューの現在のパラメーターと、キューに設定されているフィルターのパラメーターに取得できます。

キューの現在の構成パラメーターを変更するを使用してドライバーを重なってことができます、 [OID\_受信\_フィルター\_キュー\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters) OID 要求のセット。 上にあるドライバーへのポインターを提供する、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。

NDIS\_受信\_キュー\_パラメーター構造体がで使用される、 [OID\_受信\_フィルター\_ALLOCATE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue) OID と[OID\_受信\_フィルター\_キュー\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters) OID。 キューの割り当てに関する詳細については、次を参照してください。 [VM キューを割り当てる](allocating-a-vm-queue.md)します。

現在の構成を取得するキュー、ドライバーを後続のパラメーターが、OID を使用できます\_受信\_フィルター\_キュー\_パラメーター メソッド OID を要求します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters) NDIS の種類のキューの id を使用した構造\_受信\_キュー\_Id。 OID メソッドの要求から正常に戻った後、 **InformationBuffer**の NDIS メンバー\_OID\_要求の構造体にはへのポインターが含まれています、 **NDIS\_受信\_キュー\_パラメーター**構造体。

NDIS は、ミニポート ドライバー メソッド要求を処理します。 そのため、OID\_受信\_フィルター\_キュー\_メソッド OID 要求のパラメーターは、ミニポート ドライバーには要求されません。 NDIS OID から受信したデータの内部キャッシュから情報を入手した\_受信\_フィルター\_ALLOCATE\_キューと OID\_受信\_フィルター\_キュー\_パラメーターの OID を要求します。

現在の構成パラメーターを取得する受信キューでのフィルターを使用できますのドライバーが重なって、 [OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)メソッド要求の OID。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体。 NDIS を使用して、 **FilterId**入力構造で、フィルターを特定のメンバー。 メソッドの要求から正常に戻った後、 **InformationBuffer**の NDIS メンバー\_OID\_構造には、更新された NDIS へのポインターが含まれる要求\_受信\_フィルター\_パラメーター構造体。

NDIS 処理 OID\_受信\_フィルター\_ミニポート ドライバーのパラメーター メソッド OID を要求します。 NDIS から受信したデータの内部キャッシュからの情報の取得、 [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter) OID 要求。

OID を使用できるドライバーが重なって\_受信\_フィルター\_パラメーター メソッド OID 要求受信キューでのフィルターの構成パラメーターを取得します。

上にあるドライバーは、以前の OID からフィルター id を取得した\_受信\_フィルター\_設定\_メソッド OID 要求のフィルターまたはから、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters) OID 要求。 ドライバーは、OID を使用できる専用\_受信\_フィルター\_設定\_フィルター要求。

アプリケーションからのフィルターの識別子を取得した、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters) OID 要求。

 

 





