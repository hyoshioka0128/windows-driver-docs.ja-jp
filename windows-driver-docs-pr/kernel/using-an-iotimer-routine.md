---
title: IoTimer ルーチンの使用
description: IoTimer ルーチンの使用
ms.assetid: 9de2d2ec-31c5-4a60-96bf-5da067d2d9db
keywords:
- IoTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e1d778be762313022af54994da9b24df5d5fef8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838363"
---
# <a name="using-an-iotimer-routine"></a>IoTimer ルーチンの使用





関連付けられているデバイスオブジェクトのタイマーが有効になっている間、 [*Iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチンは1秒間に約1回呼び出されます。 ただし、各*iotimer*ルーチンが呼び出される間隔はシステムクロックの解像度によって異なるため、 *iotimer*ルーチンが1秒の境界で正確に呼び出されると想定しないでください。

すべての DPC ルーチンなどの*Iotimer*ルーチンは、IRQL = DISPATCH\_レベルで呼び出される  に**注意**してください。 DPC ルーチンが実行されている間、すべてのスレッドが同じプロセッサで実行されることはありません。 ドライバー開発者は、できるだけ短い時間で実行するように*Iotimer*ルーチンを慎重に設計する必要があります。

 

*Iotimer*ルーチンで最も一般的に使用されるのは、IRP に対するデバイス i/o 操作のタイムアウトです。 デバイスドライバー内で実行中のタイマーとして*iotimer*ルーチンを使用する場合は、次のシナリオを考慮してください。

1.  デバイスを起動すると、ドライバーはデバイス拡張機能のタイマーカウンターを-1 に初期化します。これは、現在のデバイス i/o 操作がないことを示します。さらに、 [**Iostarttimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostarttimer)を呼び出して、ステータス\_成功を返します。

    *Iotimer*ルーチンが呼び出されるたびに、タイマーカウンターが-1 であるかどうかがチェックされ、存在する場合はコントロールを返します。

2.  ドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンは、デバイス拡張機能のタイマーカウンターを上限に初期化します。さらに、 *iotimer*ルーチンが実行されたばかりの場合は、追加の秒数を初期化します。 次に、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を使用して、現在の IRP によって要求された操作の物理デバイスをプログラムする*SynchCritSection\_1*ルーチンを呼び出します。

3.  ドライバーの ISR は、ドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンまたは[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンをキューに再設定する前に、タイマーカウンターを-1 にリセットします。

4.  *Iotimer*ルーチンが呼び出されるたびに、timer カウンターが ISR によってリセットされたかどうかが-1 に設定されているかどうかがチェックされ、存在する場合は制御が返されます。 それ以外の場合、 *Iotimer*ルーチンは**KeSynchronizeExecution**を使用して*SynchCritSection\_2*ルーチンを呼び出します。これにより、ドライバーによって決められた秒数だけタイマーカウンターが調整されます。

5.  *SynchCritSection\_2*ルーチンは、現在の要求がまだタイムアウトしていない限り、 *Iotimer*ルーチンに**TRUE**を返します。タイマーカウンターが0に設定されている場合、 *SynchCritSection\_2*ルーチンは、タイマーカウンターをドライバーによって決定されたリセットタイムアウト値にリセットし、そのコンテキスト領域の*DpcForIsr*に対して予期されるリセットフラグを設定します。デバイスをリセットし、 **TRUE**を返します。

    *SynchCritSection\_2*ルーチンは、リセット操作がデバイスでもタイムアウトした場合に、 **FALSE**を返すと再度呼び出されます。 リセットが成功した場合、 *DpcForIsr*ルーチンは、デバイスがリセットが必要なフラグからリセットされたことを確認し、要求を再試行して、手順 2. の説明に従って*StartIo*ルーチンのアクションを繰り返します。

6.  *SynchCritSection\_2*ルーチンが**FALSE**を返す場合、 *iotimer*ルーチンは、物理デバイスをリセットしようとすると、既に失敗しているため、物理デバイスが不明な状態であると想定します。 このような状況では、 *Iotimer*ルーチンは*customdpc*ルーチンをキューに置いてを返します。 この*Customdpc*ルーチンは、デバイスの i/o エラーをログに記録し、 [**Iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出して、現在の IRP に失敗して、を返します。

このデバイスドライバーの ISR によって共有タイマーカウンターが-1 にリセットされた場合、手順 3. で説明したように、ドライバーの*DpcForIsr*ルーチンは、現在の IRP の割り込みドリブン i/o 処理を完了します。 Reset timer カウンターは、このデバイス i/o 操作がタイムアウトしていないことを示しているため、 *iotimer*ルーチンはタイマーカウンターを変更する必要がありません。

ほとんどの状況では、上記の*SynchCritSection\_2*ルーチンは timer カウンターをデクリメントするだけです。 *SynchCritSection\_2*ルーチンは、現在の i/o 操作がタイムアウトした場合にのみデバイスをリセットしようとします。これは、タイマーカウンターがゼロになったときに示されます。 また、デバイスをリセットしようとして失敗した場合にのみ、 *SynchCritSection\_2*ルーチンが*Iotimer*ルーチンに**FALSE**を返します。

その結果、上記の*Iotimer*ルーチンとそのヘルパー *SynchCritSection\_2*ルーチンは、通常の状況での実行に非常に短い時間を要することになります。 この方法で*Iotimer*ルーチンを使用することにより、デバイスドライバーは、有効なデバイス i/o 要求が、必要に応じて再試行できることを保証します。また、修正不可能なハードウェア障害によって irp が動作しなくなる場合にのみ、*カスタム DPC*ルーチンが irp を失敗させることを保証します。満たさ. さらに、ドライバーは、この機能を実行時間のごくわずかなコストで提供します。

上記のシナリオの単純さは、一度に1つの操作のみを実行するデバイスと、通常は i/o 操作が重複しないドライバーに依存しています。 重複するデバイス i/o 操作を実行するドライバー、または*Iotimer*ルーチンを使用してドライバーによって割り当てられた一連の irp を、下位のドライバーの複数のチェーンに送信するドライバーで割り当てられた irp のセットをタイムアウトさせるドライバーは、より複雑なタイムアウトシナリオを管理します。

 

 




