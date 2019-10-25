---
title: CustomTimerDpc ルーチンの登録とキュー
description: CustomTimerDpc ルーチンの登録とキュー
ms.assetid: 884bff8e-8437-44fb-acc0-f535d64ce900
keywords:
- タイマーオブジェクト WDK カーネル、CustomTimerDpc ルーチン
- CustomTimerDpc
- タイマーオブジェクトのキュー
- タイマーオブジェクトの登録
- KeSetTimer
- KeSetTimerEx
- KeInitializeTimer
- KeInitializeTimerEx
- CustomTimerDpc ルーチンの繰り返し呼び出し
- CustomTimerDpc ルーチンを繰り返し呼び出す
- DueTime の値
- タイマーの有効期限 WDK カーネル
- 期限切れのタイマー WDK カーネル
- タイマーオブジェクト WDK カーネル、キュー
- タイマーオブジェクト WDK カーネル、登録
- タイマーオブジェクト WDK カーネル、有効期限
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5486063e486fc9e3aa6be9bdb93ab47429b62e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838476"
---
# <a name="registering-and-queuing-a-customtimerdpc-routine"></a>CustomTimerDpc ルーチンの登録とキュー





ドライバーは、通常、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンから次のルーチンを呼び出すことによって、 [*customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンを登録できます。

1.  [**Keinitializer Edpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)でルーチンを登録する

2.  [**Keinitializetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)または[**Keinitializetimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex)によるタイマーオブジェクトの設定

その後、ドライバーは[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)または[**Kesettimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)を呼び出して有効期限を指定し、タイマーオブジェクトをシステムのタイマーキューに追加することができます。 有効期限に達すると、システムによってタイマーオブジェクトがデキューされ、 *Customtimerdpc*ルーチンが呼び出されます。 次の図は、これらの呼び出しを示しています。

![customtimerdpc ルーチンで timer オブジェクトと dpc オブジェクトを使用する方法を示す図](images/3ketmdpc.png)

前の図に示すように、ドライバーは DPC オブジェクトとタイマーオブジェクトの両方の記憶域を提供する必要があります。 ほとんどのドライバーは、[デバイス拡張機能](device-extensions.md)またはその他のドライバーによって割り当てられた常駐メモリ内のこれらのオブジェクトのストレージを提供します。

**KeSetTimer**の呼び出しでは、ドライバーは*Dpc*オブジェクトと*タイマー*オブジェクトへのポインターを、前の図に示すように100ナノ秒単位で表現された*DueTime*と共に渡します。 *DueTime*の正の値は、 *customtimerdpc*ルーチンを呼び出す必要がある (1601 年1月1日以降の)*絶対有効期限*を指定します。 *DueTime*の負の値は、*相対有効期限*を指定します。

絶対タイマーは特定のシステム時刻に期限切れになるため、タイマーが期限切れになる前にシステム時刻が変更されても、絶対タイマーの待機時間は影響を受けません。 一方、相対タイマーは、絶対システム時刻の変更に関係なく、指定された時間単位数が経過すると常に期限切れになります。

*Customtimerdpc*ルーチンを繰り返し呼び出すには、 **Kesettimerex**を使用してタイマーを設定し、 *Period*パラメーターに定期的な間隔を指定します。 **Kesettimerex**は、この追加のパラメーターを除き、 **KeSetTimer**と同じです。

前の図に示すように、 **KeSetTimer**または**Kesettimerex**を呼び出すと、次のように指定された間隔でタイマーオブジェクトがキューに存在します。

1.  *DueTime*の有効期限が切れると、タイマーオブジェクトがデキューされ、シグナル状態に設定されます。

2.  コンピューターのすべてのプロセッサが、ディスパッチ\_レベル以上の IRQL で現在コードを実行している場合、タイマーオブジェクトに関連付けられている DPC オブジェクトは DPC キューに格納されます。 それ以外の場合は、 *Customtimerdpc*ルーチンが呼び出されます。

3.  *DueTime* interval の有効期限が切れたときに DPC オブジェクトが既にキューにある場合、コンピューターのプロセッサの IRQL がディスパッチ\_レベルを下回るとすぐに*customtimerdpc*ルーチンが呼び出されます。

    すべての DPC ルーチンと同様に*Customtimerdpc*ルーチンは、IRQL = DISPATCH\_レベルで呼び出される  に**注意**してください。 DPC ルーチンが実行されている間、すべてのスレッドが同じプロセッサで実行されることはありません。 ドライバー開発者は、できるだけ短い時間で実行するように*Customtimerdpc*ルーチンを慎重に設計する必要があります。

     

**KeSetTimer**と**Kesettimerex**に指定できる最小の時間間隔は約10ミリ秒であるため、ドライバーは[*iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチンよりも短い間隔で、 *customtimerdpc*ルーチンを使用できます。は1秒に1回実行され、はを処理できます。

任意の時点で、特定のタイマーオブジェクトのインスタンス化を1つだけキューに入れることができます。 同じ*タイマー*オブジェクトポインターを使用して**KeSetTimer**または**kesettimerex**を再度呼び出すと、キューに入っているタイマーオブジェクトが取り消され、リセットされます。

[*Customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンの設定は、 [*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンの設定とまったく同じですが、タイマーオブジェクトを初期化するための追加の手順があります。 実際、これらのプロトタイプは同じですが、 *Customtimerdpc*ルーチンは、プロトタイプで宣言されている2つの*systemargument*ポインターを使用できません。

 

 




