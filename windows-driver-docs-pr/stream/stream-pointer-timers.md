---
title: Stream ポインター タイマー
description: Stream ポインター タイマー
ms.assetid: 98413fc6-2b62-4c52-9ac4-bd2a3a60db60
keywords:
- WDK AVStream、タイマーのポインターをストリーム配信します。
- WDK AVStream のタイマー
- WDK AVStream のタイムアウト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 260dfebf9324a34365ba757d25daeb42d6f47b4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538534"
---
# <a name="stream-pointer-timers"></a>Stream ポインター タイマー





ストリーム ポインターでは、タイマーを設定するには、呼び出す[ **KsStreamPointerScheduleTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff567135)します。 時間で指定したストリーム ポインターが削除されていないかどうかは*間隔*有効期限が切れる、AVStream ベンダーから提供されたタイマーのコールバック ルーチンを呼び出すとします。 指定*間隔*を 100 ナノ秒単位で。

タイムアウトをキャンセルする[ **KsStreamPointerCancelTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff567128)します。

 

 




