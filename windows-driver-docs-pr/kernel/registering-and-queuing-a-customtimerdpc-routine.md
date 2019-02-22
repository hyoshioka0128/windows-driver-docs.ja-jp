---
title: 登録して、CustomTimerDpc ルーチンのキュー
description: 登録して、CustomTimerDpc ルーチンのキュー
ms.assetid: 884bff8e-8437-44fb-acc0-f535d64ce900
keywords:
- タイマー オブジェクトの WDK カーネル、CustomTimerDpc ルーチン
- CustomTimerDpc
- キューのタイマー オブジェクト
- タイマー オブジェクトの登録
- KeSetTimer
- KeSetTimerEx
- KeInitializeTimer
- KeInitializeTimerEx
- 繰り返し CustomTimerDpc ルーチンを呼び出す
- 繰り返し CustomTimerDpc ルーチンを呼び出す
- DueTime 値
- タイマーの有効期限の WDK カーネル
- 有効期限が切れたタイマー WDK カーネル
- タイマー オブジェクトの WDK カーネル キュー
- タイマー オブジェクトの WDK カーネルを登録します。
- タイマー オブジェクトの WDK カーネル、有効期限の設定
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d328e808a94225536cd8ef31216a86ecf8a477c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558796"
---
# <a name="registering-and-queuing-a-customtimerdpc-routine"></a>登録して、CustomTimerDpc ルーチンのキュー





ドライバーが登録できる、 [ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンからは、通常、次のルーチンを呼び出すことによってその[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

1.  [**KeInitializeDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552130)ルーチンを登録するには

2.  [**KeInitializeTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff552168)または[ **KeInitializeTimerEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552173)タイマー オブジェクトを設定するには

その後、ドライバーが呼び出せる[ **KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286)または[ **KeSetTimerEx** ](https://msdn.microsoft.com/library/windows/hardware/ff553292)有効期限を指定し、タイマー オブジェクトを追加するにはシステムのタイマー キュー。 タイマー オブジェクトと呼び出し、有効期限に達すると、システムのキューから、 *CustomTimerDpc*ルーチン。 次の図は、これらの呼び出しを示しています。

![customtimerdpc ルーチンのタイマーおよび dpc オブジェクトの使用を示す図](images/3ketmdpc.png)

前の図に示すよう、ドライバーは DPC オブジェクトとタイマー オブジェクトの両方の記憶域を指定する必要があります。 ほとんどのドライバーは、これらのオブジェクトのストレージを[デバイス拡張機能](device-extensions.md)またはその他のドライバーに割り当てられた、常駐メモリ。

呼び出しで**KeSetTimer**、ドライバーへのポインターを渡す、 *Dpc*と*タイマー*オブジェクト、と共にで、 *DueTime*単位で表されました。前の図に示すように 100 ナノ秒です。 正の値*DueTime*を指定します、*絶対有効期限*(以降、1601 年 1 月 1 日) を*CustomTimerDpc*ルーチンを呼び出す必要があります。 負の値を*DueTime*を指定します、*相対的な有効期限*します。

絶対タイマーは、特定のシステム時に有効期限が切れる、ため、絶対のタイマーの待機時間は、タイマーの前に、システム時刻の変更の有効期限が切れた場合に影響しません。 これに対して、相対的なタイマーは、指定した数の絶対のシステム時刻の変更に関係なくの時間の単位が経過後に常に有効期限です。

呼び出す、 *CustomTimerDpc*ルーチンを使用して、繰り返し、 **KeSetTimerEx**タイマーを設定し、定期的な間隔での指定、*期間*パラメーター。 **KeSetTimerEx**と同じように、 **KeSetTimer**を除き、このパラメーターを追加します。

呼び出し前の図に示すように**KeSetTimer**または**KeSetTimerEx**タイマー オブジェクトを次のように指定した期間キューします。

1.  ときに、 *DueTime*有効期限が切れると、タイマー オブジェクトをキューから削除され、シグナルされた状態に設定します。

2.  各プロセッサ コンピューターで現在実行している場合コード IRQL でディスパッチ以上\_レベル、タイマー オブジェクトに関連付けられた DPC オブジェクトは、DPC キューに配置されます。 それ以外の場合、 *CustomTimerDpc*ルーチンが呼び出されます。

3.  DPC オブジェクトは、キュー内に既に場合と、 *DueTime*期限が切れた、 *CustomTimerDpc*ルーチンは、マシンのすべてのプロセッサ上の IRQL を下回るディスパッチとすぐと呼ばれる\_レベルです。

    **注**  、 *CustomTimerDpc* IRQL ですべての DPC ルーチンなどのルーチンと呼ばれる = ディスパッチ\_レベル。 DPC ルーチンの実行中のすべてのスレッドは、同じプロセッサで実行できなくなります。 ドライバー開発者は注意深く設計する必要があります、 *CustomTimerDpc*できるだけの時間の簡単なため、実行するルーチン。

     

指定できる最小の時間間隔**KeSetTimer**と**KeSetTimerEx**約 10 ミリ秒では、ドライバーが使用できるように、 *CustomTimerDpc*ルーチンも短い間隔の時間を計測、 [ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)ルーチンで、毎秒 1 回の実行を処理できます。

特定のタイマー オブジェクトの 1 つだけインスタンス化は、任意の時点でキューに登録できます。 呼び出す**KeSetTimer**または**KeSetTimerEx**同じ使用してもう一度*タイマー*オブジェクト ポインターのキューに置かれたタイマー オブジェクトをキャンセルし、リセットします。

設定する、 [ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンを設定するとまったく同じには、 [ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチンを初期化するために追加の手順タイマー オブジェクト。 そのプロトタイプは同じですが、実際が*CustomTimerDpc*ルーチンは、2 つを使用できません*SystemArgument*ポインターがプロトタイプで宣言します。

 

 




