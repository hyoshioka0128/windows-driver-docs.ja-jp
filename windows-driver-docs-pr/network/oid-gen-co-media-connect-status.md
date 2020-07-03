---
title: OID_GEN_CO_MEDIA_CONNECT_STATUS
description: このトピックでは、OID_GEN_CO_MEDIA_CONNECT_STATUS オブジェクト識別子 (OID) について説明します。
ms.assetid: d49ebdfb-1c41-40dc-86bf-01db50a73607
keywords:
- OID_GEN_CO_MEDIA_CONNECT_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7966d9d618780c619145f316df34d45c9d9b034
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916901"
---
# <a name="oid_gen_co_media_connect_status"></a>OID_GEN_CO_MEDIA_CONNECT_STATUS

OID_GEN_CO_MEDIA_CONNECT_STATUS OID は、次のシステム定義の値の1つとしてネットワーク上の NIC の接続状態を返すようにミニポートドライバーに要求します。

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

ネットワーク接続が失われたことがミニポートドライバーによって検知されると、NDIS_STATUS_MEDIA_DISCONNECT で[NdisMCoIndicateStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)を呼び出す必要があります。 接続が復元されると、NDIS_STATUS_MEDIA_CONNECT で NdisMCoIndicateStatus を呼び出す必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

