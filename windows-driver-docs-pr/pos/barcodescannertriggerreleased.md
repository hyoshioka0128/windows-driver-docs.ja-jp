---
title: BarcodeScannerTriggerReleased
description: BarcodeScannerTriggerReleased イベントでは、バーコード スキャナーのトリガーがリリースされたときに発生します。
ms.assetid: 49b655c3-2652-4225-ba4c-5404da672b8e
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: f110d73a2436a64a43ec2f17c550dc3b5366a67d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358664"
---
# <a name="barcodescannertriggerreleased"></a>BarcodeScannerTriggerReleased

このイベントは、バーコード スキャナーのトリガーがリリースされたときに発生します。

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

| メモリの値          | 説明                                                                |
|-----------------------|----------------------------------------------------------------------------|
| 0x00000004 | **EventType** = **PosEventType::BarcodeScannerTriggerReleased** |
| 0x00000008 | sizeof (**PosEventDataHeader**)                                  |

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface.h
