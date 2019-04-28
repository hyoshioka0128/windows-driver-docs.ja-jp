---
title: CoNDIS プロトコル ドライバー OID 要求
description: CoNDIS プロトコル ドライバー OID 要求
ms.assetid: 1338d199-2cd8-430a-a0a5-95aaea04c384
keywords:
- プロトコル ドライバー WDK ネットワー キング、いる CoNDIS
- NDIS プロトコル ドライバー WDK、いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4f89e3c2366793d1c333bad592dc5fefb3ec142
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366777"
---
# <a name="condis-protocol-driver-oid-requests"></a>CoNDIS プロトコル ドライバー OID 要求





いる CoNDIS ドライバー、クライアントまたは呼び出しのマネージャーのいずれかのプロトコル、クエリを実行したり、ミニポート ドライバーおよびその他のプロトコル ドライバーの動作のパラメーターを設定できます。 いる CoNDIS プロトコル ドライバーはクエリを実行したり、ミニポート コール マネージャー (MCMs) で情報を設定できます。 OID 要求と MCMs に関する詳細については、次を参照してください。[いる CoNDIS MCM OID 要求](condis-mcm-oid-requests.md)します。

プロトコル ドライバーを呼び出す、基になるドライバーに、OID 要求を発信、 [ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)関数およびアドレス ファミリ (AF) ハンドル セットは、 *NdisAfHandle*パラメーターに、 **NULL**します。 プロトコル ドライバーを呼び出している CoNDIS プロトコル ドライバーのもう 1 つの OID 要求を発信**NdisCoOidRequest**し AF の有効なハンドルを提供します。

プロトコル ドライバーを呼び出してから、 **NdisCoOidRequest**関数、NDIS は、その他のドライバー (基になるドライバーまたは別のいる CoNDIS プロトコル ドライバー) の OID 要求関数を呼び出します。 ミニポート ドライバーでは、NDIS 呼び出し、 [ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)関数。 プロトコル ドライバーでは、NDIS 呼び出し、 [ **ProtocolCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff570254)関数。

次の図は、送信先のミニポート ドライバーの OID 要求を示しています。

![送信先のミニポート ドライバーの oid 要求を示す図](images/protocolcorequest.png)

次の図では、プロトコル ドライバーに送信する OID 要求を示しています。

![プロトコル ドライバーに送信する oid 要求を示す図](images/clientcorequest.png)

同期的に完了する[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)返します NDIS\_状態\_成功またはエラー状態です。 非同期的に完了する**NdisCoOidRequest**返します NDIS\_状態\_保留します。

場合**NdisCoOidRequest**返します NDIS\_状態\_保留中、NDIS 呼び出し、 [ **ProtocolCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570255)関数の後、その他ドライバーは、呼び出すことにより、OID 要求を完了、 [ **NdisMCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563568)関数または[ **NdisCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561716)関数。 ここでは、NDIS がで要求の結果を渡す、 *OidRequest*パラメーターの*ProtocolCoOidRequestComplete*します。 NDIS 渡しますで要求の最終的な状態、*状態*パラメーターの*ProtocolCoOidRequestComplete*します。

場合[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)返します NDIS\_状態\_成功すると、クエリ要求の結果を[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)で構造体、 *OidRequest*パラメーター ポイント。 この場合は、NDIS は呼び出しません、 *ProtocolCoOidRequestComplete*関数。

場合は、基になるドライバーは、それ以降の状態を示す値を OID 要求を関連付ける必要があります、プロトコル ドライバーに設定する必要があります、 **RequestId**と**RequestHandle** NDIS でメンバー\_OID\_要求の構造。 基になるドライバーは、状態の表示を行う場合、ドライバーの設定、 **RequestId**内のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体から値を**RequestId**の NDIS メンバー\_OID\_要求の構造と**DestinationHandle** NDISでメンバー\_状態\_を示す値構造体から値を**RequestHandle**の NDIS メンバー\_OID\_要求の構造。

ドライバーを呼び出すことができます[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)でバインディングの場合、*再起動*、*を実行している*、 *を一時停止中*、または*Paused*状態。

 

 





