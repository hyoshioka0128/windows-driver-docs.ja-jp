---
title: NDIS プロトコル ドライバーからの OID 要求の生成
description: NDIS プロトコル ドライバーからの OID 要求の生成
ms.assetid: a27d1c9c-fc7e-414f-8cad-595e8d8fe8f8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd3a85ce6e319ac687303d5ad199d0c1e0ce7c33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842182"
---
# <a name="generating-oid-requests-from-an-ndis-protocol-driver"></a>NDIS プロトコル ドライバーからの OID 要求の生成





基になるドライバーに OID 要求を送信するために、プロトコルは[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)関数を呼び出します。

次の図は、プロトコルドライバーによって生成される OID 要求を示しています。

![プロトコルドライバーによって生成された oid 要求を示す図](images/protocolrequest.png)

プロトコルドライバーが[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)関数を呼び出すと、NDIS は、次に基になるドライバーの要求関数を呼び出します。 ミニポートドライバーが OID 要求を処理する方法の詳細については、「[アダプターに対する Oid 要求](miniport-adapter-oid-requests.md)」を参照してください。 フィルタードライバーが OID 要求を処理する方法の詳細については、「[フィルターモジュール OID 要求](filter-module-oid-requests.md)」を参照してください。

同期的に完了するには、 **NdisOidRequest**によって、NDIS\_STATUS\_SUCCESS または error status が返されます。 非同期的に完了するために、 **NdisOidRequest**は NDIS\_STATUS\_PENDING を返します。

**NdisOidRequest**が NDIS\_STATUS\_PENDING を返した場合、ndis は基になるドライバーが OID 要求を完了した後に、 [**ProtocolOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete)関数を呼び出します。 この場合、NDIS は*ProtocolOidRequestComplete*の*OidRequest*パラメーターに要求の結果を渡します。 NDIS は、 *ProtocolOidRequestComplete*の*status*パラメーターに要求の最終状態を渡します。

**NdisOidRequest**が NDIS\_STATUS\_SUCCESS を返した場合、 [**ndis\_OID\_request**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のクエリ要求の結果が、 *OidRequest*パラメーターに返されます。 この場合、NDIS は*ProtocolOidRequestComplete*関数を呼び出しません。

基になるドライバーによって正常に処理された情報を確認するには、oid 要求を発行するプロトコルドライバーが、oid 要求の後に、NDIS\_OID\_要求構造の**Supportedrevision**メンバーの値を確認する必要があります。型. NDIS バージョン情報の詳細については、「 [Ndis バージョン情報の指定](specifying-ndis-version-information.md)」を参照してください。

基になるドライバーが OID 要求を後続のステータス表示に関連付ける必要がある場合は、プロトコルドライバーによって、NDIS\_OID\_要求構造に**RequestId**メンバーが設定されます。 基になるドライバーがステータスを表示すると、 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造の**REQUESTID**メンバーが OID 要求で提供される値に設定されます。

ドライバーは、バインドが*再起動*、*実行中*、*一時停止*、または*一時停止*状態のときに**NdisOidRequest**を呼び出すことができます。

 

 





