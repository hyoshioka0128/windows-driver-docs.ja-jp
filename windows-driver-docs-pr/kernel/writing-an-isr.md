---
title: ISR の記述
description: ISR の記述
ms.assetid: d696d683-e010-4a5c-ba2d-f536ab5f38b2
keywords:
- 割り込みサービスルーチン WDK カーネル、書き込み
- Isr WDK カーネル、書き込み
- Isr の作成
- 割り込みオブジェクト WDK カーネル、Isr の作成
- I/o WDK カーネル、割り込み
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6bb1969516ea13efeac7926399ed301cf724d76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835594"
---
# <a name="writing-an-isr"></a>ISR の記述





割り込みを生成する物理デバイスのドライバーには、少なくとも1つの割り込みサービスルーチン (ISR) が必要です。 ISR は、割り込みを解除するために、デバイスに適切な処理を行う必要があります。これは、デバイスの中断を阻止する場合もあります。 次に、状態を保存し、DPC をキューに格納して、ISR が実行されるよりも低い優先順位 (IRQL) で i/o 操作を完了するために必要な操作のみを行います。

ドライバーの ISR は、 *SynchronizeIrql*パラメーターによって[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)に指定されているように、システムによって割り当てられた*dirql*で、割り込みコンテキストで実行されます。

Isr は割り込み可能です。 システムによって割り当てられた DIRQL が高い別のデバイスでは、中断される可能性があります。また、システムの割り込みが発生する可能性がある場合は、いつでも発生する可能性があります。

システムが ISR を呼び出す前に、isr が別のプロセッサで同時に実行できないように、割り込みのスピンロックを取得します。 ISR が戻ると、スピンロックが解放されます。

ISR は比較的高い IRQL で実行されるため、現在のプロセッサ上で同等またはそれ以上の IRQL を持つ割り込みをマスクします。これにより、可能な限り迅速に制御が返されます。 さらに、DIRQL で ISR を実行すると、ISR が呼び出すことができる一連のサポートルーチンが制限されます。 詳細については、「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」を参照してください。

通常、ISR は次の一般的な手順を実行します。

-   割り込みの原因となったデバイスが ISR でサポートされていない場合、ISR は直ちに**FALSE**を返します。

-   それ以外の場合、ISR は必要に応じて割り込みをクリアし、必要なすべてのデバイスコンテキストを保存し、DPC をキューに置いて i/o 操作を低 IRQL で完了します。 詳細については[、「Dpc オブジェクトと dpc](dpc-objects-and-dpcs.md) 」を参照してください。 次に、ISR は**TRUE**を返す必要があります。

具体的には、デバイスの i/o 操作と重複しないドライバーでは、ISR は次の操作を実行する必要があります。

1.  割り込みが誤って検出されたかどうかを判断します。 その場合、中断されたデバイスの ISR がすぐに呼び出されるように、直ちに**FALSE**を返します。 それ以外の場合は、割り込み処理を続行します。

2.  必要に応じて、デバイスの中断を停止します。

3.  [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) (または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)) ルーチンが現在の操作の i/o 処理を完了するために必要なすべてのコンテキスト情報を収集します。

4.  このコンテキストは、 *DpcForIsr*または*customdpc*ルーチンにアクセスできる領域に格納します。通常は、現在の i/o 要求を処理する割り込みの原因となったターゲットデバイスオブジェクトのデバイス拡張機能に格納します。

    ドライバーが i/o 操作と重複する場合、コンテキスト情報には、DPC ルーチンが完了する必要がある未処理の要求の数と、DPC ルーチンが各要求を完了するために必要なコンテキストを含める必要があります。 DPC が実行される前に別の割り込みを処理するように ISR が呼び出された場合、DPC によってまだ完了していない要求について、保存されているコンテキストを上書きしないようにする必要があります。

5.  ドライバーに*DpcForIsr*ルーチンが含まれている場合は、現在の IRP、ターゲットデバイスオブジェクト、および保存されているコンテキストへのポインターを使用して[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)を呼び出します。 **IoRequestDpc**は、IRQL がプロセッサのディスパッチ\_レベルを下回るとすぐに実行されるように*DpcForIsr*ルーチンをキューに配置します。

    ドライバーに*Customdpc*ルーチンがある場合は、( *customdpc*ルーチンに関連付けられている) DPC オブジェクトへのポインターと、保存されているコンテキストへのポインターを使用して[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)を呼び出します。 *customdpc*ルーチンは、運用. 通常、ISR は、現在の IRP とターゲットデバイスオブジェクトへのポインターも渡します。 IRQL がプロセッサのディスパッチ\_レベルを下回るとすぐに*Customdpc*ルーチンが実行されます。

6.  デバイスが割り込みを生成したことを示す**場合は TRUE**を返します。

一般に、ISR は IRP を満たすための実際の i/o 処理を行いません。 代わりに、デバイスが中断されないようにし、必要な状態情報を設定して、ドライバーの*DpcForIsr*または*customdpc*をキューに入れて、デバイスの割り込みを引き起こしている現在の要求を満たすために必要な i/o 処理を実行します。

ISR は、可能な限り最短の間隔で DIRQL で実行する必要があります。 このガイドラインに従うことで、コンピューター内のすべてのデバイスに対する i/o スループットが向上します。これは、DIRQL で実行すると、システムにより低いまたは等しい IRQL 値が割り当てられているすべての割り込みがマスク解除されるためです。

ドライバーの割り込みオブジェクトの*SynchronizeIrql*は、 **ioconnectinterrupt**というドライバーによって実行される dirql を決定します。 詳細については、「[デバイスデータへのアクセスの同期](synchronizing-access-to-device-data.md)」を参照してください。

 

 




