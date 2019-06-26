---
title: バッテリ デバイス通知の提供
description: バッテリ デバイス通知の提供
ms.assetid: 7104c43b-84f1-496d-9552-608101f5b379
keywords:
- バッテリ通知 WDK
- バッテリ miniclass ドライバー WDK、通知
- 通知の WDK バッテリ
- バッテリ miniclass ドライバー WDK、状態レポート
- WDK のバッテリの状態情報
- バッテリの状態の監視
- バッテリ クラス ドライバー WDK、通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a97ace9e4f96bcf80f4dfec2dc5279e555fb8ca7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364716"
---
# <a name="supplying-battery-device-notification"></a>バッテリ デバイス通知の提供


## <span id="ddk_supplying_battery_device_notification_dg"></span><span id="DDK_SUPPLYING_BATTERY_DEVICE_NOTIFICATION_DG"></span>


Miniclass ドライバーは、サポート、バッテリの状態を監視し、変更が発生した重要なクラス ドライバーを通知する責任を負います。

加え、 [ *BatteryMiniQueryStatus* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback) 、日常的な miniclass ドライバーも提供、 [ *BatteryMiniSetStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)[ *BatteryMiniDisableStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback)ルーチン。 クラスのドライバーを使用して、 *BatteryMiniSetStatusNotify*と*BatteryMiniDisableStatusNotify*ルーチンを要求し、特定のバッテリの状態の通知をキャンセルします。 これらのルーチンは、クラスおよび miniclass のドライバーの状態ルーチンは次のセクションで説明したと対話します。 これらの 2 つの miniclass ルーチンの詳細については、次を参照してください。[設定とバッテリの通知をキャンセル](setting-and-canceling-battery-notification.md)します。

 

 




