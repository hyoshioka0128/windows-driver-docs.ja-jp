---
title: WDI_PEER_ID
description: このトピックでは、WDI ミニポート ドライバー WDI_PEER_ID データ型について説明します。
ms.assetid: 2D8700BC-7FED-4343-AC3F-8C43B0BE40FF
keywords:
- WDI_PEER_ID、WDK WDI_PEER_ID ネットワーク ドライバー
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12cebc10a70f34dff7d43055249e53d90d5a0b47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528644"
---
# <a name="wdipeerid"></a>WDI_PEER_ID

WDI_PEER_ID のデータ型は、ピア ID を定義する UINT16 値

```c++
typedef UINT16 WDI_PEER_ID;
```

## <a name="remarks"></a>注釈

すべてのピア (ワイルドカード) を指定する場合は、WDI_PEER_ANY (0 xffff) の値を使用できます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |

