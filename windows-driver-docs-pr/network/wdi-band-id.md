---
title: WDI_BAND_ID
description: このトピックでは、WDI ミニポートドライバーの WDI_BAND_ID データ型について説明します。
ms.assetid: 28E34D2C-94A5-4035-ACAA-60CECABF3A02
keywords:
- WDI_BAND_ID、WDK WDI_BAND_ID ネットワークドライバー
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8c5744120f400a1e73d9d8ce4f86a1c29c8724b
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968241"
---
# <a name="wdi_band_id"></a>WDI_BAND_ID

WDI_BAND_ID データ型は、バンド ID を定義する UINT32 値です。

```c++
typedef UINT32 WDI_BAND_ID;
```

## <a name="remarks"></a>注釈

使用可能なバンド ID の値は次のとおりです。

| 値 |   | [説明] |
| --- | --- | --- |
| WDI_BAND_ID_ANY | ~ | すべてのバンド |
| WDI_BAND_ID_2400 | 1 | 2.4 GHz |
| WDI_BAND_ID_5000 | 2 | 5 GHz |
| WDI_BAND_ID_60000 | 3 | 60 GHz |
| WDI_BAND_ID_900 | 4 | 900 MHz |
| WDI_BAND_ID_CUSTOM_START | 0x80000000 |IHV によって報告されたバンド ID を定義するために使用される範囲の開始を指定します。 |
| WDI_BAND_ID_CUSTOM_END | 0x81000000 | IHV によって報告されたバンド ID を定義するために使用される範囲の末尾を指定します。 |

## <a name="requirements"></a>要件

**サポートされている最低限のクライアント**: Windows 10

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Wditypes


