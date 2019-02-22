---
title: タイマー オブジェクトを使用します。
description: タイマー オブジェクトを使用します。
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
ms.openlocfilehash: f90310aa08bd9780a70f619c998a93f72ee2c57f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537120"
---
# <a name="using-timer-objects"></a>タイマー オブジェクトを使用します。





次の図は、操作のタイムアウト間隔を設定し、その他のドライバーのルーチンが、I/O 要求が処理されるを待ち通知タイマーの使用を示します。

![タイマー オブジェクトの待機を示す図](images/3ketimer.png)

ドライバーがへの呼び出しによって初期化される必要があります、タイマー オブジェクトの記憶域を提供する必要があります、前の図に示す[ **KeInitializeTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff552168)この記憶域へのポインター。 通常、ドライバーでは、この呼び出しからその[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

ドライバーが作成したスレッドまたは同期 I/O 操作を要求するスレッドなどの特定のスレッドのコンテキスト内で、ドライバーは、前の図に示すように、タイマー オブジェクトを待機できます。

1.  スレッドの呼び出し[ **KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286)タイマー オブジェクトへのポインターを指定された*DueTime*を 100 ナノ秒単位で表現される値。 正の値*DueTime*タイマー オブジェクトをカーネルのタイマー キューから削除して、シグナルされた状態に設定、位置、絶対時刻を指定します。 負の値を*DueTime*の現在のシステム時間を基準と間隔を指定します。

    スレッド (またはシステムのスレッドで定期的な実行をドライバー) を渡しますが、 **NULL** DPC オブジェクトへのポインター (図の説明で示した[CustomTimerDpc ルーチンのタイマーとDPCオブジェクトの使用](registering-and-queuing-a-customtimerdpc-routine.md))呼び出し時に**KeSetTimer**キューではなく、タイマー オブジェクトで待機しているかどうか、 [ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチン。

2.  スレッドの呼び出し[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)タイマー オブジェクトへのポインターは、スレッドを待機状態タイマー オブジェクトは、カーネルのタイマー キュー。

3.  指定した*DueTime*有効期限が切れます。

4.  カーネルは、タイマー オブジェクトをキューから、シグナルされた状態に設定および準備完了状態に待機から、スレッドの状態を変更します。

5.  カーネルは、プロセッサが使用可能なすぐにスレッドの実行をディスパッチします。 つまり、優先度が高いその他のスレッドは現在準備完了状態で、より高い IRQL で実行されるルーチンをカーネル モードではありません。

IRQL で実行されるドライバー ルーチン&gt;= ディスパッチ\_レベルは、ドライバーによって提供されるキューに関連付けられている DPC オブジェクトをタイマー オブジェクトを使用して要求のタイムアウトをできます[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチン。 前の図に示すように、nonarbitrary スレッドのコンテキスト内で実行されるドライバー ルーチンのみが、タイマー オブジェクトの 0 以外の値の間隔を待機できます。

その他のすべてのスレッドのようなドライバーが作成したスレッドはディスパッチャー オブジェクトでも、カーネル スレッド オブジェクトによって表されます。 その結果、ドライバーでは、そのドライバーが作成したスレッドが自主的に配置する自体、待機状態に一定期間タイマー オブジェクトを使用してある必要はありません。 代わりに、スレッドを呼び出すことができます[ **KeDelayExecutionThread** ](https://msdn.microsoft.com/library/windows/hardware/ff551986)呼び出し元が指定の間隔を使用します。 この手法の詳細については、次を参照してください。[デバイスのポーリング](avoid-polling-devices.md)します。

[**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)、 [*を再初期化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)、および[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチンは、システムのスレッドでも実行コンテキスト、ドライバーを呼び出せるように**kewaitforsingleobject の 1**ドライバー初期化タイマー オブジェクトを使用または**KeDelayExecutionThread**の初期化中またはアンロードされるときにします。 デバイス ドライバーを呼び出すことができます[ **KeStallExecutionProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff553295)非常に短い間隔 (可能であればものより小さい 50 マイクロ秒) の場合は、デバイスの初期化中に状態を更新するを待機します.

ただしより高度なドライバーは、別の同期メカニズムで一般を使用、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)と[*を再初期化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)タイマー オブジェクトを使用する代わりにルーチン。 高度なドライバーは、特定の種類またはデバイスの種類の任意の下位のドライバーの上に常に設計必要があります。 そのためより高度なドライバーは、タイマー オブジェクトまたは呼び出しを待機している場合は読み込みに遅くなることがする傾向があります**KeDelayExecutionThread**ため、このようなドライバーする必要がありますのを待機間隔十分な時間が最も遅い可能なデバイスに対応するために。それをサポートします。 このような待機の「安全」ですが最小間隔が判断するは非常に困難にも注意してください。

PnP ドライバーがその他の操作が発生する待機しない同様に、代わりに、PnP マネージャーを使用する必要がありますが、[通知](using-pnp-notification.md)メカニズム。

 

 




