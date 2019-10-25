---
title: 情報のクエリと設定
description: 情報のクエリと設定
ms.assetid: 39bd9846-7c7e-4b93-8060-4da9c66ac591
keywords:
- 接続指向情報のクエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9976f73bb9aa0ea56d217f50c27ec35ac2492bef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844893"
---
# <a name="querying-or-setting-information"></a>情報のクエリと設定





CoNDIS プロトコルドライバーと NDIS は、基になるドライバーに OID 要求を送信できます。 CoNDIS プロトコルドライバーとミニポートコールマネージャー (MCMs) は、他のプロトコルドライバーに OID 要求を送信することもできます。

接続指向クライアントまたは呼び出しマネージャーは、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を呼び出して、バインドまたは基になるミニポートドライバーによって、別のプロトコルドライバーによって管理されている情報を照会または設定します。

**NdisCoOidRequest**を呼び出す前に、クライアントまたは呼び出しマネージャーは、要求のバッファーを割り当て、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体を初期化します。 この構造体は、要求の種類 (クエリまたはセット) を指定し、クエリまたは設定する情報 (OID) を識別し、OID データを渡すために使用されるバッファーを指します。

接続指向クライアントまたはコールマネージャーが有効な*NdisAfHandle* (「[アドレスファミリ](address-families.md)」を参照してください) を渡すと、NDIS はバインドで各プロトコルドライバーの[**ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request)関数を呼び出します。

NDIS は、デバイスの特性、構成可能な設定、統計などの操作パラメーターを含む、アダプターのパラメーターを識別するオブジェクト識別子 (OID) の値を定義します。 Oid の詳細については、「 [NDIS oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

ここでは、次のトピックについて説明します。

[CoNDIS ミニポートドライバー OID 要求](condis-miniport-driver-oid-requests.md)

[CoNDIS Protocol Driver OID 要求](condis-protocol-driver-oid-requests.md)

[Conmcm OID 要求](condis-mcm-oid-requests.md)

 

 





