---
title: IoTimer ルーチンの登録と有効化
description: IoTimer ルーチンの登録と有効化
ms.assetid: d06a6430-5098-492a-8114-d6f390083718
keywords:
- IoTimer
- IoInitializeTimer
- IoStartTimer
- IoTimer ルーチンを登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f94cc6d46cd0c0fdb9c2fc4c8fed9603ef522810
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385855"
---
# <a name="registering-and-enabling-an-iotimer-routine"></a>IoTimer ルーチンの登録と有効化





すべてのドライバーが登録できる、 [ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)ルーチンを呼び出すことによって、1 つまたは複数のデバイス オブジェクトが作成された後[ **IoInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializetimer)します。 ドライバーを呼び出してタイマーを開始できます[ **IoStartTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostarttimer)します。 次の図は、これらの呼び出しを示しています。

![iotimer ルーチンを使用して説明する図](images/3iotmer.png)

呼び出した後[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)デバイス オブジェクトを作成するドライバーを呼び出すことができます**IoInitializeTimer**のエントリ ポイントとその*IoTimer*日常的なデバイスのドライバーが作成したオブジェクトと、ドライバーがどのようなコンテキストを保持しますコンテキスト領域へのポインターと共にその*IoTimer*ルーチン。 I/O マネージャーは、タイマーのカーネルに割り当てられたオブジェクトをデバイス オブジェクトを関連付け、1 秒ごとにこのタイムアウト タイマー オブジェクトを設定します。

ドライバーの呼び出し後**IoStartTimer**その*IoTimer*ルーチンはドライバー呼び出されるまで 1 秒あたり 1 回呼び出されます[ **IoStopTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostoptimer)します。 ドライバーの呼び出しを再び有効にできる、 *IoTimer*ルーチン**IoStartTimer**します。 (多くの場合、ドライバーを呼び出すと**IoStartTimer**、現在の IRP の I/O スタックの場所から取得したデバイス オブジェクト ポインターを提供します)。

開始時、 *IoTimer*ルーチンには、デバイスのオブジェクト ポインターが渡された<em>、</em>ドライバーにはときに指定したコンテキストのポインターと共にと呼ばれる**IoInitializeTimer**。

ドライバーを呼び出してはならない**IoStopTimer**内から、 *IoTimer*ルーチン。

I/O マネージャーが、指定したデバイス オブジェクトのタイマーのルーチンの登録を解除し、ドライバーを呼び出すと、その関連付けられたコンテキストを解放[ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)します。

 

 




