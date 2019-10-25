---
title: OID_GEN_CO_MEDIA_CONNECT_STATUS
description: このトピックでは、OID_GEN_CO_MEDIA_CONNECT_STATUS オブジェクト識別子 (OID) について説明します。
ms.assetid: d49ebdfb-1c41-40dc-86bf-01db50a73607
keywords:
- OID_GEN_CO_MEDIA_CONNECT_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0eff8c9916a77cd8b5131a9608b56f3273689706
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844989"
---
# <a name="oid_gen_co_media_connect_status"></a>OID_GEN_CO_MEDIA_CONNECT_STATUS

OID_GEN_CO_MEDIA_CONNECT_STATUS OID は、次のいずれかのシステム定義値としてネットワーク上の NIC の接続状態を返すようにミニポートドライバーに要求します。

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

ネットワーク接続が失われたことがミニポートドライバーによって検知された場合は、NDIS_STATUS_MEDIA_DISCONNECT で[NdisMCoIndicateStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)を呼び出す必要があります。 接続が復元されると、NDIS_STATUS_MEDIA_CONNECT を使用して NdisMCoIndicateStatus を呼び出す必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

