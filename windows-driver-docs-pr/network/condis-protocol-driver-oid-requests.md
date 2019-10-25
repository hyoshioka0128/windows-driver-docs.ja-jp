---
title: CoNDIS プロトコル ドライバー OID 要求
description: CoNDIS プロトコル ドライバー OID 要求
ms.assetid: 1338d199-2cd8-430a-a0a5-95aaea04c384
keywords:
- プロトコルドライバー WDK ネットワーク、CoNDIS
- NDIS プロトコルドライバー WDK、CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47e0f9f59d3679634f80fc444b814dc3f36675b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835085"
---
# <a name="condis-protocol-driver-oid-requests"></a>CoNDIS プロトコル ドライバー OID 要求





クライアントまたはコールマネージャーである CoNDIS プロトコルドライバーは、ミニポートドライバーやその他のプロトコルドライバーの操作パラメーターを照会または設定できます。 CoNDIS プロトコルドライバーは、ミニポート呼び出しマネージャー (MCMs) で情報を照会または設定することもできます。 OID 要求と MCMs の詳細については、「 [CONMCM Oid 要求](condis-mcm-oid-requests.md)」を参照してください。

基になるドライバーに OID 要求を送信するために、プロトコルドライバーは[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)関数を呼び出し、 *NdisAfHandle*パラメーターでアドレスファミリ (AF) ハンドルを**NULL**に設定します。 OID 要求を別の CoNDIS ドライバーに送信するために、プロトコルドライバーは**NdisCoOidRequest**を呼び出し、有効な AF ハンドルを提供します。

プロトコルドライバーが**NdisCoOidRequest**関数を呼び出すと、NDIS は他のドライバー (基になるドライバーまたは別の condis プロトコルドライバー) の OID 要求関数を呼び出します。 ミニポートドライバーの場合、NDIS は[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を呼び出します。 プロトコルドライバーの場合、NDIS は[**ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request)関数を呼び出します。

次の図は、ミニポートドライバーに送信される OID 要求を示しています。

![ミニポートドライバーに送信される oid 要求を示す図](images/protocolcorequest.png)

次の図は、プロトコルドライバーに送信される OID 要求を示しています。

![プロトコルドライバーに送信される oid 要求を示す図](images/clientcorequest.png)

同期的に完了するには、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)によって、NDIS\_STATUS\_SUCCESS または error status が返されます。 非同期的に完了するために、 **NdisCoOidRequest**は NDIS\_STATUS\_PENDING を返します。

**NdisCoOidRequest**が NDIS\_STATUS\_PENDING を返した場合、Ndis は[**NdisMCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcooidrequestcomplete)関数を呼び出すことによって、他のドライバーが OID 要求を完了した後に[**ProtocolCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete)関数を呼び出します。[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)関数。 この場合、NDIS は*ProtocolCoOidRequestComplete*の*OidRequest*パラメーターに要求の結果を渡します。 NDIS は、 *ProtocolCoOidRequestComplete*の*status*パラメーターに要求の最終状態を渡します。

[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)が NDIS\_STATUS\_SUCCESS を返した場合は、 [**ndis\_OID\_request**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のクエリ要求の結果が、 *OidRequest*パラメーターポイントに返されます。 この場合、NDIS は*ProtocolCoOidRequestComplete*関数を呼び出しません。

基になるドライバーが OID 要求を後続のステータス表示に関連付ける必要がある場合は、プロトコルドライバーによって、NDIS\_OID\_要求構造の**RequestId** **メンバーと要求元**メンバーが設定されます。 基になるドライバーによって状態が示された場合、ドライバーは[**ndis の\_状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**requestid**メンバーを、NDIS\_OID\_要求の**requestid**メンバーからの値に設定します。ndis の\_ステータス\_構造体および**Destinationhandle**メンバーは、NDIS\_OID\_要求構造体**の要求元のメンバーから**の値に構造体を示します。

ドライバーは、バインドが*再起動*、*実行中*、*一時停止*、または*一時停止*状態のときに[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を呼び出すことができます。

 

 





