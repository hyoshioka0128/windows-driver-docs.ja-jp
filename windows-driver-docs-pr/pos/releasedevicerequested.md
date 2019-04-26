---
title: ReleaseDeviceRequested
description: ReleaseDeviceRequested イベントでは、別のクライアントがデバイスを要求しようとしたときに発生します。
ms.assetid: 0fcb8905-1370-4260-9456-6c80e2186dfc
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc0d485ed5e1946954b309cb62941a7dc7984b2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349304"
---
# <a name="releasedevicerequested"></a>ReleaseDeviceRequested

このイベントは、別のクライアントがデバイスを要求しようとしたときに発生します。 このイベントのデータ バッファーは次のとおりです。

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

| メモリの値          | 説明                               |
|-----------------------|-------------------------------------------|
| 0x00000001 | **EventType PosEventType::ReleaseDeviceRequested を =** |
| 0x00000008 | sizeof (**PosEventDataHeader**)                       |

## <a name="remarks"></a>注釈

によってポイントのサービス クラスの拡張機能 (PosCx)、デバイス ドライバーの代わりに、このイベントが処理されます。 クライアントが別のクライアントを使用しているデバイスを要求しようとすると、PosCx を別のクライアントが、デバイスを要求しようとしていることを示すために、スキャナーのデバイスで要求を現在保持しているクライアントでは、このイベントを発生させます。 現在のクライアントがそのクレームを保持するかが必要です ([IOCTL\_ポイント\_の\_サービス\_保持\_デバイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_retain_device)) またはその要求をリリース ([IOCTL\_ポイント\_の\_サービス\_リリース\_デバイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_release_device)) のデバイスでこのイベントに応答します。 現在のクライアントがデバイスで、その要求を保持していない場合、 **ClaimedBarcodeScanner**オブジェクトが有効にできなくなります。

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface.h
