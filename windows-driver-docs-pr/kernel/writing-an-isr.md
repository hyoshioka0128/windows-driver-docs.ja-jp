---
title: ISR の記述
description: ISR の記述
ms.assetid: d696d683-e010-4a5c-ba2d-f536ab5f38b2
keywords:
- 割り込みサービス ルーチン WDK カーネル、書き込み
- Isr WDK カーネル、書き込み
- isr を特定の書き込み
- 割り込みオブジェクト WDK カーネルは、isr を特定の書き込み
- I/O WDK カーネル、割り込み
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c3ec61d40e98171f5b0b173404b40d03dfec79e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574739"
---
# <a name="writing-an-isr"></a>ISR の記述





割り込みを発生の物理デバイスのドライバーには、少なくとも 1 つの割り込みサービス ルーチン (ISR) 必要があります。 中断することからデバイスの停止を含めることも、割り込みを消去するデバイスに適した ISR が行う必要があります。 次に、状態を保存し、キュー、DPC ISR が実行されるよりも低い優先順位 (IRQL) での I/O 操作を完了に必要なだけが行う必要があります。

ドライバーの ISR が割り込みコンテキストでは、システムによって割り当てられたいくつか実行*DIRQL*で指定されたとおり、 *SynchronizeIrql*パラメーターを[ **IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378).

Isr は、中断可能です。 以上のシステムによって割り当てられた DIRQL で別のデバイスを中断できる、または、いつでも高 IRQL システムの割り込みが発生します。

システムでは、ISR を呼び出し、前に、ISR は別のプロセッサで同時に実行できないために、割り込みのスピン ロックを取得します。 ISR を返した後、システムは、スピン ロックを解放します。

ISR が比較的高い IRQL、現在のプロセッサ上のと同じまたは低い IRQL と割り込みを隠してで実行されるため、できるだけ早く制御を戻すする必要があります。 さらに、ISR を DIRQL で実行されている ISR を呼び出すことができますサポート ルーチンのセットを制限します。 詳細については、[を管理するハードウェアの優先順位](managing-hardware-priorities.md)を参照してください。

通常は、ISR は、次の一般的な手順を実行します。

-   割り込みの原因となったデバイスがないかどうかの ISR によってサポートされる 1 つ、ISR を直ちに返し**FALSE**します。

-   それ以外の場合、ISR クリア割り込み必要に応じて、どのようなデバイス コンテキストは、必要に応じてと低い IRQL で I/O 操作を完了する DPC キューを保存します。 参照してください[DPC オブジェクトと Dpc](dpc-objects-and-dpcs.md)詳細についてはします。 ISR が返す必要がありますし、 **TRUE**します。

具体的には、デバイスの I/O 操作が重複しないドライバーの ISR は次の方法する必要があります。

1.  割り込みを誤ったかどうかを確認します。 そうである場合は、返す**FALSE**を中断したデバイスの ISR を速やかにというされますのですぐにします。 それ以外の場合、割り込み処理を続行します。

2.  必要な場合は、中断して、デバイスを停止します。

3.  どのようなコンテキスト情報を収集、 [ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079) (または[ *CustomDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542972)) ルーチンが I/O の処理を完了する必要があります、現在の操作。

4.  このコンテキストを格納領域にアクセスできる、 *DpcForIsr*または*CustomDpc*の原因と現在の I/O 要求を処理する対象のデバイス オブジェクトのデバイスの拡張機能では、通常、日常的な中断します。

    ドライバーには、I/O 操作が重なっている場合、コンテキスト情報は、DPC ルーチンがどのようなコンテキストと共に、各要求を完了する DPC ルーチンのニーズを完了するために必要な未処理の要求の数を含める必要があります。 ISR は、DPC が実行する前に、別の割り込みを処理するために呼び出されると、DPC が完了されていない要求の保存されたコンテキストを上書きする必要があります。

5.  ドライバーがある場合、 *DpcForIsr* 、ルーチンの呼び出し[ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657) IRP が現在、ターゲット デバイス オブジェクト、および保存されたコンテキストへのポインター。 **IoRequestDpc**キュー、 *DpcForIsr*ディスパッチ IRQL を下回ると、すぐに実行するルーチン\_プロセッサのレベル。

    ドライバーがある場合、 *CustomDpc* 、ルーチンの呼び出し[ **KeInsertQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552185) DPC オブジェクトへのポインターを (に関連付けられている、 *CustomDpc*ルーチン) と int、保存されたコンテキストへのポインター、 *CustomDpc*ルーチンは、操作を完了する必要があります。 通常、この ISR はまた、ポインターを現在の IRP と対象のデバイス オブジェクトを渡します。 *CustomDpc*ディスパッチ IRQL を下回ると、すぐルーチンが実行\_プロセッサのレベル。

6.  返す**TRUE**をそのデバイスに割り込みが生成されることを示します。

一般には、ISR は IRP を満たすために実際の I/O 処理は行われません。 中断することから、そのデバイスを停止する、必要な状態の情報を設定し、キュー、ドライバーの代わりに、 *DpcForIsr*または*CustomDpc*現在を満たすために必要な I/O 処理を行うデバイスを中断する原因となった要求。

ISR は、考えられる最短の間隔の DIRQL で実行する必要があります。 このガイドラインに従うと、システムによる小さいまたは等しい IRQL の値が割り当てられているすべての割り込みを DIRQL マスクで実行されているマシンのすべてのデバイスの I/O スループットが向上します。

*SynchronizeIrql*の割り込みのオブジェクト、指定されたドライバーが呼び出されたときに**IoConnectInterrupt**ドライバーの ISR が実行される DIRQL を決定します。 詳細については、[デバイス データへのアクセスの同期](synchronizing-access-to-device-data.md)を参照してください。

 

 




