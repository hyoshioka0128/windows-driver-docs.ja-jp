---
title: PnP 通知コールバック ルーチンの記述に関するガイドライン
description: PnP 通知コールバック ルーチンの記述に関するガイドライン
ms.assetid: 2153b4c2-f60f-4ac9-8eee-66c5f3a9f414
keywords:
- 通知 WDK PnP、コールバック ルーチン
- コールバック ルーチン PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c08c88bf63918451585353762e01dbc5a84dd1b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359882"
---
# <a name="guidelines-for-writing-pnp-notification-callback-routines"></a>PnP 通知コールバック ルーチンの記述に関するガイドライン





PnP マネージャーは IRQL で通知コールバック ルーチンを呼び出して = パッシブ\_レベル。

PnP サブシステムの円滑に運用のために、PnP 通知コールバック ルーチンは次のガイドラインに従う必要があります。

1.  通知のコールバック ルーチンをブロックする必要があります。

2.  通知のコールバック ルーチンを呼び出すと、または、PnP イベントを生成する同期のルーチンまたはデバイスのインストールまたは削除されるまで待機する任意のルーチンへの呼び出しが発生する必要がありますできません。

    通知のコールバック中にこのようなルーチンを呼び出すと、システム デッドロックが発生することができます。

    ドライバーを呼び出してはならないなど[ **IoReportTargetDeviceChange** ](https://msdn.microsoft.com/library/windows/hardware/ff549625)で通知のコールバック ルーチン。 呼び出す[ **IoReportTargetDeviceChangeAsynchronous** ](https://msdn.microsoft.com/library/windows/hardware/ff549634)代わりにします。

3.  通知のコールバック ルーチンは、明示的に失敗しないすべてのイベントの成功を返す必要があります。

    イベント カテゴリの通知の登録は、ドライバー、PnP マネージャーには、そのカテゴリの現在および将来のすべてのイベントのドライバーに通知します。 ドライバーは、イベントのエラー状態を返す場合処理されない場合、新しいクエリ イベントの失敗を誤ってドライバー リスクです。

    など、ドライバーが指定されているイベントを拒否するクエリ通知が失敗したときに、ドライバーは正しくエラー状態を返します。

4.  通知のコールバック ルーチンは、ページのコードで必要があります。

 

 




