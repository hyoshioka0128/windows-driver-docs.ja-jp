---
title: ハードウェア プロファイルの変更イベントの処理
description: ハードウェア プロファイルの変更イベントの処理
ms.assetid: ddb0f740-9b31-4ede-be84-c1f6eb60fb1a
keywords:
- 通知 WDK PnP、ハードウェア プロファイルの変更
- ハードウェア プロファイルの変更通知 PnP WDK
- EventCategoryHardwareProfileChange 通知
- プロファイルの変更通知 PnP WDK
- マシンのハードウェア プロファイルの変更通知 PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c51c44adca1a78b837af2582230d031d3a803b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529725"
---
# <a name="handling-hardware-profile-change-events"></a>ハードウェア プロファイルの変更イベントの処理





ハードウェア プロファイルの変更中に特定の時刻に、PnP マネージャーは、通知に登録するコールバック ルーチン**EventCategoryHardwareProfileChange**:

-   PnP マネージャーが登録済みの通知コールバック ルーチンを呼び出すしを指定します、マシンのハードウェア プロファイルの変更が発生する前に、 *NotificationStructure*.**イベント**GUID の\_HWPROFILE\_クエリ\_変更します。

-   PnP マネージャーが登録済みの通知コールバック ルーチンを呼び出すしを指定します、マシンのハードウェア プロファイルの変更が完了した後、 *NotificationStructure*.**イベント**GUID の\_HWPROFILE\_変更\_完了します。

-   PnP マネージャーが登録済みの通知コールバック ルーチンを呼び出すしを指定します、マシンのハードウェア プロファイルの変更が取り消された場合、 *NotificationStructure*.**イベント**GUID の\_HWPROFILE\_変更\_キャンセルします。

GUID の\_HWPROFILE\_クエリ\_変更イベント、PnP マネージャーはユーザー モードにコールバック ルーチンを呼び出すし、カーネル モード コールバック ルーチンを呼び出します。 GUID への応答で\_HWPROFILE\_クエリ\_変更イベントでは、ドライバーの通知コールバック ルーチン通常だけステータスを返します\_成功します。

GUID の\_HWPROFILE\_変更\_完了イベント PnP マネージャーはカーネル モードのコールバック ルーチンを呼び出すし、ユーザー モードにコールバック ルーチンを呼び出します。 ドライバーのコールバック ルーチンはこのようなイベントに応答してで、そのハードウェア プロファイル固有の設定を更新する可能性があります。

GUID の\_HWPROFILE\_変更\_キャンセル イベント PnP マネージャーは、カーネル モードのコールバック ルーチンとし、ユーザー モードのルーチンを呼び出します。 このようなイベントに応答して、ドライバーのコールバック ルーチン通常だけステータスを返します\_成功します。 ドライバーが GUID への応答ですべての操作を実行するかどうか\_HWPROFILE\_クエリ\_変更イベントでは、ドライバーがこれらの操作がキャンセル イベントに応答を元に戻ります。

 

 




