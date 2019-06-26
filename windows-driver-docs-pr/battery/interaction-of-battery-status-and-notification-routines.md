---
title: バッテリ状態と通知ルーチンの相互作用
description: バッテリ状態と通知ルーチンの相互作用
ms.assetid: 1f9a3785-4ea4-4b56-bc66-247dfe222377
keywords:
- バッテリ通知 WDK
- バッテリ miniclass ドライバー WDK、通知
- 通知の WDK バッテリ
- バッテリ クラス ドライバー WDK、通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d12ac75e3f1de5695eae4bd79b43866f2c7e001
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354059"
---
# <a name="interaction-of-battery-status-and-notification-routines"></a>バッテリ状態と通知ルーチンの相互作用


## <span id="ddk_interaction_of_battery_status_and_notification_routines_dg"></span><span id="DDK_INTERACTION_OF_BATTERY_STATUS_AND_NOTIFICATION_ROUTINES_DG"></span>


クラスのドライバーが要求し、バッテリの状態 - 受信、miniclass ドライバーは、いくつかの方法で--バッテリの状態を提供できます。

Miniclass ドライバーを提供する場合、 [ *BatteryMiniSetStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)ルーチンをクラス ドライバーは、バッテリの容量を超えるまたは指定された範囲を下回るときや、通知に登録することができます、電源の状態の変更。 登録済みの条件のいずれかが発生したときに、miniclass ドライバーを呼び出す[ **BatteryClassStatusNotify**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassstatusnotify)します。

なお**BatteryClassStatusNotify**状態情報を指定しないのは、唯一のパラメーターは、通知をトリガーするバッテリのコンテキスト。 単に、バッテリの状態が変更されたクラス ドライバーを通知します。 さらに、クラス ドライバーを呼び出す[ *BatteryMiniQueryStatus* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)の詳細が必要な場合。

Miniclass ドライバーがサポートされていない場合*BatteryMiniSetStatusNotify*、クラス ドライバーを呼び出すことによってステータスのポーリング、 *BatteryMiniQueryStatus*正規表現が低頻度の間隔で定期的な。

任意の通知の依存要求、miniclass ドライバーを呼び出す必要があります**BatteryClassStatusNotify**次のいずれかが発生します。

-   バッテリが、オンラインまたはオフラインです。

-   バッテリの容量が非常に低になります。

-   バッテリの変更の電源の状態: 充電が開始、放電してを開始、充電中、停止または放電して停止します。

既に説明したようにする必要があります、miniclass ドライバーを問題を解決するために試行するよう、放電中極度に少なくなったバッテリを報告する前に[バッテリの状態のクエリに応答して](responding-to-battery-status-queries.md)します。

 

 




