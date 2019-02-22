---
title: 設定して、バッテリの通知をキャンセル
description: 設定して、バッテリの通知をキャンセル
ms.assetid: bd0920f0-9f3f-47f7-b1a7-29ec233e93ff
keywords:
- バッテリ通知 WDK
- バッテリ miniclass ドライバー WDK、通知
- 通知の WDK バッテリ
- バッテリ クラス ドライバー WDK、通知
- バッテリの通知をキャンセル
- バッテリの通知を停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e00cadc51bb62c4a3456c4d5a51b5f0d2121494f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553145"
---
# <a name="setting-and-canceling-battery-notification"></a>設定して、バッテリの通知をキャンセル


## <span id="ddk_setting_and_canceling_battery_notification_dg"></span><span id="DDK_SETTING_AND_CANCELING_BATTERY_NOTIFICATION_DG"></span>


Miniclass ドライバーを提供、 [ *BatteryMiniSetStatusNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff536277)ルーチンのクラス ドライバーは、特定の状況の通知を要求できるようにします。 ルーチンは、次のように宣言されます。

```cpp
typedef
NTSTATUS
(*BCLASS_SET_STATUS_NOTIFY)(
    IN PVOID Context,
    IN ULONG BatteryTag,
    IN PBATTERY_NOTIFY BatteryNotify
    );
```

*コンテキスト*パラメーター miniclass ドライバーによって割り当てられ、バッテリのクラス ドライバーに渡されるコンテキスト領域へのポインターは、\_ミニポート\_でデバイスの初期化情報構造体。 *BatteryTag*パラメーターは、値によって以前返さ[ *BatteryMiniQueryTag*](https://msdn.microsoft.com/library/windows/hardware/ff536275)します。

*BatteryNotify*パラメーターには、バッテリ電源の状態、およびバッテリの許容可能な容量の範囲を定義する ULONG 値のペアを示すフラグのセットが含まれています。 Miniclass ドライバーを呼び出す必要があります、バッテリ電源が指定した条件を満たしていませんまたは容量が指定された範囲より上または下、 [ **BatteryClassStatusNotify**](https://msdn.microsoft.com/library/windows/hardware/ff536269)します。

*BatteryMiniSetStatusNotify*状態を返す必要があります\_いない\_条件またはこのバッテリの正しいと判断できないトリガー値をすべてサポートします。

クラスのドライバーの呼び出し、 [ *BatteryMiniDisableStatusNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff536272) BatteryMiniSetStatusNotify によって以前に要求されたバッテリの状態変更の通知をキャンセルするルーチン。 このルーチンは、次のように宣言されます。

```cpp
typedef
NTSTATUS
(*BCLASS_DISABLE_STATUS_NOTIFY)(
    IN PVOID Context
    );
```

*コンテキスト*パラメーター miniclass ドライバーによって割り当てられ、バッテリーのクラス ドライバーに渡されるコンテキスト領域へのポインターは、\_ミニポート\_でデバイスの初期化情報構造体。

Miniclass ドライバーが両方のルーチンの機能の省略し、状態を返す\_いない\_サポートされています。 ただし、miniclass ドライバーを提供する、 *BatteryMiniSetStatusNotify*ルーチンは、対応するを指定する必要があります*BatteryMiniDisableStatusNotify*ルーチン、またはその逆です。

 

 




