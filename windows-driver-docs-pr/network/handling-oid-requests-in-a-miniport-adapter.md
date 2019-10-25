---
title: ミニポート アダプターの OID 要求の処理
description: ミニポート アダプターの OID 要求の処理
ms.assetid: 0819ef06-5715-4814-a1ed-ddc757728ec4
keywords:
- ミニポートドライバー WDK ネットワーク, OID 要求
- Oid WDK ネットワーク、ミニポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bf869c2f8e395dfe3cc38196c82bd8567ffd840
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842575"
---
# <a name="handling-oid-requests-in-a-miniport-adapter"></a>ミニポート アダプターの OID 要求の処理





NDIS は、ミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数を呼び出して、クエリを送信したり、ドライバーの情報を設定したりするための OID 要求を送信します。 NDIS は、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)または[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)関数を呼び出した後のドライバーの代わりに、またはその代わりに*miniportoidrequest*関数を呼び出します。

NDIS は、要求情報を含む[**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造*へのポインターを渡します*。 要求構造には、要求データを定義する要求の種類とその他のメンバーを示す OID\_Xxx 識別子が含まれています。

**タイムアウト**メンバーは、要求のタイムアウトを秒単位で指定します。 ドライバーが要求を完了する前にタイムアウトの期限が切れた場合、NDIS はドライバーをリセットするか、要求をキャンセルできます。

**RequestId**メンバーは、要求のオプションの識別子を指定します。 ミニポートドライバーは、ステータスを示す**requestid**メンバーを、関連付けられた OID 要求の**requestid**メンバーから取得した値に設定できます。 通常、ミニポートドライバーは、このメンバーを無視できます。 ドライバーがこのメンバーを設定する必要がある場合、特定の OID の参照ページに必要な値が表示されます。 ステータスの表示の詳細については、「[アダプターの状態](miniport-adapter-status-indications.md)の表示」を参照してください。

OID セット要求を正常に処理するミニポートドライバーは、OID セット要求から戻ったときに、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体で**supportedrevision**メンバーを設定する必要があります。 **Supportedrevision**メンバーは、ドライバーがサポートしているリビジョンの要求をイニシエーターに通知します。 たとえば、ミニポートドライバーでは、Xxx\_REVISION\_2 の構造を作成し、Xxx\_REVISION\_1 構造に適切な値を指定して、構造体の残りの部分に0を設定できます。 ミニポートドライバーは、 **supportedrevision**メンバーで XXX\_REVISION\_1 を報告します。 この場合、Xxx\_リビジョン\_2 をサポートするプロトコルドライバーでは、ミニポートドライバーがサポートする Xxx\_リビジョン\_1 の情報が使用されます。 NDIS 構造体のバージョン情報の詳細については、「 [Ndis バージョン情報の指定](specifying-ndis-version-information.md)」を参照してください。

ミニポートドライバーは、成功または失敗の状態を返すことによって、OID 要求を同期的に完了させることができます。

ミニポートドライバーは、NDIS\_STATUS\_PENDING を返すことによって、OID 要求を非同期的に完了させることができます。 この場合、ミニポートドライバーは、操作を完了するために[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)関数を呼び出す必要があります。

*Miniportoidrequest*が NDIS\_STATUS\_pending を返した場合、ndis は、保留中の要求が完了するまで、そのアダプターに対する別の要求と共に*miniportoidrequest*を呼び出しません。

NDIS は、ミニポートドライバーの[*Miniportcanceloidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request)関数を呼び出して、OID 要求を取り消すことができます。

 

 





