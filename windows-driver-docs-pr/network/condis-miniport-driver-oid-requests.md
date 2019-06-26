---
title: CoNDIS ミニポート ドライバー OID 要求
description: CoNDIS ミニポート ドライバー OID 要求
ms.assetid: a283d430-f90c-4704-868b-f4086922737b
keywords:
- ミニポート ドライバー WDK ネットワー キング、いる CoNDIS
- NDIS ミニポート ドライバー WDK、いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae657f4877940b44d9e737dbb9266709732f9a4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379240"
---
# <a name="condis-miniport-driver-oid-requests"></a>CoNDIS ミニポート ドライバー OID 要求





NDIS は呼び出している CoNDIS ミニポート ドライバーの[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)クエリまたはドライバーの情報を設定する OID 要求を送信する関数。 NDIS 呼び出し*MiniportCoOidRequest*自身が代理として、または呼び出される上位のドライバーに代わって、 [ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)関数。

NDIS 渡します*MiniportCoOidRequest*へのポインター、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)要求情報を含む構造体。 要求の構造には、OID が含まれています。\_*Xxx*要求データを定義するには、要求とその他のメンバーの種類を示す識別子です。

**タイムアウト**メンバーは、秒単位の要求で、タイムアウトを指定します。 NDIS は、ドライバーをリセットしたり、ドライバーは、要求を完了する前にタイムアウトに達すると、要求をキャンセルできます。

**RequestId**メンバーは、要求のオプションの識別子を指定します。 ミニポート ドライバーを設定できる、 **RequestId**ドライバーがから取得した値に状態表示のメンバー、 **RequestId**関連付けられている OID 要求のメンバー。 通常、ミニポート ドライバーでは、このメンバーを無視できます。 ドライバーは、このメンバーを設定する必要がある場合、ドライバーは、特定の OID のリファレンス ページで指定された必要な値のいずれかを使用する必要があります。 状態インジケーターの詳細については、次を参照してください。[いる CoNDIS ミニポート ドライバーの状態インジケーター](condis-miniport-driver-status-indications.md)します。

ミニポート ドライバーは、成功または失敗の状態を返すことによって、OID 要求を同期的に完了できます。 ドライバーは NDIS を返すことによって、OID 要求を非同期的に実行できる\_状態\_保留します。 この場合、ドライバーを呼び出す必要があります、 [ **NdisMCoOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcooidrequestcomplete)操作を完了する関数。

場合、 *MiniportCoOidRequest*返します NDIS\_状態\_保留中、NDIS を呼び出すことができます*MiniportCoOidRequest*別の要求をする前に、アダプターで、保留中要求が完了したとします。 これは OID のすべての要求がシリアル化、コネクションレスの NDIS インターフェイスを異なることに注意してください。

NDIS ミニポート ドライバーを呼び出すことができます[ *MiniportCancelOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_oid_request)いる CoNDIS OID 要求をキャンセルする関数。

 

 





