---
title: StatusUpdated
description: 電源変更通知など、デバイス固有の StatusUpdated イベントはイベントを表します。
ms.assetid: e5d04e61-859a-49ee-bc54-58be4133b38a
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: c1cdd2759b564f54f27790095bc67a60e33997a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386499"
---
# <a name="statusupdated"></a>StatusUpdated

電源変更通知など、このデバイスに固有のイベントはイベントを表します。

このイベントのデータ バッファーは次のとおりです。

## <a name="syntax"></a>構文

```cpp
typedef struct _PosStatusUpdatedEventData
{
    PosEventDataHeader Header;
    UINT32 Status;
    UINT32 ExtendedStatus;
} PosStatusUpdatedEventData;
```

次の表では、このイベントのデータ バッファーのメモリ レイアウトを示します。

| メモリの値    | 説明 |
|-----------------| -------------------------------------------|
| 0x00000002 | **Header.EventType PosEventType::StatusUpdated を =**  |
| 0x00000010 | **Header.DataLength** = sizeof (**PosEventDataHeader**) + sizeof (**PosStatusUpdatedEventData.Status** + sizeof (**PosStatusUpdatedEventData.ExtendedStatus**) |
| UINT32     | **ステータス**します。 参照してください[BarcodeStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodestatus)します。   |
| UINT32     | **ExtendedStatus** |

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface.h
