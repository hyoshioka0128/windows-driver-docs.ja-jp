---
title: OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: f598199e-48f2-4ff5-846e-e88139408824
keywords:
- OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6db1e451d9bb86309e766caf6cc7e7585d890ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556436"
---
# <a name="oidtcptaskipsecdeleteudpespsa"></a>OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA

トランスポート プロトコルでは、ミニポート ドライバーが NIC パーサーのエントリの一覧から、UDP ESP セキュリティ アソシエーション (SA) と、場合によっては、パーサーのエントリを削除することを要求する OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA を設定します。 SA とパーサーのエントリの情報として書式設定、 [OFFLOAD_IPSEC_DELETE_UDPESP_SA](https://msdn.microsoft.com/library/windows/hardware/ff569059)構造体。

場合、 **EncapTypeEntryOffldHandle**は**NULL**SA のすべてのシステム リソースが割り当てられている無料、ミニポートは、NIC から、指定された SA を削除する必要があります。 場合、 **EncapTypeEntryOffldHandle**以外**NULL**ミニポートではパーサーの指定したエントリを NIC のパーサーのエントリの一覧からも削除する必要があります。

トランスポート プロトコルがミニポートの SA やパーサー エントリの追加が完了する前に、SA やパーサー エントリを削除するミニポートを要求する可能性がありますに注意してください。 ミニポートに加算演算で削除操作がシリアル化したがって必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

