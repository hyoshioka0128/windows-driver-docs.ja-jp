---
title: BarcodeScannerImagePreviewReceived
description: BarcodeScannerImagePreviewReceived イベントは、デバイスがスキャンのビットマップ イメージを受信するときに発生します。
ms.assetid: ec05bffb-95e6-4d9c-b632-adee1cbd5bad
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: ad80780dcb8af4d32b58732833c2dd0af62cadf1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358762"
---
# <a name="barcodescannerimagepreviewreceived"></a>BarcodeScannerImagePreviewReceived

このイベントは、デバイスは、スキャンのビットマップ イメージを受け取ると発生します。

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

typedef struct _PosEventDataHeader PosBarcodeScannerImagePreviewEventData;
```

次の表では、このイベントのデータ バッファーのメモリ レイアウトを示します。

| メモリの値                                 | 説明                                                                                                 |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| 0x00000007                        | **EventType** = **PosEventType:。BarcodeScannerImagePreviewReceived**                            |
| 0x00000008 + イメージ データの長さ | sizeof (**PosBarcodeScannerImagePreviewEventData**) + (バイト単位) のデータのプレビュー イメージのサイズ |
| イメージ データ                        | イメージ データのプレビュー                                                                           |

## <a name="requirements"></a>必要条件

**ヘッダー:** pointofservicedriverinterface.h
