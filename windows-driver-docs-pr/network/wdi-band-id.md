---
title: WDI_BAND_ID
description: このトピックでは、WDI ミニポート ドライバー WDI_BAND_ID データ型について説明します。
ms.assetid: 28E34D2C-94A5-4035-ACAA-60CECABF3A02
keywords:
- WDI_BAND_ID、WDK WDI_BAND_ID ネットワーク ドライバー
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e8782091eaf19c4217ff0d7e57b2eb4d85895e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391922"
---
# <a name="wdibandid"></a>WDI_BAND_ID

WDI_BAND_ID のデータ型は、バンドの ID を定義する UINT32 値

```c++
typedef UINT32 WDI_BAND_ID;
```

## <a name="remarks"></a>注釈

可能なバンド ID の値は次のとおりです。

| 値 |   | 説明 |
| --- | --- | --- |
| WDI_BAND_ID_ANY | 0 xffffffff | すべてのバンド |
| WDI_BAND_ID_2400 | 1 | 2.4 GHz |
| WDI_BAND_ID_5000 | 2 | 5 GHz |
| WDI_BAND_ID_60000 | 3 | 60 GHz |
| WDI_BAND_ID_900 | 4 | 900 MHz |
| WDI_BAND_ID_CUSTOM_START | 0x80000000 |IHV によって報告されたバンド ID を定義するために使用される範囲の開始を指定します。 |
| WDI_BAND_ID_CUSTOM_END | 0x81000000 | IHV によって報告されたバンド ID を定義するために使用される範囲の末尾を指定します。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |

