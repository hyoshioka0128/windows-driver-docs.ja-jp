---
title: BarcodeScannerTriggerPressed
description: BarcodeScannerTriggerPressed イベントは、バーコード スキャナーのトリガが押されたときに発生します。
ms.assetid: 6f0a373f-bf3f-4201-9430-3474f84b9037
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f43c8a74e6aebfc6fe81e8cca92677889f740d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550691"
---
# <a name="barcodescannertriggerpressed"></a>BarcodeScannerTriggerPressed

このイベントは、バーコード スキャナーのトリガが押されたときに発生します。

このイベントのデータ バッファーは次のとおりです。

## <a name="syntax"></a>構文

```cpp
typedef struct _PosEventDataHeader
{
    // Event enumeration value
    PosEventType EventType;

    // Size of buffer required to read entire event (including header)
    UINT32 DataLength;
} PosEventDataHeader;
```

次の表では、このイベントのデータ バッファーのメモリ レイアウトを示します。

| メモリの値          | 説明                                                               |
|-----------------------|---------------------------------------------------------------------------|
| 0x00000003 | **EventType** = **PosEventType::BarcodeScannerTriggerPressed** |
| 0x00000008 | sizeof (**PosEventDataHeader**)                                 |

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface.h
