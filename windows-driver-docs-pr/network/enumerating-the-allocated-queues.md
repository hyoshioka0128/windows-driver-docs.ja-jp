---
title: 割り当て済みキューの列挙
description: 割り当て済みキューの列挙
ms.assetid: 4566314b-ea6b-49e2-bc85-946ed303bc6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9972e0512207d45e6cdcfaa5a08862868b9c6096
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354561"
---
# <a name="enumerating-the-allocated-queues"></a>割り当て済みキューの列挙





すべての受信キューの一覧を取得するに割り当てられたネットワーク アダプターでは、上位のドライバーの問題、 [OID\_受信\_フィルター\_ENUM\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)クエリ OID 要求。 OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体ポインターが含まれています、 [ **NDIS\_受信\_キュー\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)が続く構造体、 [**NDIS\_受信\_キュー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info)キューごとに構造体。

NDIS 処理 OID\_受信\_フィルター\_列挙\_ミニポート ドライバーのキュー クエリ OID 要求。 NDIS から受信したデータの内部キャッシュからの情報の取得、 [OID\_受信\_フィルター\_ALLOCATE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)と[OID\_受信\_フィルター\_キュー\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters) OID 要求。

OID を使用できるドライバーとユーザー モード アプリケーションが重なって\_受信\_フィルター\_ENUM\_ネットワーク アダプターの受信キューを列挙するためにクエリ要求をキューの OID。

要求の種類のプロトコル ドライバーには、要求が発行した場合、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造に設定されている**NdisRequestQueryInformation**し、この OID は、ネットワーク アダプターのプロトコル ドライバーに割り当てられているすべての受信キューの配列を返します。 ユーザー モード アプリケーションが要求を発行した場合、要求入力、NDIS\_OID\_要求に設定**NdisRequestQueryStatistics**、この OID が上のすべての受信キュー情報の配列を返しますミニポート アダプター。

 

 





