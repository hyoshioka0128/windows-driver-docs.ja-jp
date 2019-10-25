---
title: KeXxxTimer ルーチン、KTIMER オブジェクト、DPC
description: Windows 2000 以降では、一連の KeXxxTimer ルーチンを使用してタイマーを管理できます。
ms.assetid: b58487de-6e9e-45f4-acb8-9233c8718ee2
keywords:
- タイマー WDK カーネル
- タイマーオブジェクト WDK カーネル
- タイマーオブジェクト WDK カーネル、タイマーオブジェクトについて
- 遅延プロシージャ呼び出し WDK カーネル
- Dpc WDK カーネル
- カーネルディスパッチャーオブジェクト WDK、タイマーオブジェクト
- ディスパッチャーオブジェクト WDK カーネル、タイマーオブジェクト
- 通知タイマー WDK カーネル
- 同期タイマー WDK カーネル
- KTIMER
- KeXxxTimer ルーチン
- KeInitializeTimer
- KeInitializeTimerEx
- KeSetTimer
- KeSetTimerEx
- CustomTimerDpc
- タイムアウト間隔 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb51282f76bee15468be7957802307bc761b0369
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838387"
---
# <a name="kexxxtimer-routines-ktimer-objects-and-dpcs"></a>KeXxxTimer ルーチン、KTIMER オブジェクト、DPC


Windows 2000 以降では、タイマーを管理するための一連の**Ke*Xxx*タイマー**ルーチンを使用できます。 これらのルーチンは、 [**Ktimer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造に基づくタイマーオブジェクトを使用します。 タイマーオブジェクトを作成するために、ドライバーはまず**Ktimer**構造にストレージを割り当てます。 次に、ドライバーは[**Keinitializetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)や[**Keinitializetimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex)などのルーチンを呼び出して、この構造体を初期化します。




タイマーは、1回だけ有効期限が切れるように設定することも、特定の間隔で繰り返し有効期限を切れるように設定することもできます。 [**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)は、常に1回だけ有効期限が切れるタイマーを設定します。 [**Kesettimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)は、定期的なタイマー間隔を指定するオプションの*Period*パラメーターを受け取ります。

省略可能な[*Customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチン (遅延プロシージャ呼び出しの一種) は、通知タイマーまたは同期タイマーに関連付けることができます。 このルーチンは、指定した時間間隔が経過すると実行されます。 詳細については、「 [Timer オブジェクトの使用](using-timer-objects.md)」を参照してください。

タイマーは、*通知タイマー*または*同期タイマー*にすることができます。

-   通知タイマーがシグナル状態になると、待機中のすべてのスレッドの待機が満たされます。 タイマーの状態は、明示的にリセットされるまでシグナル状態のままになります。

-   同期タイマーの有効期限が切れると、1つの待機中のスレッドが解放されるまで、その状態はシグナル状態に設定されます。 その後、タイマーはシグナル状態ではない状態にリセットされます。

**Keinitializetimer**は、常に通知タイマーを作成します。 **Keinitializetimerex**は、 **Notificationtimer**または**同期タイマー**として使用できる*型*パラメーターを受け取ります。

次のトピックでは、タイマーオブジェクトと Dpc の詳細について説明します。

[タイマーオブジェクトの使用](using-timer-objects.md)
[タイマー精度](timer-accuracy.md)
Customtimerdpc ルーチンを[登録してキューに登録し](registering-and-queuing-a-customtimerdpc-routine.md)、Customtimerdpc[コンテキスト
情報を提供](providing-customtimerdpc-context-information.md)する
[customtimerdpc ルーチンを使用](using-a-customtimerdpc-routine.md)する
 

 




