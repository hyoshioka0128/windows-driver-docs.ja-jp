---
title: OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: f598199e-48f2-4ff5-846e-e88139408824
keywords:
- OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3b9f62f39645bb047c1f0cbb5359bc58ca5295d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843892"
---
# <a name="oid_tcp_task_ipsec_delete_udpesp_sa"></a>OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA

トランスポートプロトコルは、OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA を設定して、ミニポートドライバーが UDP ESP セキュリティアソシエーション (SA) を削除し、場合によっては、NIC パーサーエントリリストからパーサーエントリを削除するように要求します。 SA およびパーサーのエントリ情報は、 [OFFLOAD_IPSEC_DELETE_UDPESP_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_delete_udpesp_sa)構造体として書式設定されます。

**Encaptypeentryoffldhandle**が**NULL**の場合、ミニポートは、指定された sa を NIC から削除し、sa に割り当てられているすべてのシステムリソースを解放する必要があります。 **Encaptypeentryoffldhandle**が**NULL**以外の場合、ミニポートは、NIC のパーサーエントリリストから指定されたパーサーエントリも削除する必要があります。

トランスポートプロトコルでは、sa またはパーサーのエントリの追加が完了する前に、ミニポートで SA やパーサーのエントリを削除するようにミニポートを要求できることに注意してください。 したがって、ミニポートは、加算演算を使用して削除操作をシリアル化する必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

