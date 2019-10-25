---
title: 共有している状態情報へのアクセス
description: 共有している状態情報へのアクセス
ms.assetid: f3e5ac07-cab1-4f66-90e4-88b2e28079a5
keywords:
- クリティカルセクションルーチン WDK カーネル
- タイマーカウンター WDK カーネル
- 共有状態情報 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04a7b9ba98ae50837e0cb5a98a0b7887737c49a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828682"
---
# <a name="accessing-shared-state-information"></a>共有している状態情報へのアクセス





状態を維持する[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンの設計と作成には、次の一般的なガイドラインを使用します。

-   また、ISR がアクセスするデータにアクセスするには、ドライバールーチンで*SynchCritSection*ルーチンを呼び出す必要があります。 重要ではないセクションコードは中断できます。 Isr でもアクセスされるデータを保護するためにスピンロックを取得するだけでは十分ではないことに注意してください。これは、Isr が DIRQL で実行され、スピンロック ([**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)) を取得するための\_IRQL のみを発生させ、割り込みを可能にするためです。現在のプロセッサで ISR を呼び出します。

-   状態変数の個別のセットについて、状態情報を保持する各*SynchCritSection*ルーチンを提供します。 つまり、重複する状態情報を保持する*SynchCritSection*ルーチンを記述することは避けてください。

    これにより、 *SynchCritSection*ルーチン (および ISR) 間の競合 (場合によっては競合状態) が同じ状態に同時にアクセスしようとします。

    また、1つの*SynchCritSection*ルーチンは、同じ状態情報の一部を更新して制御を返すことができないため、各*SynchCritSection*ルーチンはできるだけ早く制御を戻します。

-   実際に有用な作業を実行するよりも、条件のテストを実行する単一の大規模な汎用*SynchCritSection*ルーチンを作成するのは避けてください。 一方、条件付きステートメントを実行しない*SynchCritSection*ルーチンが多数ある場合は、それぞれが1バイトの状態情報を更新するだけで済みます。

-   *SynchCritSection*ルーチンを実行すると、ドライバーの ISR が実行されないため、すべての*SynchCritSection*ルーチンはできるだけ早く制御を返す必要があります。

次に、デバイス拡張機能でタイマーカウンターを維持する方法を示します。 ドライバーがカウンターを使用して、i/o 操作がタイムアウトしたかどうかを判断します。また、ドライバーが i/o 操作と重複しないことを想定しています。

-   ドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンは、それぞれの i/o 要求に対してタイマーカウンターを初期値に初期化します。 その後、 [*Iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチンが制御を返しただけの場合、ドライバーはデバイスのタイムアウト値に秒を追加します。

-   ドライバーの ISR は、このタイマーカウンターを1から引いた値に設定する必要があります。

-   ドライバーの[*Iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチンは1秒間に1回呼び出され、時間カウンターを読み取り、ISR で既にマイナス1に設定されているかどうかを確認します。 それ以外の場合、 *Iotimer*ルーチンは、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を使用して SynchCritSection\_1 ルーチンを呼び出すことによってカウンターをデクリメントします。

    カウンターがゼロに設定され、要求がタイムアウトしたことが示された場合、SynchCritSection\_1 ルーチンは SynchCritSection\_2 ルーチンを呼び出して、デバイスのリセット操作をプログラムします。 カウンターが1を引いた場合、 [*Iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチンは単にを返します。

-   部分転送操作を開始するために、ドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンがデバイスを再プログラミングする必要がある場合は、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンと同様にタイマーカウンターを再初期化する必要があります。

    また、 [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンは、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を使用して SynchCritSection\_2 ルーチンを呼び出すか、場合によっては SynchCritSection\_3 ルーチンを呼び出して、別の転送操作のためにデバイスをプログラミングする必要があります。

このシナリオでは、ドライバーに複数の*SynchCritSection*ルーチンがあり、それぞれに個別の責任があります。1つはタイマーカウンターを維持するためのもので、もう1つはデバイスをプログラミングするためのものです。 各*SynchCritSection*ルーチンは、単一の個別のタスクを実行するため、制御を迅速に返すことができます。

ドライバーには単一の SynchCritSection\_1 ルーチンがあり、ドライバーの ISR と共にタイマーカウンターの状態が維持されることに注意してください。 そのため、複数の*SynchCritSection*ルーチンと ISR 間でのタイマーカウンターへのアクセスに競合は発生しません。

 

 




