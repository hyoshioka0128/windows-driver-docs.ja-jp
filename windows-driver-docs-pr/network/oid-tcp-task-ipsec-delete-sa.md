---
title: OID_TCP_TASK_IPSEC_DELETE_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_DELETE_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: 5f3b1f30-ab44-4d1c-96ff-b70ae6cfe324
keywords:
- OID_TCP_TASK_IPSEC_DELETE_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f6c61150fd7976f2fb6b9b0c590bf524afadf94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531682"
---
# <a name="oidtcptaskipsecdeletesa"></a>OID_TCP_TASK_IPSEC_DELETE_SA

OID_TCP_TASK_IPSEC_DELETE_SA OID は、ミニポート ドライバーが NIC からセキュリティ アソシエーション (SA) を削除することを要求するトランスポート プロトコルによって設定されます。 SA の情報として書式設定、 [OFFLOAD_IPSEC_DELETE_SA](https://msdn.microsoft.com/library/windows/hardware/ff569058)構造体。

この要求を受信するには、ミニポート ドライバーは、SA のすべてのシステム リソースが割り当てられている指定された SA NIC からと無料を削除する必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

