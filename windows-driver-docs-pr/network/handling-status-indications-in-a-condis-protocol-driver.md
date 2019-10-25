---
title: CoNDIS プロトコル ドライバーでの状態表示の処理
description: CoNDIS プロトコル ドライバーでの状態表示の処理
ms.assetid: 948df51b-0561-4b67-b87f-e1652bb18772
keywords:
- プロトコルドライバー WDK ネットワーク、CoNDIS
- NDIS プロトコルドライバー WDK、CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2525106988337cfb39f4104be4db9d8e1488ec39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842558"
---
# <a name="handling-status-indications-in-a-condis-protocol-driver"></a>CoNDIS プロトコル ドライバーでの状態表示の処理





プロトコルドライバーは、基になるドライバーがステータスを報告したときに NDIS が呼び出す[**Protocolcostatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)関数を提供する必要があります。

NDIS は、基になるドライバーがステータス表示関数 ( [**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)など) を呼び出すと、プロトコルドライバーの*Protocolcostatusex*関数を呼び出します。 ミニポートドライバーの状態を示す詳細については、「 [Condis ミニポートドライバーの状態](condis-miniport-driver-status-indications.md)の表示」を参照してください。

状態の表示が OID 要求に関連付けられている場合、基になるドライバーは、ステータス情報を含む[**NDIS\_status\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造の**Destinationhandle**メンバーと**RequestId**メンバーを設定できます。これにより、NDIS は特定のプロトコルバインドの状態を示すことができます。 OID 要求の詳細については、「 [Condis Protocol DRIVER OID requests](condis-protocol-driver-oid-requests.md)」を参照してください。

 

 





