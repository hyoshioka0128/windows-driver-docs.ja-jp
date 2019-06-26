---
title: CoNDIS MCM OID 要求
description: CoNDIS MCM OID 要求
ms.assetid: efddbcb0-98f1-4cd3-9707-f3ed17c20181
keywords:
- ミニポート コール マネージャー WDK ネットワー キング、OID 要求
- MCMs WDK ネットワーク、OID 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e32c73d1f2d7b375eedeb04f8f2b947889a122b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379266"
---
# <a name="condis-mcm-oid-requests"></a>CoNDIS MCM OID 要求





その他のいる CoNDIS コール マネージャーのようなミニポート コール マネージャー (MCMs) はクエリか、いる CoNDIS クライアント ドライバーの動作のパラメーターを設定できます。 いる CoNDIS クライアント ドライバーでは、クエリを実行したり、または呼び出し manager パラメーターを MCM のミニポート ドライバーのパラメーターを設定することができます。

MCM を呼び出している CoNDIS クライアント ドライバーの OID 要求を発信、 [ **NdisMCmOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequest)関数。

次の図は、MCM で発生した OID 要求を示しています。

![mcm で発生した oid 要求を示す図](images/mcmcorequest.png)

MCM にドライバーを呼び出してから、 [ **NdisMCmOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequest)関数では、NDIS 呼び出し、 [ **ProtocolCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request)クライアントの関数ドライバー。

同期的に完了する**NdisMCmOidRequest**返します NDIS\_状態\_成功またはエラー状態です。 非同期的に完了する**NdisMCmOidRequest**返します NDIS\_状態\_保留します。

場合[ **NdisMCmOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequest)返します NDIS\_状態\_保留中、NDIS 呼び出し、 [ **ProtocolCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request_complete)クライアント ドライバーが呼び出すことによって、OID 要求を完了した後の MCM の関数、 [ **NdisCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)関数。 ここでは、NDIS がで要求の結果を渡す、 *OidRequest*パラメーターの*ProtocolCoOidRequestComplete*します。 NDIS 渡しますで要求の最終的な状態、*状態*パラメーターの*ProtocolCoOidRequestComplete*します。

場合**NdisMCmOidRequest** NDIS を返します\_状態\_成功するでのクエリ要求の結果が返されますが、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)で構造体、 *OidRequest*パラメーター。 この場合は、NDIS は呼び出しません、 *ProtocolCoOidRequestComplete* MCM の関数。

いる CoNDIS クライアント ドライバーでは、クエリを実行したり、コール マネージャーの操作パラメーターまたはミニポート MCMs のパラメーターを設定することができます。 クライアントが呼び出す、MCM コール マネージャーのパラメーターの OID の要求を発信、 [ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)関数し、で有効なアドレス ファミリ (AF) のハンドルを提供します、 *NdisAfHandle*パラメーター。 MCM ミニポート パラメーターの OID 要求の送信元をクライアントが呼び出す、 **NdisCoOidRequest**関数し、AF ハンドルを設定**NULL**します。

クライアントを呼び出してから、 **NdisCoOidRequest**関数、NDIS 呼び出すか、 [ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)関数または[ **ProtocolCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request) MCM ドライバーの機能です。

次の図では、ミニポート パラメーター、MCM の OID 要求を示しています。

![oid 要求を mcm のミニポート パラメーターを示す図](images/protocol2mcmcorequest.png)

次の図は、MCM のコール マネージャーのパラメーターの OID 要求を示しています。

![oid 要求を mcm のコール マネージャーのパラメーターを示す図](images/client2mcmcorequest.png)

同期的に完了する[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)返します NDIS\_状態\_成功またはエラー状態です。 非同期的に完了する[ **ProtocolCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request)または[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)返します NDIS\_状態\_保留します。

場合*ProtocolCoOidRequest*または**MininportCoOidRequest**返します NDIS\_状態\_保留中、NDIS 呼び出し、 [ **ProtocolCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request_complete) 、MCM が呼び出すことにより、OID 要求を完了した後、クライアントの関数、 [ **NdisMCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcooidrequestcomplete)または[ **NdisMCmOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequestcomplete)関数。 ここでは、NDIS がで要求の結果を渡す、 *OidRequest*パラメーターの*ProtocolCoOidRequestComplete*します。 NDIS 渡しますで要求の最終的な状態、*状態*パラメーターの*ProtocolCoOidRequestComplete*します。

場合[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)返します NDIS\_状態\_成功すると、クエリ要求の結果を[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)で構造体、 *OidRequest*パラメーター。 ここで、NDIS には、クライアントは呼び出しません*ProtocolCoOidRequestComplete*関数。

 

 





