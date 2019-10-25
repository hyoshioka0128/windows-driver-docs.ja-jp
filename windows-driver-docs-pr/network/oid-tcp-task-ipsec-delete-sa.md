---
title: OID_TCP_TASK_IPSEC_DELETE_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_DELETE_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: 5f3b1f30-ab44-4d1c-96ff-b70ae6cfe324
keywords:
- OID_TCP_TASK_IPSEC_DELETE_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: d38e25ffc8b622662829bb98eae9a36a48359b21
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843893"
---
# <a name="oid_tcp_task_ipsec_delete_sa"></a>OID_TCP_TASK_IPSEC_DELETE_SA

OID_TCP_TASK_IPSEC_DELETE_SA OID は、ミニポートドライバーが NIC からセキュリティアソシエーション (SA) を削除するように要求するために、トランスポートプロトコルによって設定されます。 SA 情報は、 [OFFLOAD_IPSEC_DELETE_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_delete_sa)構造体として書式設定されます。

この要求を受信すると、ミニポートドライバーは、指定された SA を NIC から削除し、SA に割り当てられているすべてのシステムリソースを解放する必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

