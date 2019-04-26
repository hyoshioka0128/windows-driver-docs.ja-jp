---
title: BarcodeScannerTriggerPressed
description: BarcodeScannerTriggerPressed イベントは、バーコード スキャナーのトリガが押されたときに発生します。
ms.assetid: 6f0a373f-bf3f-4201-9430-3474f84b9037
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f43c8a74e6aebfc6fe81e8cca92677889f740d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358665"
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
