---
title: BarcodeScannerErrorOccurred
description: BarcodeScannerErrorOccurred イベントは、スキャンのエラーなど、エラーがあるときに発生します。
ms.assetid: 38cfbd87-0526-49d1-8580-96f4e1adf7bb
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0060519110f16262ca643b8bb4c2805ab640a534
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358774"
---
# <a name="barcodescannererroroccurred"></a>BarcodeScannerErrorOccurred

このイベントは、スキャンのエラーなど、エラーがある場合に発生します。

このイベントのデータ バッファーは次のとおりです。

## <a name="syntax"></a>構文

```cpp
// Error occurred data should fill the ReadFile buffer in this order:
//    PosBarcodeScannerErrorOccurredEventData structure (length = sizeof(PosBarcodeScannerErrorOccurredEventData))
//    Error Message (length = MessageLength)
//    Scan Data (length = ScanDataLength)
//    Scan Data Label (length = ScanDataLabelLength)

typedef struct _PosBarcodeScannerErrorOccurredEventData
{
    PosEventDataHeader Header;
    LONG IsRetriable;
    UnifiedPosErrorSeverity Severity;
    UINT32 VendorErrorCode;
    UnifiedPosErrorReason Reason;
    UINT32 ExtendedReason;
    UINT32 MessageLength;
    PosBarcodeScannerDataReceivedEventData PartialData;
} PosBarcodeScannerErrorOccurredEventData;
```

次の表では、このイベントのデータ バッファーのメモリ レイアウトを示します。

| メモリの値                                      | 説明                                                                                                                                        |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000006                             | **EventType = PosEventType:。BarcodeScannerTriggerPressed**                                                                             |
| UINT32                                 | **DataLength** = sizeof (**PosBarcodeScannerErrorOccurredData**) + **MessageLength** + **ScanDataLength**  +  **ScanDataLabelLength**)     |
| BOOL                                   | **IsRetriable**                                                                                                                         |
| 32 ビット UnifiedPosErrorSeverity         | **重要度**                                                                                                                            |
| UINT32                                 | **VendorErrorCode**                                                                                                                     |
| 32 ビット UnifiedPosErrorReason           | **Reason**                                                                                                                              |
| UINT32                                 | **ExtendedReason**                                                                                                                      |
| UINT32                                 | **MessageLength**                                                                                                                       |
| PosBarcodeScannerDataReceivedEventData | **PartialData**                                                                                                                         |
| UINT32                                 | **EventType**指定されていません                                                                                                             |
| UINT32                                 | **DataLength** = sizeof(**PosBarcodeScannerDataRecievedEventData**) + **MessageLength** + **ScanDataLength** + **ScanDataLabelLength**) |
| UINT32                                 | **DataType**指定されていません                                                                                                              |
| UINT32                                 | **ScanDataLength**                                                                                                                      |
| UINT32                                 | **ScanDataLabelLength**                                                                                                                 |
| バイト \[\]                              | **MessageLength**メッセージのバイト数                                                                                                      |
| バイト \[\]                              | **ScanDataLength**ラベルのデータのバイト数                                                                                                  |
| バイト \[\]                              | **ScanDataLabelLength**スキャン データのバイト数                                                                                              |



## <a name="remarks"></a>注釈

スキャン エラーが発生するいくつかのスキャン データが取得された場合は、イベント データには、部分的なスキャン データが含まれています。

## <a name="requirements"></a>必要条件

**ヘッダー:** pointofservicedriverinterface.h
