---
title: GUID_TARGET_DEVICE_QUERY_REMOVE イベントを処理します。
description: GUID_TARGET_DEVICE_QUERY_REMOVE イベントを処理します。
ms.assetid: f3e867c5-f7b8-40d2-a6cc-c5cb82e0b59b
keywords:
- 通知 WDK PnP、ターゲット デバイスの変更
- ターゲット デバイスの変更通知 PnP WDK
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_QUERY_REMOVE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f72e34a78a1aae2ca450e8a4fc96d902afba6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559352"
---
# <a name="handling-a-guidtargetdevicequeryremove-event"></a>GUID の処理\_ターゲット\_デバイス\_クエリ\_削除イベント





PnP マネージャーに送信する前に、 [ **IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705) IRP のデバイス ドライバーをすべての通知コールバックを呼び出します登録ルーチン**EventCategoryTargetDeviceChange**デバイスにします。 PnP マネージャーを指定します、 *NotificationStructure*.**イベント**GUID の\_ターゲット\_デバイス\_クエリ\_を削除します。

そのような通知に応答して、コールバック ルーチンは、システムを停止することがなく、デバイスを削除できるかどうかを決定します。

コールバック ルーチンが状態を返す場合は、デバイスは削除されませんが、\_失敗しました。 この状態に応答して、PnP マネージャーは、クエリの削除処理を中止し、デバイスは削除されません。

デバイスが削除できる場合、コールバック ルーチンは終了 (可能な場合)、デバイスのすべてのハンドルを開くなど、デバイスの削除の準備を適切な操作を実行する必要があります。 ハンドルが、デバイスで開いたまま、PnP マネージャーは、デバイスを削除できませんし、PnP マネージャーは、クエリの削除処理を中止します。

GUID を正常に処理するときに\_ターゲット\_デバイス\_クエリ\_削除イベント、通知のコールバック ルーチンをする必要があります。

-   デバイスに開いているハンドルを閉じます。

-   ファイル オブジェクトの未解決の参照にドライバーがある場合は、ファイル オブジェクトを逆参照します。

-   登録されたまま将来**EventCategoryTargetDeviceChange**通知します。 これは、機能は、間もなくの削除操作をキャンセルする場合がありますので重要です。

デバイスを識別するハンドルを終了しても、PnP ターゲット デバイスの変更通知のドライバーの登録は取り消されません。 PnP マネージャーもで呼び出すことがドライバーの通知コールバック ルーチンですがこのような呼び出しで、ファイル オブジェクト、 *NotificationStructure*が無効です。

 

 




