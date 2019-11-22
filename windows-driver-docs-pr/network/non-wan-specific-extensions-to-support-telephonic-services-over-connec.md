---
title: 接続指向 NDIS 経由の TAPI 向けの WAN 固有ではない拡張機能
description: 接続指向 NDIS 経由で電話サービスをサポートする WAN 固有でない拡張機能
ms.assetid: be677971-8c4a-435a-81b1-ff1ad9d849b4
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、TAPI サービス
- 電話 services WDK WAN、非 WAN 固有の拡張機能
- CoNDIS TAPI WDK ネットワーク、WAN に固有ではない拡張機能
- NDIS/TAPI 変換 Oid WDK ネットワーク
- 接続指向の NDIS WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a108ce51e90f654cd87465a95dcf00fd336b8b87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842767"
---
# <a name="non-wan-specific-extensions-to-support-telephonic-services-over-connection-oriented-ndis"></a>接続指向 NDIS 経由で電話サービスをサポートする WAN 固有でない拡張機能





このトピックでは、接続指向の NDIS での TAPI のサポートに関する WAN 以外の拡張機能について説明します。 これらの拡張機能は、NDIS/TAPI 変換 Oid です。 これらの拡張機能を使用すると、WAN 固有ではない呼び出しマネージャーおよび統合ミニポート呼び出しマネージャー (MCM) ドライバーによって、TAPI パラメーターを NDIS パラメーターまたは TAPI パラメーターに変換することができます。 これらの拡張機能を使用すると、たとえば、ATM をサポートする呼び出しマネージャーと MCMs で、接続指向メディアに対する TAPI アクセスを提供できます。 接続指向 NDIS での TAPI のサポートに関する WAN 固有の拡張機能の詳細については、「[電話 Services をサポートする CONDIS Wan 操作](condis-wan-operations-that-support-telephonic-services.md)」を参照してください。

NDIS/TAPI 変換 Oid は、 [**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)または[**NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex)で CO\_ADDRESS\_ファミリ\_TAPI\_プロキシをそれぞれ登録する呼び出しマネージャーまたは MCMs には使用しないでください。 代わりに、このような通話マネージャーと MCMs、および TAPI クライアントは、[電話 Services をサポートする「CONDIS WAN 操作](condis-wan-operations-that-support-telephonic-services.md)」で説明されているように、接続指向の構造体内に tapi パラメーターをカプセル化する必要があります。

NDIS/TAPI 変換 Oid は次のとおりです。

-   [OID\_CO\_TAPI\_変換\_TAPI\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-callparams)

    この OID は、クライアントによって提供される TAPI 呼び出しパラメーターを NDIS 呼び出しパラメーターに変換するために、呼び出しマネージャーまたは MCM を要求します。 クライアントは、通常、呼び出しマネージャーまたは MCM によって返される NDIS 呼び出しパラメーターを入力として使用します ( [**CO\_call\_parameters**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体として書式設定されます)。これは[**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)です。 クライアントは、 **NdisClMakeCall**を使用して接続指向の呼び出しを開始します。

-   [OID\_CO\_TAPI\_変換\_NDIS\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-ndis-callparams)

    この OID は、呼び出しマネージャーまたは MCM に対して、着信呼び出しの NDIS 呼び出しパラメーター (クライアントの[**ProtocolClIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call)関数への CO\_呼び出し\_パラメーター構造体) を TAPI 呼び出しパラメーターに変換するように要求します。 クライアントは、呼び出しマネージャーまたは MCM によって返された変換済みの TAPI 呼び出しパラメーターを使用して、着信呼び出しを受け入れるか拒否するかを決定します。

-   [OID\_CO\_TAPI\_変換\_SAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-sap)

    この OID は、コールマネージャーまたは MCM に対して、クライアントから提供される TAPI 呼び出しパラメーターから1つまたは複数の NDIS の Sap を準備するように要求します。 クライアントは、通常、呼び出しマネージャーまたは MCM によって返される NDIS SAP を[**NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)に入力 ( [**CO\_SAP**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))構造として書式設定) として使用します。これにより、クライアントは、着信呼び出しを受信する SAP を登録します。

 

 





