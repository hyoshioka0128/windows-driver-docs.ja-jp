---
title: ストリーム ポインター タイマー
description: ストリーム ポインター タイマー
ms.assetid: 98413fc6-2b62-4c52-9ac4-bd2a3a60db60
keywords:
- WDK AVStream、タイマーのポインターをストリーム配信します。
- WDK AVStream のタイマー
- WDK AVStream のタイムアウト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 260dfebf9324a34365ba757d25daeb42d6f47b4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373571"
---
# <a name="stream-pointer-timers"></a>ストリーム ポインター タイマー





ストリーム ポインターでは、タイマーを設定するには、呼び出す[ **KsStreamPointerScheduleTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff567135)します。 時間で指定したストリーム ポインターが削除されていないかどうかは*間隔*有効期限が切れる、AVStream ベンダーから提供されたタイマーのコールバック ルーチンを呼び出すとします。 指定*間隔*を 100 ナノ秒単位で。

タイムアウトをキャンセルする[ **KsStreamPointerCancelTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff567128)します。

 

 




