---
title: StatusUpdated
description: 電源変更通知など、デバイス固有の StatusUpdated イベントはイベントを表します。
ms.assetid: e5d04e61-859a-49ee-bc54-58be4133b38a
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 57703edb67b4db5b2b3776cc550ede5c4a46db2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579635"
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

## <a name="requirements"></a>必要条件

**ヘッダー:** pointofservicedriverinterface.h
