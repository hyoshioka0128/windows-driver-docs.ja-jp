---
title: タイマー オブジェクトの使用
description: タイマー オブジェクトの使用
ms.assetid: b3ee9d92-87b9-47b7-ab13-11e42bec7997
keywords:
- タイマー オブジェクトの WDK カーネル、待機しています。
- タイマー オブジェクトを待機しています。
- 通知タイマー WDK カーネル
- KeDelayExecutionThread
- Kewaitforsingleobject の 1
- KeInitializeTimer
- KeSetTimer
- DueTime 値
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c8ec4e30dd6e03ea9ed1ea1f152443151174f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358166"
---
# <a name="using-timer-objects"></a>タイマー オブジェクトの使用





次の図は、操作のタイムアウト間隔を設定し、その他のドライバーのルーチンが、I/O 要求が処理されるを待ち通知タイマーの使用を示します。

![タイマー オブジェクトの待機を示す図](images/3ketimer.png)

ドライバーがへの呼び出しによって初期化される必要があります、タイマー オブジェクトの記憶域を提供する必要があります、前の図に示す[ **KeInitializeTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimer)この記憶域へのポインター。 通常、ドライバーでは、この呼び出しからその[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。

ドライバーが作成したスレッドまたは同期 I/O 操作を要求するスレッドなどの特定のスレッドのコンテキスト内で、ドライバーは、前の図に示すように、タイマー オブジェクトを待機できます。

1.  スレッドの呼び出し[ **KeSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)タイマー オブジェクトへのポインターを指定された*DueTime*を 100 ナノ秒単位で表現される値。 正の値*DueTime*タイマー オブジェクトをカーネルのタイマー キューから削除して、シグナルされた状態に設定、位置、絶対時刻を指定します。 負の値を*DueTime*の現在のシステム時間を基準と間隔を指定します。

    スレッド (またはシステムのスレッドで定期的な実行をドライバー) を渡しますが、 **NULL** DPC オブジェクトへのポインター (図の説明で示した[CustomTimerDpc ルーチンのタイマーとDPCオブジェクトの使用](registering-and-queuing-a-customtimerdpc-routine.md))呼び出し時に**KeSetTimer**キューではなく、タイマー オブジェクトで待機しているかどうか、 [ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチン。

2.  スレッドの呼び出し[ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)タイマー オブジェクトへのポインターは、スレッドを待機状態タイマー オブジェクトは、カーネルのタイマー キュー。

3.  指定した*DueTime*有効期限が切れます。

4.  カーネルは、タイマー オブジェクトをキューから、シグナルされた状態に設定および準備完了状態に待機から、スレッドの状態を変更します。

5.  カーネルは、プロセッサが使用可能なすぐにスレッドの実行をディスパッチします。 つまり、優先度が高いその他のスレッドは現在準備完了状態で、より高い IRQL で実行されるルーチンをカーネル モードではありません。

IRQL で実行されるドライバー ルーチン&gt;= ディスパッチ\_レベルは、ドライバーによって提供されるキューに関連付けられている DPC オブジェクトをタイマー オブジェクトを使用して要求のタイムアウトをできます[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチン。 前の図に示すように、nonarbitrary スレッドのコンテキスト内で実行されるドライバー ルーチンのみが、タイマー オブジェクトの 0 以外の値の間隔を待機できます。

その他のすべてのスレッドのようなドライバーが作成したスレッドはディスパッチャー オブジェクトでも、カーネル スレッド オブジェクトによって表されます。 その結果、ドライバーでは、そのドライバーが作成したスレッドが自主的に配置する自体、待機状態に一定期間タイマー オブジェクトを使用してある必要はありません。 代わりに、スレッドを呼び出すことができます[ **KeDelayExecutionThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kedelayexecutionthread)呼び出し元が指定の間隔を使用します。 この手法の詳細については、次を参照してください。[デバイスのポーリング](avoid-polling-devices.md)します。

[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)、 [*を再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)、および[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチンは、システムのスレッドでも実行コンテキスト、ドライバーを呼び出せるように**kewaitforsingleobject の 1**ドライバー初期化タイマー オブジェクトを使用または**KeDelayExecutionThread**の初期化中またはアンロードされるときにします。 デバイス ドライバーを呼び出すことができます[ **KeStallExecutionProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-kestallexecutionprocessor)非常に短い間隔 (可能であればものより小さい 50 マイクロ秒) の場合は、デバイスの初期化中に状態を更新するを待機します.

ただしより高度なドライバーは、別の同期メカニズムで一般を使用、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)と[*を再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)タイマー オブジェクトを使用する代わりにルーチン。 高度なドライバーは、特定の種類またはデバイスの種類の任意の下位のドライバーの上に常に設計必要があります。 そのためより高度なドライバーは、タイマー オブジェクトまたは呼び出しを待機している場合は読み込みに遅くなることがする傾向があります**KeDelayExecutionThread**ため、このようなドライバーする必要がありますのを待機間隔十分な時間が最も遅い可能なデバイスに対応するために。それをサポートします。 このような待機の「安全」ですが最小間隔が判断するは非常に困難にも注意してください。

PnP ドライバーがその他の操作が発生する待機しない同様に、代わりに、PnP マネージャーを使用する必要がありますが、[通知](using-pnp-notification.md)メカニズム。

 

 




