---
title: バッテリ通知の設定とキャンセル
description: バッテリ通知の設定とキャンセル
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
ms.openlocfilehash: 981e34f9f4f919806cb4ce501be235697f0fc237
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364733"
---
# <a name="setting-and-canceling-battery-notification"></a>バッテリ通知の設定とキャンセル


## <span id="ddk_setting_and_canceling_battery_notification_dg"></span><span id="DDK_SETTING_AND_CANCELING_BATTERY_NOTIFICATION_DG"></span>


Miniclass ドライバーを提供、 [ *BatteryMiniSetStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)ルーチンのクラス ドライバーは、特定の状況の通知を要求できるようにします。 ルーチンは、次のように宣言されます。

```cpp
typedef
NTSTATUS
(*BCLASS_SET_STATUS_NOTIFY)(
    IN PVOID Context,
    IN ULONG BatteryTag,
    IN PBATTERY_NOTIFY BatteryNotify
    );
```

*コンテキスト*パラメーター miniclass ドライバーによって割り当てられ、バッテリのクラス ドライバーに渡されるコンテキスト領域へのポインターは、\_ミニポート\_でデバイスの初期化情報構造体。 *BatteryTag*パラメーターは、値によって以前返さ[ *BatteryMiniQueryTag*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)します。

*BatteryNotify*パラメーターには、バッテリ電源の状態、およびバッテリの許容可能な容量の範囲を定義する ULONG 値のペアを示すフラグのセットが含まれています。 Miniclass ドライバーを呼び出す必要があります、バッテリ電源が指定した条件を満たしていませんまたは容量が指定された範囲より上または下、 [ **BatteryClassStatusNotify**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassstatusnotify)します。

*BatteryMiniSetStatusNotify*状態を返す必要があります\_いない\_条件またはこのバッテリの正しいと判断できないトリガー値をすべてサポートします。

クラスのドライバーの呼び出し、 [ *BatteryMiniDisableStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback) BatteryMiniSetStatusNotify によって以前に要求されたバッテリの状態変更の通知をキャンセルするルーチン。 このルーチンは、次のように宣言されます。

```cpp
typedef
NTSTATUS
(*BCLASS_DISABLE_STATUS_NOTIFY)(
    IN PVOID Context
    );
```

*コンテキスト*パラメーター miniclass ドライバーによって割り当てられ、バッテリーのクラス ドライバーに渡されるコンテキスト領域へのポインターは、\_ミニポート\_でデバイスの初期化情報構造体。

Miniclass ドライバーが両方のルーチンの機能の省略し、状態を返す\_いない\_サポートされています。 ただし、miniclass ドライバーを提供する、 *BatteryMiniSetStatusNotify*ルーチンは、対応するを指定する必要があります*BatteryMiniDisableStatusNotify*ルーチン、またはその逆です。

 

 




