---
title: WDI_PORT_ID
description: このトピックでは、WDI ミニポートドライバーの WDI_PORT_ID データ型について説明します。
ms.assetid: 16385F87-E3BE-4CCC-8E40-C4AAEA399964
keywords:
- WDI_PORT_ID、WDK WDI_PORT_ID ネットワークドライバー
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13b50d51671de17a4cc72b6a3fbc60a2c104aaba
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967921"
---
# <a name="wdi_port_id"></a>WDI_PORT_ID

WDI_PORT_ID データ型は、ポート ID を定義する UINT16 値です。

```c++
typedef UINT16 WDI_PORT_ID;
```

## <a name="remarks"></a>注釈

任意のポート (ワイルドカード) を指定する場合は、WDI_PORT_ANY (0xFFFF) 値を使用できます。

## <a name="requirements"></a>要件

**サポートされている最低限のクライアント**: Windows 10

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Dot11wdi


