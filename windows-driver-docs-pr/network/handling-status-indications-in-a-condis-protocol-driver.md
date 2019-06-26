---
title: CoNDIS プロトコル ドライバーでの状態表示の処理
description: CoNDIS プロトコル ドライバーでの状態表示の処理
ms.assetid: 948df51b-0561-4b67-b87f-e1652bb18772
keywords:
- プロトコル ドライバー WDK ネットワー キング、いる CoNDIS
- NDIS プロトコル ドライバー WDK、いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7a87e0f391e5c7919e388f4e7a569ce9edb73e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381356"
---
# <a name="handling-status-indications-in-a-condis-protocol-driver"></a>CoNDIS プロトコル ドライバーでの状態表示の処理





プロトコル ドライバーを指定する必要があります、 [ **ProtocolCoStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex) NDIS が、基になるドライバーの状態を報告したときに呼び出す関数です。

NDIS 呼び出しプロトコル ドライバーの*ProtocolCoStatusEx*関数の状態を示す値の関数を呼び出して、基になるドライバーから (たとえば、 [ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)). 詳細については、ミニポート ドライバーからの状態を示す、次を参照してください。[いる CoNDIS ミニポート ドライバーの状態インジケーター](condis-miniport-driver-status-indications.md)します。

状態の表示が OID 要求に関連付けられている場合は、基になるドライバーを設定できます、 **DestinationHandle**と**RequestId**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication) NDIS は、特定のプロトコル バインドに、状態を示す値を提供できるように、状態情報を含む構造体。 OID 要求の詳細については、次を参照してください。[いる CoNDIS プロトコル ドライバー OID 要求](condis-protocol-driver-oid-requests.md)します。

 

 





