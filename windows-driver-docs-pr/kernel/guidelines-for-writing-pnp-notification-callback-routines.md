---
title: PnP 通知コールバック ルーチンの記述に関するガイドライン
description: PnP 通知コールバック ルーチンの記述に関するガイドライン
ms.assetid: 2153b4c2-f60f-4ac9-8eee-66c5f3a9f414
keywords:
- 通知 WDK PnP、コールバックルーチン
- コールバックルーチン WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c81087181efaf7b6df073b494c4f22dc8adbef51
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836676"
---
# <a name="guidelines-for-writing-pnp-notification-callback-routines"></a>PnP 通知コールバック ルーチンの記述に関するガイドライン





PnP マネージャーは、IRQL = パッシブ\_レベルで通知コールバックルーチンを呼び出します。

PnP サブシステムがスムーズに動作するように、PnP 通知コールバックルーチンは次のガイドラインに従う必要があります。

1.  通知のコールバックルーチンは、ブロックしないでください。

2.  通知コールバックルーチンは、PnP イベントを生成する同期ルーチンや、デバイスのインストールまたは削除を待機していることをブロックするルーチンの呼び出しを行うことはできません。

    通知コールバック中にこのようなルーチンを呼び出すと、システムのデッドロックが発生する可能性があります。

    たとえば、ドライバーが通知コールバックルーチンで[**IoReportTargetDeviceChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechange)を呼び出すことはできません。 代わりに[**IoReportTargetDeviceChangeAsynchronous**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechangeasynchronous)を呼び出してください。

3.  通知コールバックルーチンは、明示的に失敗しないすべてのイベントに対して成功を返す必要があります。

    ドライバーがイベントカテゴリの通知に登録すると、PnP マネージャーは、そのカテゴリのすべてのイベント (現在および将来) をドライバーに通知します。 ドライバーが処理していないイベントのエラー状態を返した場合、ドライバーは新しいクエリイベントの失敗を誤って発生させます。

    ドライバーがエラー状態を正しく返すのは、たとえば、ドライバーがクエリ通知に失敗して、イベントが提案されていることを拒否する場合です。

4.  通知コールバックルーチンは、ページコードである必要があります。

 

 




