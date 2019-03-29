---
title: WHEA ハードウェア エラー イベント
description: WHEA ハードウェア エラー イベント
ms.assetid: c9f88e3b-3915-4a77-8d60-f0f3da514abc
keywords:
- イベントに関するイベント WDK WHEA では、
- Windows ハードウェア エラー アーキテクチャ WDK のイベント
- WHEA WDK、イベント
- ハードウェア エラー WDK WHEA、イベント
- WDK WHEA、イベントのエラー
- ハードウェア エラー イベント WDK WHEA
- WDK WHEA イベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4113478be650c3c8cccd820b1cbbc123b10677b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579556"
---
# <a name="whea-hardware-error-events"></a>WHEA ハードウェア エラー イベント


Windows ハードウェア エラー アーキテクチャ (WHEA) は、ハードウェア エラーが発生したときに、Event Tracing for Windows (ETW) イベントを発生させます。 これらのハードウェア エラー イベントは、システム イベント ログに記録されます。 WHEA によって発生するさまざまなハードウェアのエラー イベントの説明については、次を参照してください。[ハードウェア エラー イベント](https://msdn.microsoft.com/library/windows/hardware/ff559387)します。

アプリケーションは、WHEA によってログに記録されたイベントをクエリすることによって、システム イベント ログからハードウェア エラー イベントを取得できます。 システム イベント ログから WHEA ハードウェア エラーのイベントを取得する方法の例については、次を参照してください。[のハードウェア エラー イベント、システム イベント ログを照会](querying-the-system-event-log-for-hardware-error-events.md)します。

アプリケーションは、WHEA によって新しいハードウェアのエラー イベントが発行されるたびに通知にも登録できます。 新しいハードウェアのエラー イベントの通知に登録する方法の例については、次を参照してください。[ハードウェア エラー イベントの通知の登録](registering-for-notification-of-hardware-error-events.md)します。

かどうか、特定のハードウェアのエラー イベントは、システム イベント ログを照会することによって、またはイベント通知を受信することによって取得されたに関係なく、イベントから、ハードウェア エラーのデータを取得するプロセスは同じです。

各ハードウェア エラー イベントが含まれる、[エラー レコード](error-records.md)発生したエラー条件をについて説明します。 各イベントの詳細な分析からエラー レコードを取得できます。

 

 




