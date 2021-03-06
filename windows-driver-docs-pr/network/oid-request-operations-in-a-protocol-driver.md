---
title: プロトコル ドライバーの OID 要求操作
description: プロトコル ドライバーの OID 要求操作
ms.assetid: 767252a2-98de-4df2-89dc-ee48b2c7ca9d
keywords:
- プロトコル ドライバー WDK ネットワーク、OID 要求
- NDIS プロトコル ドライバー WDK、OID 要求します。
- OID 要求 WDK ネットワーク
- Oid WDK ネットワー キング、プロトコル ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abd82494f48e218f1013a239faf4147b60466a13
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356130"
---
# <a name="oid-request-operations-in-a-protocol-driver"></a>プロトコル ドライバーの OID 要求操作





プロトコル ドライバーに OID 要求の操作の 2 つの異なるインターフェイスがあります。 NDIS ドライバー コネクションレス低い edge 呼び出しでのプロトコル、 [ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest) OID 要求を開始する関数。 コネクションレスの下端との NDIS プロトコル ドライバーを指定する必要があります、 [ **ProtocolOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_oid_request_complete)関数。 NDIS 呼び出し*ProtocolOidRequestComplete*基になるドライバーが保留中の OID 要求を完了するとします。 コネクションレスのプロトコル ドライバーに OID 要求の詳細については、次を参照してください。[プロトコル ドライバー OID 要求](protocol-driver-oid-requests.md)します。

接続指向の NDIS (いる CoNDIS) プロトコルのドライバーの呼び出し、 [ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest) OID 要求を開始する関数。 いる CoNDIS プロトコルのドライバーを指定する必要があります、 [ **ProtocolCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request_complete)関数。 NDIS 呼び出し*ProtocolOidRequestComplete*基になるドライバーが保留中の OID 要求を完了するとします。 接続指向プロトコル ドライバーの詳細情報の OID 要求を参照してください。 [Connection-Oriented 操作](connection-oriented-operations.md)します。

Oid の詳細については、次を参照してください。 [NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

 

 





