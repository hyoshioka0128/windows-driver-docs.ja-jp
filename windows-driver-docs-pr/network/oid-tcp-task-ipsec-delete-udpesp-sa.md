---
title: OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: f598199e-48f2-4ff5-846e-e88139408824
keywords:
- OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bf20a103e053ddd7ea0d068b955f20c358b1d25
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916436"
---
# <a name="oid_tcp_task_ipsec_delete_udpesp_sa"></a>OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA

トランスポートプロトコルは OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA を設定して、ミニポートドライバーが UDP ESP セキュリティアソシエーション (SA) を削除し、場合によっては、NIC パーサーエントリリストからパーサーエントリを削除するように要求します。 SA およびパーサーのエントリ情報は、 [OFFLOAD_IPSEC_DELETE_UDPESP_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_delete_udpesp_sa)構造として書式設定されます。

**Encaptypeentryoffldhandle**が**NULL**の場合、ミニポートは、指定された sa を NIC から削除し、sa に割り当てられているすべてのシステムリソースを解放する必要があります。 **Encaptypeentryoffldhandle**が**NULL**以外の場合、ミニポートは、NIC のパーサーエントリリストから指定されたパーサーエントリも削除する必要があります。

トランスポートプロトコルでは、sa またはパーサーのエントリの追加が完了する前に、ミニポートで SA やパーサーのエントリを削除するようにミニポートを要求できることに注意してください。 したがって、ミニポートは、加算演算を使用して削除操作をシリアル化する必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

