---
title: WDI_PORT_ID
description: このトピックでは、WDI ミニポート ドライバー WDI_PORT_ID データ型について説明します。
ms.assetid: 16385F87-E3BE-4CCC-8E40-C4AAEA399964
keywords:
- WDI_PORT_ID、WDK WDI_PORT_ID ネットワーク ドライバー
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b5f33728e7ff3421ecfd2c36db9ee8d8378f80e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560685"
---
# <a name="wdiportid"></a>WDI_PORT_ID

WDI_PORT_ID のデータ型は、ポートの ID を定義する UINT16 値

```c++
typedef UINT16 WDI_PORT_ID;
```

## <a name="remarks"></a>注釈

(ワイルドカード) の任意のポートを指定する場合は、WDI_PORT_ANY (0 xffff) の値を使用できます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |

