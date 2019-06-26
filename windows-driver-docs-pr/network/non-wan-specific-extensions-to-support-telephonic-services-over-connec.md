---
title: 接続指向の NDIS 経由で TAPI の WAN 特定されていない拡張機能
description: 接続指向 NDIS 経由で電話サービスをサポートする WAN 固有でない拡張機能
ms.assetid: be677971-8c4a-435a-81b1-ff1ad9d849b4
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、TAPI サービス
- 電話サービス WDK WAN、WAN 固有の拡張機能
- いる CoNDIS TAPI WDK ネットワーク、WAN 特定されていない拡張機能
- NDIS/TAPI 翻訳 Oid WDK ネットワーク
- 接続指向の NDIS WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa5744ef33c0e2485e374c10ec07bbcf69dd5ce6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354533"
---
# <a name="non-wan-specific-extensions-to-support-telephonic-services-over-connection-oriented-ndis"></a>接続指向 NDIS 経由で電話サービスをサポートする WAN 固有でない拡張機能





このトピックでは、接続指向の NDIS 経由での TAPI サポート WAN 特定されていない拡張機能について説明します。 これらの拡張機能は、NDIS/TAPI 翻訳 Oid です。 これらの拡張機能は、NDIS パラメーターまたは TAPI パラメーターを NDIS パラメーターに TAPI パラメーターを変換するには、WAN 特定されていない呼び出しマネージャーと統合ミニポート コール マネージャー (MCM) ドライバーを許可します。 これらの拡張機能は、コール マネージャーとの接続指向のメディアを介した TAPI アクセスを提供する ATM などをサポートする MCMs を許可します。 接続指向の NDIS 経由の TAPI サポートの WAN 固有の拡張機能については、次を参照してください。[いる CoNDIS WAN 操作サポートの電話サービスのその](condis-wan-operations-that-support-telephonic-services.md)します。

呼び出しの管理者または共同をそれぞれ登録 MCMs NDIS/TAPI 翻訳 Oid を使用しない必要があります\_アドレス\_ファミリ\_TAPI\_プロキシを[ **NdisCmRegisterAddressFamilyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmregisteraddressfamilyex)または[ **NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmregisteraddressfamilyex)します。 代わりに、マネージャーと MCMs、さらに、TAPI クライアントを呼び出すなど、」の説明に従って、接続指向の構造内に TAPI パラメーターをカプセル化する必要があります[いる CoNDIS WAN 操作電話サービスをサポートする](condis-wan-operations-that-support-telephonic-services.md)します。

NDIS/TAPI 翻訳 Oid 次に示します。

-   [OID\_CO\_TAPI\_TRANSLATE\_TAPI\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-callparams)

    この OID は、NDIS 呼び出しのパラメーターにクライアントによって提供される TAPI 呼び出しのパラメーターを変換するには、コール マネージャーまたは MCM を要求します。 クライアントは通常、コール マネージャーまたは入力として MCM によって返される NDIS 呼び出しパラメーターを使用して (として書式設定、 [ **CO\_呼び出す\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造)に[ **NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmakecall)します。 クライアントを使用して**NdisClMakeCall**接続指向の呼び出しを開始します。

-   [OID\_CO\_TAPI\_TRANSLATE\_NDIS\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-ndis-callparams)

    この OID 要求が着信呼び出しの NDIS 呼び出しのパラメーターを変換するには、コール マネージャーまたは MCM (CO に渡される\_呼び出す\_パラメーター構造体、クライアントの[ **ProtocolClIncomingCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_call)関数) から TAPI には、呼び出しパラメーター。 クライアントでは、コール マネージャーまたは MCM によって返される翻訳された TAPI 呼び出しパラメーターを使用して、受け入れるか、着信通話を拒否するかどうかを判断します。

-   [OID\_CO\_TAPI\_TRANSLATE\_SAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-sap)

    この OID は、クライアントによって提供される TAPI 呼び出しパラメーターから 1 つまたは複数の NDIS SAPs を準備するには、コール マネージャーまたは MCM を要求します。 クライアントは通常、コール マネージャーまたは入力として MCM によって返される NDIS SAP を使用 (として書式設定、 [ **CO\_SAP** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))構造) に[ **NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclregistersap)クライアントが着信呼び出しを受信する SAP を登録します。

 

 





