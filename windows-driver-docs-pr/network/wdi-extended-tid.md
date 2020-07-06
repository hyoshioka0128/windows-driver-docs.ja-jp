---
title: WDI_EXTENDED_TID
description: このトピックでは、WDI ミニポートドライバーの WDI_EXTENDED_TID データ型について説明します。
ms.assetid: C7ECB1BD-CB4A-4FD7-8222-9C9E25C15910
keywords:
- WDI_EXTENDED_TID、WDK WDI_EXTENDED_TID ネットワークドライバー
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a58bca838aeb851ba899d933c8fa8899910bed9
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967889"
---
# <a name="wdi_extended_tid"></a>WDI_EXTENDED_TID

WDI_EXTENDED_TID データ型は、トラフィック識別子 (TID) を定義する UINT8 値です。

```c++
typedef UINT8 WDI_EXTENDED_TID;
```

## <a name="remarks"></a>注釈

使用できる値は次のとおりです。

| 値 | [説明] |
| --- | --- |
| 0-15 | 802.11 TIDs |
| 16 (WDI_EXT_TID_NON_QOS) | 非 QoS データ |
| 17-24 | IHV が挿入したフレームで使用するために予約されています。 間隔17-24 の拡張 TID を持つフレームは、同じ間隔17-24 の拡張 TID が小さい方より高い優先順位と見なされます。 |
| 25-30 | 未使用の値 |
| 31 (WDI_EXT_TID_UNKNOWN) | 不明/未指定 |

## <a name="requirements"></a>要件

**サポートされている最低限のクライアント**: Windows 10

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Dot11wdi


