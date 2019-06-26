---
title: OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: f598199e-48f2-4ff5-846e-e88139408824
keywords:
- OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b6747edd3e931f359c105b71241569f72db5ced
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353722"
---
# <a name="oidtcptaskipsecdeleteudpespsa"></a>OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA

トランスポート プロトコルでは、ミニポート ドライバーが NIC パーサーのエントリの一覧から、UDP ESP セキュリティ アソシエーション (SA) と、場合によっては、パーサーのエントリを削除することを要求する OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA を設定します。 SA とパーサーのエントリの情報として書式設定、 [OFFLOAD_IPSEC_DELETE_UDPESP_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_offload_ipsec_delete_udpesp_sa)構造体。

場合、 **EncapTypeEntryOffldHandle**は**NULL**SA のすべてのシステム リソースが割り当てられている無料、ミニポートは、NIC から、指定された SA を削除する必要があります。 場合、 **EncapTypeEntryOffldHandle**以外**NULL**ミニポートではパーサーの指定したエントリを NIC のパーサーのエントリの一覧からも削除する必要があります。

トランスポート プロトコルがミニポートの SA やパーサー エントリの追加が完了する前に、SA やパーサー エントリを削除するミニポートを要求する可能性がありますに注意してください。 ミニポートに加算演算で削除操作がシリアル化したがって必要があります。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

