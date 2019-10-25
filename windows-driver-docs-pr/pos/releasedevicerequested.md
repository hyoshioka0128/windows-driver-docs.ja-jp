---
title: ReleaseDeviceRequested
description: ReleaseDeviceRequested イベントは、別のクライアントがデバイスを要求しようとしたときに発生します。
ms.assetid: 0fcb8905-1370-4260-9456-6c80e2186dfc
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: c10303ea75da385166f55706dc75a139a18623b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845263"
---
# <a name="releasedevicerequested"></a>ReleaseDeviceRequested

このイベントは、別のクライアントがデバイスを要求しようとしたときに発生します。 このイベントのデータバッファーは次のとおりです。

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

次の表は、このイベントのデータバッファーのメモリレイアウトを示しています。

| メモリ値          | 説明                               |
|-----------------------|-------------------------------------------|
| 0x00000001 | **EventType = PosEventType:: ReleaseDeviceRequested** |
| 0x00000008 | sizeof (**PosEventDataHeader**)                       |

## <a name="remarks"></a>注釈

このイベントは、デバイスドライバーに代わってサービスクラス拡張 (PosCx) によって処理されます。 別のクライアントが使用しているデバイスをクライアントが要求しようとすると、そのクライアントでは、現在、別のクライアントがデバイスを要求しようとしていることを示すために、このイベントがスキャナーデバイスに要求されています。 現在のクライアントは、その要求 ([ioctl\_ポイント\_\_サービスの\_デバイスの保持\_](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_retain_device)) を保持するか、\_[サービス\_リリースの ioctl\_ポイント\_を解放する必要があり\_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_release_device)) このイベントに応答します。 現在のクライアントがデバイス上の要求を保持していない場合、その**ClaimedBarcodeScanner**オブジェクトは無効になります。

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface
