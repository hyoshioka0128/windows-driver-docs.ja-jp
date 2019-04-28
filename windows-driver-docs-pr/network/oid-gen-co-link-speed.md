---
title: OID_GEN_CO_LINK_SPEED
description: このトピックでは、OID_GEN_CO_LINK_SPEED オブジェクト識別子 (OID) について説明します。
ms.assetid: a88ef1b9-b3f0-403e-8188-85aead46663f
keywords:
- OID_GEN_CO_LINK_SPEED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 604d057c478e3ffa66488e0d89abe760633cf019
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379220"
---
# <a name="oidgencolinkspeed"></a>OID_GEN_CO_LINK_SPEED

OID_GEN_CO_LINK_SPEED OID は、その現在の送信を返し、次のように定義されている NDIS_CO_LINK_SPEED 構造体として書式設定された速度を受信するミニポート ドライバーを要求します。

```c++
typedef struct _NDIS_CO_LINK_SPEED{
    ULONG   Outbound;
    ULONG   Inbound;
} NDIS_CO_LINK_SPEED, *PNDIS_CO_LINK_SPEED;
```

この構造体のメンバーには、次の情報が含まれます。

**送信**  
NIC の現在の送信速度 測定単位は 100,000 の値が 10 Mbps のハードウェア ビット レートを表すためにの 100 bps です。

**受信**  
NIC の現在の受信速度 測定単位は 100,000 の値が 10 Mbps のハードウェア ビット レートを表すためにの 100 bps です。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

