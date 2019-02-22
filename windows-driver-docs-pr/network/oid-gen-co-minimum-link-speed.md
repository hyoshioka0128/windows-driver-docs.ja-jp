---
title: OID_GEN_CO_MINIMUM_LINK_SPEED
description: このトピックでは、OID_GEN_CO_MINIMUM_LINK_SPEED オブジェクト識別子 (OID) について説明します。
ms.assetid: 2ed27ec7-b773-4751-96d3-42d839f35a97
keywords:
- OID_GEN_CO_MINIMUM_LINK_SPEED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8df5f23d62dd9be3be1a8768581aa0aefdd8ac5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560333"
---
# <a name="oidgencominimumlinkspeed"></a>OID_GEN_CO_MINIMUM_LINK_SPEED

OID_GEN_CO_MINIMUM_LINK_SPEED OID が返す最小の送信と受信速度が次のように定義されている NDIS_CO_LINK_SPEED 構造体として書式設定するには、ミニポート ドライバーを要求します。

```c++
typedef struct _NDIS_CO_LINK_SPEED{
    ULONG   Outbound;
    ULONG   Inbound;
} NDIS_CO_LINK_SPEED, *PNDIS_CO_LINK_SPEED;
```

この構造体のメンバーには、次の情報が含まれます。

**送信**  
NIC の最小の送信速度 測定単位は 100,000 の値が 10 Mbps のハードウェア ビット レートを表すためにの 100 bps です。

**受信**  
NIC の最小の受信速度 測定単位は 100,000 の値が 10 Mbps のハードウェア ビット レートを表すためにの 100 bps です。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

