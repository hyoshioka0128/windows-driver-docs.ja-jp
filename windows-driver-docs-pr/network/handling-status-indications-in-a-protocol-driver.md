---
title: プロトコル ドライバーの状態表示の処理
description: プロトコル ドライバーの状態表示の処理
ms.assetid: 1a021919-fd27-49b2-95a0-5ccb9029abd4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a07d7ac61015f5bfcb6d10f0169be859a7ef1a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842557"
---
# <a name="handling-status-indications-in-a-protocol-driver"></a>プロトコル ドライバーの状態表示の処理





プロトコルドライバーは、基になるドライバーがステータスを報告したときに NDIS が呼び出す[**Protocolstatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)関数を提供する必要があります。

NDIS は、基になるドライバーがステータス表示関数 ([**NdisMIndicateStatus**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))または[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)) を呼び出すと、プロトコルドライバーの*protocolstatusex*関数を呼び出します。 ミニポートドライバーの状態を示す詳細については、「[アダプターの状態](miniport-adapter-status-indications.md)の表示」を参照してください。

フィルタードライバーの状態を示す詳細については、「[フィルターモジュールの状態](filter-module-status-indications.md)の表示」を参照してください。

状態の表示が OID 要求に関連付けられている場合、基になるドライバーは**Destinationhandle**メンバーと**RequestId**メンバーを設定して、NDIS が特定のプロトコルバインドに状態を示すことができるようにすることができます。 OID 要求の詳細については、「 [Protocol DRIVER OID requests](protocol-driver-oid-requests.md)」を参照してください。

 

 





