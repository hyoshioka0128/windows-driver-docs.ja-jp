---
title: OID_TCP_TASK_IPSEC_DELETE_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_DELETE_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: 5f3b1f30-ab44-4d1c-96ff-b70ae6cfe324
keywords:
- OID_TCP_TASK_IPSEC_DELETE_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64faff7c14433def5995419cbd5c66dbea72a26e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918290"
---
# <a name="oid_tcp_task_ipsec_delete_sa"></a>OID_TCP_TASK_IPSEC_DELETE_SA

OID_TCP_TASK_IPSEC_DELETE_SA OID は、ミニポートドライバーが NIC からセキュリティアソシエーション (SA) を削除するように要求するために、トランスポートプロトコルによって設定されます。 SA 情報は[OFFLOAD_IPSEC_DELETE_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_delete_sa)構造として書式設定されます。

この要求を受信すると、ミニポートドライバーは、指定された SA を NIC から削除し、SA に割り当てられているすべてのシステムリソースを解放する必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

