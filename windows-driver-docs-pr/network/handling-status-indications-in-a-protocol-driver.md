---
title: プロトコル ドライバーの状態表示の処理
description: プロトコル ドライバーの状態表示の処理
ms.assetid: 1a021919-fd27-49b2-95a0-5ccb9029abd4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 091bb98ad7e3c6a3b83e92d9e349c18d87c43d21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381367"
---
# <a name="handling-status-indications-in-a-protocol-driver"></a>プロトコル ドライバーの状態表示の処理





プロトコル ドライバーを指定する必要があります、 [ **ProtocolStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex) NDIS が、基になるドライバーの状態を報告したときに呼び出す関数です。

NDIS 呼び出しプロトコル ドライバーの*ProtocolStatusEx*関数は、状態を示す値の関数を呼び出して、基になるドライバーから ([**NdisMIndicateStatus** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))または[ **NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus))。 詳細については、ミニポート ドライバーからの状態を示す、次を参照してください。[アダプター状態のインジケーター](miniport-adapter-status-indications.md)します。

詳細については、フィルター ドライバーからの状態を示す、次を参照してください。[フィルター モジュールの状態インジケーター](filter-module-status-indications.md)します。

状態の表示が OID 要求に関連付けられている場合は、基になるドライバーを設定できます、 **DestinationHandle**と**RequestId**その NDIS は、特定の状態の表示を提供できるように、メンバープロトコル バインディング。 OID 要求の詳細については、次を参照してください。[プロトコル ドライバー OID 要求](protocol-driver-oid-requests.md)します。

 

 





