---
title: WDI_EXTENDED_TID
description: このトピックでは、WDI ミニポート ドライバー WDI_EXTENDED_TID データ型について説明します。
ms.assetid: C7ECB1BD-CB4A-4FD7-8222-9C9E25C15910
keywords:
- WDI_EXTENDED_TID、WDK WDI_EXTENDED_TID ネットワーク ドライバー
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6654123110081e749b939e1d147f8685a7a16b60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538128"
---
# <a name="wdiextendedtid"></a>WDI_EXTENDED_TID

WDI_EXTENDED_TID のデータ型は、トラフィックの識別子 (TID) を定義する UINT8 値です。

```c++
typedef UINT8 WDI_EXTENDED_TID;
```

## <a name="remarks"></a>注釈

使用できる値は次のとおりです。

| Value | 説明 |
| --- | --- |
| 0-15 | 802.11 Tid |
| 16 (WDI_EXT_TID_NON_QOS) | 非 QoS データ |
| 17-24 | IHV が挿入されたフレームで使用するために予約されています。 17 ~ 24 の間隔で拡張 TID を持つフレームは、同じ間隔 17 ~ 24 の小さい拡張 TID よりも優先順位の高いと見なされます。 |
| 25-30 | 未使用の値 |
| 31 (WDI_EXT_TID_UNKNOWN) | 不明または未指定 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |

