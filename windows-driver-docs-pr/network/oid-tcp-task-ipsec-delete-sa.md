---
title: OID_TCP_TASK_IPSEC_DELETE_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_DELETE_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: 5f3b1f30-ab44-4d1c-96ff-b70ae6cfe324
keywords:
- OID_TCP_TASK_IPSEC_DELETE_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36503de3e132073f01fb0fab324c5e6bab12bd36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353719"
---
# <a name="oidtcptaskipsecdeletesa"></a>OID_TCP_TASK_IPSEC_DELETE_SA

OID_TCP_TASK_IPSEC_DELETE_SA OID は、ミニポート ドライバーが NIC からセキュリティ アソシエーション (SA) を削除することを要求するトランスポート プロトコルによって設定されます。 SA の情報として書式設定、 [OFFLOAD_IPSEC_DELETE_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_offload_ipsec_delete_sa)構造体。

この要求を受信するには、ミニポート ドライバーは、SA のすべてのシステム リソースが割り当てられている指定された SA NIC からと無料を削除する必要があります。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

