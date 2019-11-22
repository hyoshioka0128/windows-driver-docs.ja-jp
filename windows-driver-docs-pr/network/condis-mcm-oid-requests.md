---
title: CoNDIS MCM OID 要求
description: CoNDIS MCM OID 要求
ms.assetid: efddbcb0-98f1-4cd3-9707-f3ed17c20181
keywords:
- ミニポート呼び出しマネージャー WDK ネットワーク, OID 要求
- MCMs WDK ネットワーク, OID 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fe8b5ebb15fd440f923f9511a7180ef4bc703c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835153"
---
# <a name="condis-mcm-oid-requests"></a>CoNDIS MCM OID 要求





他の condis call マネージャーと同様に、ミニポートコールマネージャー (MCMs) は、condis client ドライバーの操作パラメーターを照会または設定できます。 CoNDIS クライアントドライバーは、MCM の呼び出しマネージャーパラメーターまたはミニポートドライバーパラメーターを照会または設定できます。

CoNDIS クライアントドライバーに OID 要求を送信するために、MCM は[**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequest)関数を呼び出します。

次の図は、MCM が生成された OID 要求を示しています。

![mcm の生成元である oid 要求を示す図](images/mcmcorequest.png)

MCM ドライバーが[**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequest)関数を呼び出すと、NDIS はクライアントドライバーの[**ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request)関数を呼び出します。

同期的に完了するには、 **NdisMCmOidRequest**によって、NDIS\_STATUS\_SUCCESS または error status が返されます。 非同期的に完了するために、 **NdisMCmOidRequest**は NDIS\_STATUS\_PENDING を返します。

[**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequest)が NDIS\_STATUS\_PENDING を返した場合、Ndis は[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)を呼び出して、クライアントドライバーが OID 要求を完了した後に mcm の[**ProtocolCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete)関数を呼び出します。プロシージャ. この場合、NDIS は*ProtocolCoOidRequestComplete*の*OidRequest*パラメーターに要求の結果を渡します。 NDIS は、 *ProtocolCoOidRequestComplete*の*status*パラメーターに要求の最終状態を渡します。

**NdisMCmOidRequest**が NDIS\_STATUS\_SUCCESS を返した場合、 [**ndis\_OID\_request**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のクエリ要求の結果が、 *OidRequest*パラメーターに返されます。 この場合、NDIS は MCM の*ProtocolCoOidRequestComplete*関数を呼び出しません。

CoNDIS client ドライバーは、MCMs の呼び出しマネージャーの操作パラメーターまたはミニポート操作パラメーターを照会または設定できます。 MCM call manager パラメーターの OID 要求を開始するために、クライアントは[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)関数を呼び出し、 *NdisAfHandle*パラメーターに有効なアドレスファミリ (AF) ハンドルを提供します。 MCM ミニポートパラメーターの OID 要求を開始するために、クライアントは**NdisCoOidRequest**関数を呼び出し、AF ハンドルを**NULL**に設定します。

クライアントが**NdisCoOidRequest**関数を呼び出すと、NDIS は mcm ドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数または[**ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request)関数のいずれかを呼び出します。

次の図は、MCM のミニポートパラメーターに対する OID 要求を示しています。

![mcm のミニポートパラメーターの oid 要求を示す図](images/protocol2mcmcorequest.png)

次の図は、MCM の call manager パラメーターに対する OID 要求を示しています。

![mcm の call manager パラメーターに対する oid 要求を示す図](images/client2mcmcorequest.png)

同期的に完了するには、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)によって、NDIS\_STATUS\_SUCCESS または error status が返されます。 非同期的に完了するために、 [**ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request)または[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)は NDIS\_STATUS\_PENDING を返します。

*ProtocolCoOidRequest*または**MininportCoOidRequest**が NDIS\_STATUS\_PENDING を返した場合、ndis は[**NdisMCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcooidrequestcomplete)または[**NdisMCmOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequestcomplete)関数を呼び出して OID 要求を完了した後に、クライアントの[**ProtocolCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request_complete)関数を呼び出します。 この場合、NDIS は*ProtocolCoOidRequestComplete*の*OidRequest*パラメーターに要求の結果を渡します。 NDIS は、 *ProtocolCoOidRequestComplete*の*status*パラメーターに要求の最終状態を渡します。

[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)が NDIS\_STATUS\_SUCCESS を返した場合、 [**ndis\_OID\_request**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のクエリ要求の結果が、 *OidRequest*パラメーターに返されます。 この場合、NDIS はクライアントの*ProtocolCoOidRequestComplete*関数を呼び出しません。

 

 





