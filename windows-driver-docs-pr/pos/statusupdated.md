---
title: StatusUpdated
description: 電源変更通知など、デバイス固有の StatusUpdated イベントはイベントを表します。
ms.assetid: e5d04e61-859a-49ee-bc54-58be4133b38a
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 57703edb67b4db5b2b3776cc550ede5c4a46db2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349302"
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
| UINT32     | **ステータス**します。 参照してください[BarcodeStatus](https://msdn.microsoft.com/library/windows/hardware/dn757472)します。   |
| UINT32     | **ExtendedStatus** |

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface.h
