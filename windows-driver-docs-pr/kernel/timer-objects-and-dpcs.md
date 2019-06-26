---
title: KeXxxTimer ルーチン、KTIMER オブジェクト、DPC
description: Windows 2000 以降、KeXxxTimer ルーチンのセットはタイマーの管理に使用できます。
ms.assetid: b58487de-6e9e-45f4-acb8-9233c8718ee2
keywords:
- タイマーの WDK カーネル
- タイマー オブジェクトの WDK カーネル
- タイマー オブジェクトについて、タイマー オブジェクトの WDK カーネル
- 遅延プロシージャ呼び出しの WDK カーネル
- Dpc WDK カーネル
- カーネルのディスパッチャー オブジェクト WDK、タイマー オブジェクト
- ディスパッチャー オブジェクト WDK カーネル、タイマー オブジェクト
- 通知タイマー WDK カーネル
- 同期のタイマーの WDK カーネル
- KTIMER
- KeXxxTimer ルーチン
- KeInitializeTimer
- KeInitializeTimerEx
- KeSetTimer
- KeSetTimerEx
- CustomTimerDpc
- タイムアウト間隔の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6129d2abd868a0be01b638fabc3cf4ed8320a39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382955"
---
# <a name="kexxxtimer-routines-ktimer-objects-and-dpcs"></a>KeXxxTimer ルーチン、KTIMER オブジェクト、DPC


以降では、Windows 2000 では、一連の**Ke*Xxx*タイマー**ルーチンがタイマーの管理に使用します。 これらのルーチンを使用して、タイマー オブジェクトに基づく、 [ **KTIMER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体。 タイマー オブジェクトを作成するドライバーを最初にストレージを割り当てるを**KTIMER**構造体。 ドライバーなどのルーチンの呼び出し、 [ **KeInitializeTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimer)または[ **KeInitializeTimerEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimerex)この構造体を初期化します。




1 回だけは、有効期限が切れるか、繰り返し一定期間切れになるよう、タイマーを設定できます。 [**KeSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)常に 1 回だけの有効期限をタイマーを設定します。 [**KeSetTimerEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimerex)受け取る省略可能な*期間*パラメーターで、定期的なタイマーの間隔を指定します。

省略可能な[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチン (遅延プロシージャ呼び出しの種類) と関連付けができる通知タイマーまたは同期タイマーのいずれか。 このルーチンは、指定した期間、有効期限が切れるときに実行されます。 詳細については、次を参照してください。[タイマー オブジェクトを使用する](using-timer-objects.md)します。

タイマーを*通知タイマー*または*同期タイマー*します。

-   通知タイマーがシグナルを受け取る、待機中のすべてのスレッドは満足の待機があります。 タイマーの状態をシグナル状態のまま、明示的にリセットされるまでです。

-   同期のタイマーの期限が切れると、単一の待機スレッドが解放されるまでに、その状態がシグナルされたに設定されます。 タイマーは、非シグナル状態にリセットされます。

**KeInitializeTimer**通知タイマーを常に作成されます。 **KeInitializeTimerEx**を受け入れる、*型*パラメーターとして指定できます**NotificationTimer**または**SynchronizationTimer**します。

タイマー オブジェクトと Dpc の詳細については、以下のトピックです。

[タイマー オブジェクトを使用して](using-timer-objects.md)
[タイマー精度](timer-accuracy.md)
[CustomTimerDpc ルーチンのキューの登録と](registering-and-queuing-a-customtimerdpc-routine.md)
[を提供します。CustomTimerDpc コンテキスト情報](providing-customtimerdpc-context-information.md)
[CustomTimerDpc ルーチンを使用して](using-a-customtimerdpc-routine.md)
 

 




