---
title: EFI_BATTERY_CHARGING_COMPLETION_TOKEN
description: EFI_BATTERY_CHARGING_COMPLETION_TOKEN
ms.assetid: 1151643e-8b22-4034-b043-ac4d44c01082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e9e931cccf04e2d90410c85c249815302c9eb29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558873"
---
# <a name="efibatterychargingcompletiontoken"></a>EFI\_バッテリ\_充電中\_完了\_トークン


この構造体の定義に使用される完了トークン[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)します。

## <a name="syntax"></a>構文


```cpp
typedef struct _EFI_BATTERY_CHARGING_COMPLETION_TOKEN {
  EFI_EVENT Event;
  EFI_BATTERY_CHARGING_STATUS Status;
} EFI_BATTERY_CHARGING_COMPLETION_TOKEN;
```

## <a name="members"></a>Members


<a href="" id="event"></a>**イベント**  
料金の要求が完了した後に通知するイベントです。 イベントの種類は EVT である必要があります\_通知\_信号。

<a href="" id="status"></a>**状態**  
完了した操作の結果。

## <a name="remarks"></a>注釈


EFI\_バッテリ\_充電中\_完了\_でトークンが返されます、 *CompletionToken*パラメーターの[EFI\_バッテリ\_充電\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)します。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

## <a name="related-topics"></a>関連トピック

[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)  

[EFI\_バッテリ\_充電中\_状態](efi-battery-charging-status.md)  
