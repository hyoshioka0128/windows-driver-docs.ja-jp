---
title: BarcodeScannerDataReceived
description: BarcodeScannerDataReceived イベントは、スキャンが成功イベントの後に発生します。
ms.assetid: 3dd7699a-5e2b-484b-bd83-c37ee7f0e851
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4d163fb0b0f679d71dc8f5692dd8bd8e8af62f83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552190"
---
# <a name="barcodescannerdatareceived"></a>BarcodeScannerDataReceived

このイベントは、スキャンが成功イベントの後に発生します。

スキャンされたデータは可変長とから成る、 [PosBarcodeScannerDataReceivedEventData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ns-pointofservicedriverinterface-_posbarcodescannerdatareceivedeventdata
)構造が続く**ScanDataLength**バイトの生のスキャン データが続く**ScanDataLabelLength**スキャナーのデータのみを残したまま、ヘッダーとフッターの情報が削除されたをデコードされたスキャン データのバイト数。 このイベントのデータ バッファーは次のとおりです。

## <a name="syntax"></a>構文

```cpp
typedef struct _PosBarcodeScannerDataReceivedEventData
{
    PosEventDataHeader Header;
    UINT32 DataType;
    UINT32 ScanDataLength;
    UINT32 ScanDataLabelLength;
} PosBarcodeScannerDataReceivedEventData;
```

次の表では、このイベントのデータ バッファーのメモリ レイアウトを示します。

| メモリの値                                            | 説明                                                                                                                          |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000005                                   | **Header.EventType PosEventType::BarcodeScannerDataReceived を =**                                                           |
| 0000020 + スキャン データの長さ + ラベル データの長さ | **Header.DataLength** = sizeof(**PosBarcodeScannerDataReceivedEventData**) + **ScanDataLength** + **ScanDataLabelLength** |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.DataType**                                                                       |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLength**                                                                 |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLabelLength**                                                            |
| バイト \[\]                                    | **ScanDataLength**生のスキャン データのバイト数                                                                                 |
| バイト \[\]                                    | **ScanDataLabelLength**スキャンのデコードされたデータのバイト数                                                                     |

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface.h
