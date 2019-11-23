---
title: NDIS フィルター ドライバーでの OID 要求のフィルター処理
description: NDIS フィルター ドライバーでの OID 要求のフィルター処理
ms.assetid: 88bb8318-f19c-4d98-bb06-6120e6adb51d
keywords:
- Oid WDK ネットワーク, フィルタードライバー
- フィルタードライバーでの OID 要求のフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0bba02584bf99913d22c01681e08fff486e1c03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840489"
---
# <a name="filtering-oid-requests-in-an-ndis-filter-driver"></a>NDIS フィルター ドライバーでの OID 要求のフィルター処理





フィルタードライバーは、その後のドライバーによって生成された OID 要求を処理できます。 NDIS は、 [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)関数を呼び出して、各 OID 要求を処理します。 フィルタードライバーは、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)関数を呼び出すことにより、基になるドライバーに OID 要求を転送できます。

NDIS は、フィルタードライバーの[*Filtercanceloidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_oid_request)関数を呼び出して OID 要求を取り消すことができます。 NDIS が*Filtercanceloidrequest*を呼び出すと、フィルタードライバーはできるだけ早く[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)関数を呼び出そうとします。

次の図は、フィルター処理された OID 要求を示しています。

![フィルター処理された oid 要求を示す図](images/requestfilter.png)

フィルタードライバーは、 [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)から、それぞれ NDIS\_STATUS\_SUCCESS または NDIS\_STATUS\_PENDING を返すことによって、OID 要求を同期的または非同期的に完了できます。 *FilterOidRequest*は、エラー状態で同期的に完了することもできます。

OID セット要求を正常に処理するフィルタードライバーは、OID セット要求から戻った時点で、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体で**supportedrevision**メンバーを設定する必要があります。 **Supportedrevision**メンバーは、ドライバーがサポートしているリビジョンに関する OID 要求をイニシエーターに通知します。 NDIS 構造体のバージョン情報の詳細については、「 [Ndis バージョン情報の指定](specifying-ndis-version-information.md)」を参照してください。

*FilterOidRequest*が NDIS\_STATUS\_PENDING を返した場合、OID 要求が完了した後で、 [**NdisFOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete)関数を呼び出す必要があります。 この場合、ドライバーは**NdisFOidRequestComplete**の*OidRequest*パラメーターに要求の結果を渡します。 ドライバーは、要求の最終ステータスを**NdisFOidRequestComplete**の*status*パラメーターに渡します。

*FilterOidRequest*が NDIS\_STATUS\_SUCCESS を返した場合、 [**ndis\_OID\_request**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のクエリ要求の結果が、 *OidRequest*パラメーターに返されます。 この場合、ドライバーは**NdisFOidRequestComplete**関数を呼び出しません。

OID 要求を基になるドライバーに転送するために、フィルタードライバーは[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)関数を呼び出します。 要求を基になるドライバーに転送しない場合、フィルタードライバーは要求を直ちに完了できます。 転送せずに要求を完了するために、ドライバーは*FilterOidRequest*から NDIS\_STATUS\_SUCCESS (またはエラー状態) を返すことができます。また、NDIS\_STATUS\_PENDING を返した後に、 **NdisFOidRequestComplete**を呼び出すこともできます。

**注**  ドライバーが[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す前に、ドライバーは[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を割り当て、 [**NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest)を呼び出して要求情報を新しい構造に転送する必要があります。

 

転送された要求は、フィルタードライバーによって開始された要求と同じように処理されます。 詳細については、「 [NDIS フィルタードライバーからの OID 要求の生成](generating-oid-requests-from-an-ndis-filter-driver.md)」を参照してください。

基になるドライバーが転送された要求を完了した後、フィルタードライバーは必要に応じて応答を変更し、それを後続のドライバーに渡すことができます。

フィルタードライバーは、*再起動*、*実行中*、*一時停止*、または*一時停止*状態にあるときに、それ以降のドライバーから OID 要求を受け取ることができます。

**注**  ミニポートドライバーでは、フィルタードライバーは一度に1つの OID 要求のみを受信できます。 NDIS はフィルターモジュールに送信される要求をシリアル化するため、以前の要求を完了する前に、 *FilterOidRequest*でフィルタードライバーを呼び出すことはできません。

 

OID 要求を変更するフィルタードライバーの例を次に示します。

-   フィルタードライバーはヘッダーを追加します。 この場合、ドライバーが、基になるドライバーからのクエリに対して、 [OID\_GEN\_最大\_フレーム\_サイズ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)の応答を受信すると、そのヘッダーのサイズが応答から減算されます。 ドライバーは、送信された各パケットの前にヘッダーを挿入し、受信した各パケットのヘッダーを削除するため、ドライバーはヘッダーサイズを減算します。

 

 





