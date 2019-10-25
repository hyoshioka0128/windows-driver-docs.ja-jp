---
title: BarcodeScannerDataReceived
description: Barの実行が成功したイベントが発生すると、barのイベントが発生します。
ms.assetid: 3dd7699a-5e2b-484b-bd83-c37ee7f0e851
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: c6c1cff03e585c428ed8aac80aa0c038fcdce02b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843577"
---
# <a name="barcodescannerdatareceived"></a>BarcodeScannerDataReceived

このイベントは、スキャンイベントが成功した後に発生します。

スキャンされたデータは可変長で、 [PosBarcodeScannerDataReceivedEventData](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ns-pointofservicedriverinterface-_posbarcodescannerdatareceivedeventdata)構造体の後**に生**のスキャンデータの ScanDataLabelLength バイトが続き、デコードされたスキャンデータのバイトが含まれます。ヘッダーとフッターの情報は削除され、スキャナーデータだけが残ります。 このイベントのデータバッファーは次のとおりです。

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

次の表は、このイベントのデータバッファーのメモリレイアウトを示しています。

| メモリ値                                            | 説明                                                                                                                          |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000005                                   | **Header. EventType = PosEventType:: Barのイベント受信**                                                           |
| 0000020 + Scan data length + label data length | **Header. DataLength** = Sizeof (**PosBarcodeScannerDataReceivedEventData**) + **scandatalength** + **ScanDataLabelLength** |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData**                                                                       |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData**                                                                 |
| UINT32                                       | **PosBarcodeScannerDataReceivedEventData.ScanDataLabelLength**                                                            |
| バイト \[\]                                    | 生のスキャンデータの**Scandatalength**バイト数                                                                                 |
| バイト \[\]                                    | デコードされたスキャンデータの**ScanDataLabelLength**バイト数                                                                     |

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface
