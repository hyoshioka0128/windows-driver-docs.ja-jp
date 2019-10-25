---
title: StatusUpdated
description: デバイス固有の StatusUpdated イベントは、電源変更通知などのイベントを表します。
ms.assetid: e5d04e61-859a-49ee-bc54-58be4133b38a
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2107c3b30ec46a6ca3a07cbb63f81deeba0464a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841642"
---
# <a name="statusupdated"></a>StatusUpdated

このデバイス固有のイベントは、電源変更通知などのイベントを表します。

このイベントのデータバッファーは次のとおりです。

## <a name="syntax"></a>構文

```cpp
typedef struct _PosStatusUpdatedEventData
{
    PosEventDataHeader Header;
    UINT32 Status;
    UINT32 ExtendedStatus;
} PosStatusUpdatedEventData;
```

次の表は、このイベントのデータバッファーのメモリレイアウトを示しています。

| メモリ値    | 説明 |
|-----------------| -------------------------------------------|
| 0x00000002 | **Header. EventType = PosEventType:: StatusUpdated**  |
| 0x00000010 | **Header. DataLength** = Sizeof (**PosEventDataHeader**) + sizeof (**PosStatusUpdatedEventData** + sizeof (**PosStatusUpdatedEventData status**) |
| UINT32     | **状態**。 「 [Barcodestatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodestatus)」を参照してください。   |
| UINT32     | **ExtendedStatus** |

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface
