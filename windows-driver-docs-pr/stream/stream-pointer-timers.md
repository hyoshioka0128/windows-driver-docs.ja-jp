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
ms.openlocfilehash: 10317e951a5f6e606d46194554eb2343aa674e55
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377802"
---
# <a name="stream-pointer-timers"></a>ストリーム ポインター タイマー





ストリーム ポインターでは、タイマーを設定するには、呼び出す[ **KsStreamPointerScheduleTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerscheduletimeout)します。 時間で指定したストリーム ポインターが削除されていないかどうかは*間隔*有効期限が切れる、AVStream ベンダーから提供されたタイマーのコールバック ルーチンを呼び出すとします。 指定*間隔*を 100 ナノ秒単位で。

タイムアウトをキャンセルする[ **KsStreamPointerCancelTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointercanceltimeout)します。

 

 




