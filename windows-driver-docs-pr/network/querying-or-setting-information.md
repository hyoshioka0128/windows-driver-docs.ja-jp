---
title: 情報のクエリと設定
description: 情報のクエリと設定
ms.assetid: 39bd9846-7c7e-4b93-8060-4da9c66ac591
keywords:
- 接続指向の情報の照会
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff3ccd33913d00dab3a910a6c487ca2ac63aa073
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381186"
---
# <a name="querying-or-setting-information"></a>情報のクエリと設定





いる CoNDIS プロトコル ドライバーおよび NDIS は、基になるドライバーに OID 要求を送信できます。 いる CoNDIS プロトコル ドライバーおよびミニポート コール マネージャー (MCMs) では、その他のプロトコル ドライバーに OID 要求を送信できますも。

接続指向のクライアントまたは呼び出しマネージャーは、 [ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)クエリまたはバインディング上の別のプロトコル ドライバーによって、または基になるミニポート ドライバーによって管理されている情報を設定します。

呼び出す前に**NdisCoOidRequest**、クライアントまたは呼び出しのマネージャーを選択し、その要求のバッファーを割り当てますを初期化します、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 この構造体では、照会したり、設定されているは、OID のデータを渡すために使用されるバッファーを指すようにする情報 (OID) を識別する要求 (クエリまたはセット) の種類を指定します。

接続指向のクライアントまたは呼び出し manager 渡します、有効な場合*NdisAfHandle* (を参照してください[アドレス ファミリ](address-families.md))、NDIS 呼び出し、 [ **ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request)バインディングでは、各プロトコル ドライバーの機能です。

NDIS は、デバイスの特性、構成可能な設定、および統計情報などのパラメーターを含む、アダプターのパラメーターを識別するためにオブジェクト識別子 (OID) の値を定義します。 Oid の詳細については、次を参照してください。 [NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

ここでは、次のトピックについて説明します。

[いる CoNDIS ミニポート ドライバー OID 要求](condis-miniport-driver-oid-requests.md)

[いる CoNDIS プロトコル ドライバー OID 要求](condis-protocol-driver-oid-requests.md)

[いる CoNDIS MCM OID 要求](condis-mcm-oid-requests.md)

 

 





