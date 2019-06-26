---
title: IoTimer ルーチンの使用
description: IoTimer ルーチンの使用
ms.assetid: 9de2d2ec-31c5-4a60-96bf-5da067d2d9db
keywords:
- IoTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e74de4699e99eba3fabaa91d3f2c4ca11fc32b49
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355225"
---
# <a name="using-an-iotimer-routine"></a>IoTimer ルーチンの使用





タイマーを関連するデバイス オブジェクトが有効になっているときに、 [ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)ルーチンに約 1 秒あたり 1 回呼び出されます。 ただし、ため、各間隔*IoTimer*ルーチンが呼び出される、システム時計の解像度に依存して、あるありません、 *IoTimer*ルーチンは 1 秒で正確に呼び出されます境界。

**注**  、 *IoTimer* IRQL ですべての DPC ルーチンなどのルーチンと呼ばれる = ディスパッチ\_レベル。 DPC ルーチンの実行中のすべてのスレッドは、同じプロセッサで実行できなくなります。 ドライバー開発者は注意深く設計する必要があります、 *IoTimer*できるだけの時間の簡単なため、実行するルーチン。

 

おそらく、最も一般的なを使用する*IoTimer*ルーチンが IRP のタイムアウトになるデバイスの I/O 操作には。 使用して、次のシナリオを検討してください、 *IoTimer*デバイス ドライバー内で実行中のタイマーとしてルーチン。

1.  ドライバーがないことを示す現在のデバイスの I/O 操作、および呼び出し、-1 をデバイスの拡張機能のタイマー カウンターを初期化します、デバイス、開始時に[ **IoStartTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostarttimer)直前の状態を返します\_成功しました。

    毎回、 *IoTimer*ルーチンを呼び出すと、かどうか、タイマー カウンターが-1 の場合、そうである場合は、コントロールを返しますを確認します。

2.  ドライバーの[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンで、上限にデバイスの拡張機能タイマー カウンターと場合、追加の 2 番目の初期化、 *IoTimer*だけルーチンには実行されています。 使用して、 [ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)を呼び出す、 *SynchCritSection\_1*ルーチンで、プログラムによって要求された操作の物理デバイス現在の IRP では。

3.  ドライバーの ISR キュー、ドライバーの前に、タイマーを-1 にカウンターをリセットする[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチンまたは[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)ルーチン。

4.  毎回、 *IoTimer*ルーチンを呼び出すと、-1 の ISR によってタイマー カウンターがリセットされ、コントロールがあればを返すかどうかを確認します。 ない場合、 *IoTimer*ルーチン**KeSynchronizeExecution**を呼び出す、 *SynchCritSection\_2*ルーチンで、いくつかで、タイマー カウンターを調整します。ドライバーにより決定された秒数です。

5.  *SynchCritSection\_2*ルーチンを返します。 **TRUE**を、 *IoTimer*ルーチンの現在の要求がまだタイムアウトしていない限り、します。タイマー カウンターがゼロにする場合、 *SynchCritSection\_2*ルーチンのカウンターをリセット-タイムアウトのドライバーにより決定された値のタイマーをリセット、自身のリセットが予想フラグを設定 (および、 *DpcForIsr*) のコンテキスト 領域で、デバイスをリセットする試みを返します**TRUE**します。

    *SynchCritSection\_2*ルーチンが再度呼び出されます、リセット操作もがタイムアウトした場合、デバイスに戻ったときに**FALSE**します。 そのリセットに成功した場合、 *DpcForIsr*ルーチンと判断したデバイス リセット予想フラグからがリセットされたのアクションを繰り返し、要求の再試行、 *StartIo*ルーチンの説明に従って手順 2。

6.  場合、 *SynchCritSection\_2*ルーチンを返します**FALSE**、 *IoTimer*ルーチンは、ために、物理デバイスが不明な状態が前提としています。 しようとしました。リセットが既にに失敗しました。 このような場合、 *IoTimer*日常的なキュー、 *CustomDpc*ルーチンを返します。 これは、 *CustomDpc*ルーチンは、デバイスの I/O エラー、呼び出しをログ[**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)、現在の IRP が失敗し、返します。

ドライバーの手順 3. で説明されているように、このデバイス ドライバの ISR が共有のタイマーを-1 にカウンターをリセットした場合*DpcForIsr*ルーチンが現在の IRP の I/O の割り込み駆動処理を完了します。 タイマー カウンターのリセットでは、このデバイスの I/O 操作が、タイムアウトしていないことを示しますが、そのため*IoTimer*ルーチンは、タイマー カウンターを変更する必要はありません。

上記のほとんどの状況で*SynchCritSection\_2*ルーチン単純にタイマー カウンター。 *SynchCritSection\_2*ルーチンのみであるには、タイマー カウンターがゼロになる場合が示される場合は、現在の I/O 操作がタイムアウトになっている場合、デバイスをリセットしようとしました。 デバイスをリセットしようとすると、既に失敗した場合にのみ、 *SynchCritSection\_2*ルーチンの戻り値**FALSE**を*IoTimer*ルーチン。

その結果、両方の前に*IoTimer*ルーチンとそのヘルパー *SynchCritSection\_2*ルーチンが通常の状況で実行するには、ほとんどの時間を取得します。 使用して、 *IoTimer*この方法で日常的なデバイス ドライバーにより、各デバイス I/O が有効な要求を再試行できます必要に応じて、および、 *CustomDpc*修正不可能な場合にのみ、ルーチンの IRP が失敗します。ハードウェアの障害には、満たされているから IRP ができないようにします。 さらに、ドライバーは、実行時間のごくわずかなコストでこの機能を提供します。

上記のシナリオの簡潔さは、デバイスには、一度に 1 つだけの操作および I/O 操作を通常重複しないドライバーによって異なります。 デバイス I/O がオーバー ラップの操作を実行するドライバーまたはを使用するより高度なドライバー、 *IoTimer*がタイムアウトする日常的な一連のドライバーに割り当てられた Irp が下位のドライバーの 1 つ以上のチェーンに送信される必要がありますより複雑なタイムアウト管理するシナリオ。

 

 




