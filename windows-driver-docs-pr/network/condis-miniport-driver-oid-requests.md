---
title: CoNDIS ミニポート ドライバー OID 要求
description: CoNDIS ミニポート ドライバー OID 要求
ms.assetid: a283d430-f90c-4704-868b-f4086922737b
keywords:
- ミニポートドライバー WDK ネットワーク、CoNDIS
- NDIS ミニポートドライバー WDK、CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75982f1a5be4837da67906465fe8e06ee6367e88
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835138"
---
# <a name="condis-miniport-driver-oid-requests"></a>CoNDIS ミニポート ドライバー OID 要求





NDIS は、CoNDIS ミニポートドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を呼び出して、OID 要求を送信し、ドライバーの情報を照会または設定します。 NDIS は、 *MiniportCoOidRequest*を呼び出すことによって、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)関数を呼び出した別のドライバーに代わって、またはその代わりに呼び出しを行います。

NDIS は、要求情報を含む[**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造*へのポインターを渡します*。 要求構造には、要求データを定義する要求の種類とその他のメンバーを示す OID\_*Xxx*識別子が含まれています。

**タイムアウト**メンバーは、要求のタイムアウトを秒単位で指定します。 ドライバーが要求を完了する前にタイムアウトの期限が切れた場合、NDIS はドライバーをリセットするか、要求をキャンセルできます。

**RequestId**メンバーは、要求のオプションの識別子を指定します。 ミニポートドライバーは、ステータスを示す**requestid**メンバーを、関連付けられた OID 要求の**requestid**メンバーから取得したドライバーの値に設定できます。 通常、ミニポートドライバーは、このメンバーを無視できます。 ドライバーがこのメンバーを設定する必要がある場合、ドライバーは、特定の OID の参照ページで指定されている必須の値のいずれかを使用する必要があります。 ステータスの表示の詳細については、「 [Condis ミニポートドライバーの状態](condis-miniport-driver-status-indications.md)の表示」を参照してください。

ミニポートドライバーは、成功または失敗の状態を返すことによって、OID 要求を同期的に完了させることができます。 ドライバーは、NDIS\_STATUS\_PENDING を返すことによって、OID 要求を非同期的に完了させることができます。 この場合、ドライバーは、操作を完了するために[**NdisMCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcooidrequestcomplete)関数を呼び出す必要があります。

*MiniportCoOidRequest*関数が NDIS\_STATUS\_pending を返した場合、ndis は、保留中の要求が完了する前に、アダプターに対する別の要求を使用して*MiniportCoOidRequest*を呼び出すことができます。 これは、すべての OID 要求をシリアル化するコネクションレス NDIS インターフェイスとは異なることに注意してください。

NDIS は、ミニポートドライバーの[*Miniportcanceloidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request)関数を呼び出して、CONDIS OID 要求を取り消すことができます。

 

 





