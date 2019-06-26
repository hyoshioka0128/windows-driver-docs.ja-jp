---
title: バッテリ状態クエリへの応答
description: バッテリ状態クエリへの応答
ms.assetid: 756d7dd3-c4cc-4185-95cf-5a28ce86cacc
keywords:
- WDK バッテリの状態
- 低バッテリ WDK
- WDK のバッテリが放電しています
- 電源の状態の WDK バッテリ
- 失敗したバッテリ WDK
- バッテリ障害 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f161b24ffa361a0ca63cb6b3a320c03aadf09b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364740"
---
# <a name="responding-to-battery-status-queries"></a>バッテリ状態クエリへの応答


## <span id="ddk_responding_to_battery_status_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_STATUS_QUERIES_DG"></span>


バッテリ クラス ドライバー呼び出し miniclass ドライバーの[ *BatteryMiniQueryStatus* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)ルーチンを放電率、バッテリの電源の状態、容量、電圧を取得します。 このルーチンのプロトタイプを次に示します。

```cpp
typedef
NTSTATUS
(*BCLASS_QUERY_STATUS)(
    IN PVOID Context,
    IN ULONG BatteryTag,
    OUT PBATTERY_STATUS BatteryStatus
    );
```

*コンテキスト*パラメーターは miniclass ドライバーによって割り当てられ、クラス ドライバーに渡されるコンテキスト領域へのポインター、 [**バッテリ\_ミニポート\_情報**](https://docs.microsoft.com/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)デバイスの初期化で構造体。 *BatteryTag*パラメーターは BatteryMiniQueryTag によって以前返される値です。

バッファー内のバッテリで\_ステータス構造体 miniclass ドライバーを報告、バッテリの電圧、容量、および料金/放電評価できる程度に miniclass ドライバーが確認できます。 Miniclass ドライバーは、バッテリの電力状態を記述する次の定数の 1 つ以上にも報告します。

-   バッテリ\_充電中

-   バッテリ\_DISCHARGING

-   バッテリ\_POWER\_ON\_行

-   バッテリ\_重大

Miniclass ドライバーでは、放電中極度に少なくなったバッテリを報告する必要があります (バッテリ\_重大] および [バッテリ\_DISCHARGING) まで、条件が変動は一時的なものだけでないしが他のすべての不足を確認には状況を解決の手段です。 Miniclass ドライバーがこれを行う場合、または別のバッテリを AC 電源への切り替えが、このような解決策になどがあります。

Miniclass ドライバー報告すると、非常に少ない中、放電バッテリ電源マネージャーでは、バッテリ障害が近づいていること前提としています。 バッテリは、システムの電源を提供またはセカンダリ (充電) セルは、システムは、重要なバッテリの DC 電源ポリシーを実行します。 電源ポリシーの詳細では、ハードウェアの機能、アプリケーションの設定、およびユーザー設定によって、システムが異なります。 通常、システムがスリープ状態または電源オフ、コンピューターを入力しようとします。 詳細については、次を参照してください。[システム電源ポリシー](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-policy)します。

クラス ドライバーの[ **BatteryClassStatusNotify** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassstatusnotify)ルーチンと miniclass ドライバーの[ *BatteryMiniQueryStatus*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)、 [ *BatteryMiniSetStatusNotify*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)、および[ *BatteryMiniDisableStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback)ルーチンは、2 つのドライバーでシーケンスで使用されますタイムリーなステータス情報を提供します。 詳細については、次を参照してください。[相互作用のバッテリの状態と通知ルーチン](interaction-of-battery-status-and-notification-routines.md)します。

 

 




