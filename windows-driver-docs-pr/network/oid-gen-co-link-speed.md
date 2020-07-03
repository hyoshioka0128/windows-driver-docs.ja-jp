---
title: OID_GEN_CO_LINK_SPEED
description: このトピックでは、OID_GEN_CO_LINK_SPEED オブジェクト識別子 (OID) について説明します。
ms.assetid: a88ef1b9-b3f0-403e-8188-85aead46663f
keywords:
- OID_GEN_CO_LINK_SPEED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: edad21b56d642a77d337cbc6d6282a7a46c67c3e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917960"
---
# <a name="oid_gen_co_link_speed"></a>OID_GEN_CO_LINK_SPEED

OID_GEN_CO_LINK_SPEED OID は、次のように定義されている NDIS_CO_LINK_SPEED 構造として書式設定された現在の送信速度と受信速度をミニポートドライバーに返すように要求します。

```c++
typedef struct _NDIS_CO_LINK_SPEED{
    ULONG   Outbound;
    ULONG   Inbound;
} NDIS_CO_LINK_SPEED, *PNDIS_CO_LINK_SPEED;
```

この構造体のメンバーには、次の情報が含まれています。

**Outbound**  
NIC の現在の送信速度。 測定単位は100bps であるため、10万の値は、ハードウェアのビットレートとして 10 Mbps を表します。

**受信**  
NIC の現在の受信速度。 測定単位は100bps であるため、10万の値は、ハードウェアのビットレートとして 10 Mbps を表します。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

