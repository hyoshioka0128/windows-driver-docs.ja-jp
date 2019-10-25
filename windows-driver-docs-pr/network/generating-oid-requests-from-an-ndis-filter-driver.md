---
title: NDIS フィルター ドライバーからの OID 要求の生成
description: NDIS フィルター ドライバーからの OID 要求の生成
ms.assetid: 6567bf98-bf56-4337-8670-af4c78d2c947
keywords:
- Oid WDK ネットワーク, フィルタードライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da0623e57bd66bd265fd579cb889384f54288ea5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842184"
---
# <a name="generating-oid-requests-from-an-ndis-filter-driver"></a>NDIS フィルター ドライバーからの OID 要求の生成





フィルタードライバーは、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)関数を呼び出すことによって、OID クエリを開始したり、基になるドライバーに要求を設定したりできます。

次の図は、フィルタードライバーによって生成される OID 要求を示しています。

![フィルタードライバーによって生成された oid 要求を示す図](images/filterrequest.png)

フィルタードライバーが[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)関数を呼び出すと、NDIS は、次に基になるドライバーの要求関数を呼び出します。 ミニポートドライバーが OID 要求を処理する方法の詳細については、「[アダプターに対する Oid 要求](miniport-adapter-oid-requests.md)」を参照してください。

同期的に完了するには、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)によって、NDIS\_STATUS\_SUCCESS または error status が返されます。 非同期的に完了するために、 **NdisFOidRequest**は NDIS\_STATUS\_PENDING を返します。

基になるドライバーによって正常に処理された情報を調べるには、oid 要求を発行するフィルタードライバーが、oid 要求の後に、NDIS\_OID\_要求構造の**Supportedrevision**メンバーの値を確認する必要があります。型. NDIS バージョン情報の詳細については、「 [Ndis バージョン情報の指定](specifying-ndis-version-information.md)」を参照してください。

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)が NDIS\_STATUS\_PENDING を返した場合、ndis は基になるドライバーが OID 要求を完了した後に、 [*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)関数を呼び出します。 この場合、NDIS は*FilterOidRequestComplete*の*OidRequest*パラメーターに要求の結果を渡します。 NDIS は、 *FilterOidRequestComplete*の*status*パラメーターに要求の最終状態を渡します。

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)が NDIS\_STATUS\_SUCCESS を返した場合、 [**ndis\_OID\_request**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のクエリ要求の結果が、 *OidRequest*パラメーターに返されます。 この場合、NDIS は[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)関数を呼び出しません。

ドライバーは、*再起動*、*実行中*、*一時停止*、または*一時停止*状態のときに[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出すことができます。

フィルタードライバーは、生成された OID 要求を追跡し、そのような要求が完了したときに[**NdisFOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete)関数を呼び出さないようにする必要があることに  **注意**してください。

 

 

 





