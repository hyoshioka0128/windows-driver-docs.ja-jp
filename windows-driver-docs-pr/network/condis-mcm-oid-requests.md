---
title: CoNDIS MCM OID 要求
description: CoNDIS MCM OID 要求
ms.assetid: efddbcb0-98f1-4cd3-9707-f3ed17c20181
keywords:
- ミニポート コール マネージャー WDK ネットワー キング、OID 要求
- MCMs WDK ネットワーク、OID 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acb7bbd1f0b49740783a344976bc6c1ba4c89e65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344317"
---
# <a name="condis-mcm-oid-requests"></a>CoNDIS MCM OID 要求





その他のいる CoNDIS コール マネージャーのようなミニポート コール マネージャー (MCMs) はクエリか、いる CoNDIS クライアント ドライバーの動作のパラメーターを設定できます。 いる CoNDIS クライアント ドライバーでは、クエリを実行したり、または呼び出し manager パラメーターを MCM のミニポート ドライバーのパラメーターを設定することができます。

MCM を呼び出している CoNDIS クライアント ドライバーの OID 要求を発信、 [ **NdisMCmOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563548)関数。

次の図は、MCM で発生した OID 要求を示しています。

![mcm で発生した oid 要求を示す図](images/mcmcorequest.png)

MCM にドライバーを呼び出してから、 [ **NdisMCmOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563548)関数では、NDIS 呼び出し、 [ **ProtocolCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff570254)クライアントの関数ドライバー。

同期的に完了する**NdisMCmOidRequest**返します NDIS\_状態\_成功またはエラー状態です。 非同期的に完了する**NdisMCmOidRequest**返します NDIS\_状態\_保留します。

場合[ **NdisMCmOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563548)返します NDIS\_状態\_保留中、NDIS 呼び出し、 [ **ProtocolCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff570255)クライアント ドライバーが呼び出すことによって、OID 要求を完了した後の MCM の関数、 [ **NdisCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561716)関数。 ここでは、NDIS がで要求の結果を渡す、 *OidRequest*パラメーターの*ProtocolCoOidRequestComplete*します。 NDIS 渡しますで要求の最終的な状態、*状態*パラメーターの*ProtocolCoOidRequestComplete*します。

場合**NdisMCmOidRequest** NDIS を返します\_状態\_成功するでのクエリ要求の結果が返されますが、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)で構造体、 *OidRequest*パラメーター。 この場合は、NDIS は呼び出しません、 *ProtocolCoOidRequestComplete* MCM の関数。

いる CoNDIS クライアント ドライバーでは、クエリを実行したり、コール マネージャーの操作パラメーターまたはミニポート MCMs のパラメーターを設定することができます。 クライアントが呼び出す、MCM コール マネージャーのパラメーターの OID の要求を発信、 [ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)関数し、で有効なアドレス ファミリ (AF) のハンドルを提供します、 *NdisAfHandle*パラメーター。 MCM ミニポート パラメーターの OID 要求の送信元をクライアントが呼び出す、 **NdisCoOidRequest**関数し、AF ハンドルを設定**NULL**します。

クライアントを呼び出してから、 **NdisCoOidRequest**関数、NDIS 呼び出すか、 [ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)関数または[ **ProtocolCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff570254) MCM ドライバーの機能です。

次の図では、ミニポート パラメーター、MCM の OID 要求を示しています。

![oid 要求を mcm のミニポート パラメーターを示す図](images/protocol2mcmcorequest.png)

次の図は、MCM のコール マネージャーのパラメーターの OID 要求を示しています。

![oid 要求を mcm のコール マネージャーのパラメーターを示す図](images/client2mcmcorequest.png)

同期的に完了する[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)返します NDIS\_状態\_成功またはエラー状態です。 非同期的に完了する[ **ProtocolCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff570254)または[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)返します NDIS\_状態\_保留します。

場合*ProtocolCoOidRequest*または**MininportCoOidRequest**返します NDIS\_状態\_保留中、NDIS 呼び出し、 [ **ProtocolCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570255) 、MCM が呼び出すことにより、OID 要求を完了した後、クライアントの関数、 [ **NdisMCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563568)または[ **NdisMCmOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563551)関数。 ここでは、NDIS がで要求の結果を渡す、 *OidRequest*パラメーターの*ProtocolCoOidRequestComplete*します。 NDIS 渡しますで要求の最終的な状態、*状態*パラメーターの*ProtocolCoOidRequestComplete*します。

場合[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)返します NDIS\_状態\_成功すると、クエリ要求の結果を[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)で構造体、 *OidRequest*パラメーター。 ここで、NDIS には、クライアントは呼び出しません*ProtocolCoOidRequestComplete*関数。

 

 





