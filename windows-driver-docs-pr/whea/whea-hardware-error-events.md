---
title: WHEA ハードウェア エラー イベント
description: WHEA ハードウェア エラー イベント
ms.assetid: c9f88e3b-3915-4a77-8d60-f0f3da514abc
keywords:
- イベント WDK WHEA、イベントについて
- Windows ハードウェアエラーアーキテクチャ WDK、イベント
- WHEA WDK、イベント
- ハードウェアエラー WDK WHEA、イベント
- エラー WDK WHEA、イベント
- ハードウェアエラーイベントの WDK WHEA
- イベント WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e6e0375cd73d5f985d66e53a66003d1a81abc09
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844712"
---
# <a name="whea-hardware-error-events"></a>WHEA ハードウェア エラー イベント


ハードウェアエラーが発生するたびに、Windows ハードウェアエラーアーキテクチャ (WHEA) によって Windows イベントトレーシング (ETW) イベントが発生します。 これらのハードウェアエラーイベントは、システムイベントログに記録されます。 WHEA によって発生する可能性のあるさまざまなハードウェアエラーイベントの説明については、「[ハードウェアエラーイベント](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)」を参照してください。

アプリケーションでは、WHEA によってログに記録されたすべてのイベントを照会することによって、システムイベントログからハードウェアエラーイベントを取得できます。 システムイベントログから WHEA ハードウェアエラーイベントを取得する方法の例については、「[ハードウェアエラーイベントのシステムイベントログのクエリ](querying-the-system-event-log-for-hardware-error-events.md)」を参照してください。

アプリケーションでは、新しいハードウェアエラーイベントが WHEA によって発生したときに通知を受け取るように登録することもできます。 新しいハードウェアエラーイベントの通知に登録する方法の例については、「[ハードウェアエラーイベントの通知の登録](registering-for-notification-of-hardware-error-events.md)」を参照してください。

システムイベントログに対してクエリを実行したり、イベント通知を受け取ったりすることによって、特定のハードウェアエラーイベントが取得されたかどうかに関係なく、イベントからハードウェアエラーデータを取得するプロセスは同じです。

各ハードウェアエラーイベントには、発生したエラー状態を示す[エラーレコード](error-records.md)が含まれています。 詳細な分析のために、各イベントからエラーレコードを取得できます。

 

 




