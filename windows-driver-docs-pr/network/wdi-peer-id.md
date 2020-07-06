---
title: WDI_PEER_ID
description: このトピックでは、WDI ミニポートドライバーの WDI_PEER_ID データ型について説明します。
ms.assetid: 2D8700BC-7FED-4343-AC3F-8C43B0BE40FF
keywords:
- WDI_PEER_ID、WDK WDI_PEER_ID ネットワークドライバー
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb25861a52f1d83ab9ce8f93ec7fafdd1e6f0118
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967894"
---
# <a name="wdi_peer_id"></a>WDI_PEER_ID

WDI_PEER_ID データ型は、ピア ID を定義する UINT16 値です。

```c++
typedef UINT16 WDI_PEER_ID;
```

## <a name="remarks"></a>注釈

任意のピア (ワイルドカード) を指定する場合は、WDI_PEER_ANY (0xFFFF) 値を使用できます。

## <a name="requirements"></a>要件

**サポートされている最低限のクライアント**: Windows 10

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Dot11wdi


