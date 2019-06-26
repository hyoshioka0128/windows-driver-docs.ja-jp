---
title: NDIS フィルター ドライバーでの OID 要求のフィルター処理
description: NDIS フィルター ドライバーでの OID 要求のフィルター処理
ms.assetid: 88bb8318-f19c-4d98-bb06-6120e6adb51d
keywords:
- Oid WDK ネットワー キング、フィルター ドライバー
- OID 要求フィルター ドライバーのフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecb6d34d40b620b1a2305d659805e15a253be507
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353335"
---
# <a name="filtering-oid-requests-in-an-ndis-filter-driver"></a>NDIS フィルター ドライバーでの OID 要求のフィルター処理





フィルター ドライバーは、後続のドライバーによって発信された OID 要求を処理できます。 NDIS 呼び出し、 [ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)各 OID 要求を処理する関数。 フィルター ドライバーは呼び出すことによって基になるドライバーに OID 要求を転送することができます、 [ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)関数。

NDIS フィルター ドライバーを呼び出すことができます[ *FilterCancelOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_cancel_oid_request) OID 要求をキャンセルする関数。 NDIS を呼び出すと*FilterCancelOidRequest*、呼び出すしようとする必要があります、フィルター ドライバー、 [ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)できるだけ早く関数。

次の図は、フィルター選択された OID 要求を示しています。

![フィルター選択された oid 要求を示す図](images/requestfilter.png)

フィルター ドライバーは、要求を完了 OID 同期または非同期で NDIS を返すことによって\_状態\_成功または NDIS\_状態\_PENDING からそれぞれ[ *FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)します。 *FilterOidRequest*はエラー状態を同期的に完了もできます。

OID のセット要求を正常に処理するフィルター ドライバーを設定する必要があります、 **SupportedRevision**内のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)OID のセットの要求からの戻り時に構造体。 **SupportedRevision**メンバーにサポートされているドライバーのリビジョンに関する OID 要求の発信側に通知します。 NDIS 構造のバージョン情報の詳細については、次を参照してください。 [NDIS バージョン情報を指定する](specifying-ndis-version-information.md)します。

場合*FilterOidRequest*返します NDIS\_状態\_保留中、呼び出す必要があります、 [ **NdisFOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequestcomplete)関数が完了した後OID 要求。 この場合、ドライバーに渡しますで要求の結果、 *OidRequest*パラメーターの**NdisFOidRequestComplete**します。 ドライバーで要求の最終的な状態を渡す、*状態*パラメーターの**NdisFOidRequestComplete**します。

場合*FilterOidRequest* NDIS を返します\_状態\_成功するでのクエリ要求の結果が返されますが、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)で構造体、 *OidRequest*パラメーター。 この場合、ドライバーは呼び出しません、 **NdisFOidRequestComplete**関数。

フィルター ドライバーの呼び出しを基になるドライバーの OID 要求を転送するように、 [ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)関数。 基になるドライバーに要求を転送しないよう場合、フィルター ドライバーは、要求をすぐに完了できます。 転送なし要求を完了するには、ドライバーは NDIS を返す\_状態\_成功 (またはエラー状態) から*FilterOidRequest*、呼び出すこともできます**NdisFOidRequestComplete** NDIS が返された後\_状態\_保留します。

**注**  ドライバー呼び出しの前に[ **NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)、ドライバーを割り当てる必要があります、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体し、新しい構造に呼び出すことによって、要求の情報を転送[ **NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatecloneoidrequest)します。

 

転送された要求では、フィルター ドライバーによって開始された要求と同じ処理されます。 詳細については、次を参照してください。 [NDIS フィルター ドライバーから OID の要求を生成する](generating-oid-requests-from-an-ndis-filter-driver.md)します。

転送された要求を完了すると、基になるドライバー、フィルター ドライバーは、必要に応じて、応答を変更し、関連ドライバーに渡すことできます。

フィルター ドライバーがあるときにドライバーを後続の OID 要求を受信できる、*再起動*、*を実行している*、*一時停止中*、または*Paused*状態。

**注**  のミニポート ドライバーのようにフィルター ドライバーは、一度に 1 つだけの OID 要求を受信できます。 フィルター ドライバーを呼び出すことはできませんので、NDIS フィルター モジュールに送信される要求をシリアル化、 *FilterOidRequest*前回の要求を完了する前にします。

 

OID 要求を変更するフィルター ドライバーの例を次に示します。

-   フィルター ドライバーでは、ヘッダーを追加します。 この場合は、ドライバーは、に対するクエリへの応答を受信した後で[OID\_GEN\_最大\_フレーム\_サイズ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)フィルターを基になるドライバーからのヘッダーのサイズを減算します応答。 ドライバーは、ドライバーが各送信パケットの前に、ヘッダーを挿入し、各受信パケットのヘッダーを削除するためにそのヘッダーのサイズを減算します。

 

 





