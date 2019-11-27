---
title: ハードウェアの優先度の管理
description: ハードウェアの優先度の管理
ms.assetid: c27eb357-49d7-4f50-9554-643b70ca33dc
keywords:
- 条件の優先順位 WDK カーネル
- ハードウェアの優先順位 WDK カーネル
- IRQL レベル WDK カーネル
- WDK PASSIVE_LEVEL
- WDK APC_LEVEL
- WDK DISPATCH_LEVEL
- DIRQL WDK
- 割り込みサービスルーチン WDK カーネル、ハードウェアの優先順位
- Isr WDK カーネル、ハードウェアの優先順位
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 64d39f3d3cd4bffa7f5aaa049a83151285e7057e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838549"
---
# <a name="managing-hardware-priorities"></a>ハードウェアの優先度の管理





ドライバールーチンが実行される IRQL によって、どのカーネルモードドライバーが呼び出し可能なルーチンをサポートしているかが決まります。 たとえば、一部のドライバーサポートルーチンでは、呼び出し元が IRQL = DISPATCH\_レベルで実行されている必要があります。 呼び出し元がパッシブ\_レベルよりも高い IRQL で実行されている場合、他のユーザーは安全に呼び出すことができません。

最も一般的に実装されている標準ドライバールーチンが呼び出される IRQLs の一覧を次に示します。 IRQLs は、最も低い優先順位から順に表示されます。

<a href="" id="passive-level"></a>**パッシブ\_レベル**  
**割り込みマスクオフ**-なし。

**で呼び出されるドライバールーチン**パッシブ\_レベル— [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)、[*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチン、ほとんどのディスパッチルーチン、ドライバーで作成されたスレッド、ワーカースレッドのコールバック。

<a href="" id="apc-level"></a>**APC\_レベル**  
**割り込みマスクオフ**— APC\_レベルの割り込みはマスクされません。

**で呼び出されるドライバールーチン**APC\_レベル—ディスパッチルーチン (「[ディスパッチルーチン」と「IRQLs」を](dispatch-routines-and-irqls.md)参照)。

<a href="" id="dispatch-level"></a>**ディスパッチ\_レベル**  
**割り込みマスクオフ** —ディスパッチ\_レベルおよび APC\_レベルの割り込みはマスクされていません。 デバイス、クロック、電源障害の割り込みが発生する可能性があります。

**で呼び出されるドライバールーチン**ディスパッチ\_レベル— [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)、 [*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)、 [*AdapterListControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_list_control)、 [](https://msdn.microsoft.com/library/windows/hardware/ff542049)、 [*iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)、 [*cancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) (キャンセルスピンロックを保持している場合)、 [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)、 [*customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)、 [*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチン。

<a href="" id="dirql"></a>**DIRQL**  
**割り込みがマスク**されていない -すべての割り込みは、ドライバーの interrupt オブジェクトの IRQL&lt;= dirql にあります。 より高い DIRQL 値を持つデバイス割り込みは、クロックおよび電源障害の割り込みと共に発生する可能性があります。

DIRQL ( [*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine), [*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチン) で呼び出されるドライバールーチン。

APC\_レベルとパッシブ\_レベルの唯一の違いは、APC\_レベルで実行されているプロセスは、APC 割り込みを取得できないことです。 ただし、どちらの IRQLs もスレッドコンテキストを意味し、両方ともコードがページアウトできることを意味します。

最下位レベルのドライバーは、次の3つの IRQLs のいずれかで実行されている間、Irp を処理します。

-   ドライバーのディスパッチルーチンで、割り込みがプロセッサ上でマスクされていないパッシブ\_レベル

    **Driverentry**、 *AddDevice*、*再初期化*、および*アンロード*ルーチンも、ドライバーで作成されたシステムスレッドと同様に、パッシブ\_レベルで実行されます。

-   *StartIo*ルーチンでディスパッチ\_レベルと APC\_レベルの割り込みがプロセッサ上でマスクされている\_レベルをディスパッチします。

    *Adaptercontrol*、 *AdapterListControl*、*コントローラー制御*、 *iotimer*、 *cancel* (キャンセルスピンロックを保持しています)、および*customtimerdpc*ルーチンもディスパッチ\_レベルで実行されます *。DpcForIsr*および*customdpc*ルーチン。

-   ISR および*SynchCritSection*ルーチンで、プロセッサ上でマスクされているドライバーの interrupt オブジェクトの*SynchronizeIrql*以下のすべての割り込みを含むデバイスの IRQL (dirql)

最も上位レベルのドライバーは、次の2つの IRQLs のいずれかで実行されている間、Irp を処理します。

-   ドライバーのディスパッチルーチンで、割り込みがプロセッサ上でマスクされていないパッシブ\_レベル

    **Driverentry**、*再初期化*、 *AddDevice*、および*アンロード*ルーチンもパッシブ\_レベルで実行されます。これは、ドライバーによって作成されたシステムスレッドやワーカースレッドのコールバックルーチンやファイルシステムドライバーと同様です。

-   ディスパッチ\_レベルおよび APC\_レベルの割り込みがプロセッサ上でマスクされ、ドライバーの*Iocompletion*ルーチンによって\_レベルがディスパッチされます。

    *Iotimer*、 *Cancel*、および*CUSTOMTIMERDPC*ルーチンもディスパッチ\_レベルで実行されます。

状況によっては、大容量記憶装置の中間および最下位レベルのドライバーは、IRQL APC\_レベルで呼び出されます。 特に、この問題は、ファイルシステムドライバーが[**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)要求を下位のドライバーに送信するページフォールトで発生する可能性があります。

ほとんどの標準ドライバールーチンは、適切なサポートルーチンを呼び出すことができるようにする IRQL で実行されます。 たとえば、デバイスドライバーは、IRQL ディスパッチ\_レベルで実行されているときに、 [**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出す必要があります。 ほとんどのデバイスドライバーは*StartIo*ルーチンからこれらのルーチンを呼び出すため、通常はディスパッチ\_レベルで実行されています。

*StartIo*ルーチンを持たないデバイスドライバーは、irp の独自のキューを設定および管理するため、必ずしも**Allocateadapterchannel**を呼び出す必要がある場合にディスパッチ\_レベルの IRQL で実行されるわけではないことに注意してください。 このようなドライバーは、 [**Keraiseirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)と[**ke-irql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql) **の呼び出しの**間に**allocateadapterchannel**への呼び出しを入れ子にする必要があります。これにより、必要な irql が割り当てられます。ルーチンの回復制御を呼び出しています。

ドライバーサポートルーチンを呼び出すときは、次の点に注意してください。

- 現在の IRQL より小さい入力*NewIrql*値で[**Keraiseirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)を呼び出すと、致命的なエラーが発生します。 元の IRQL を復元する以外に[**Kelowerirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)を呼び出すと (つまり、 **Keraiseirql**を呼び出した後)、致命的なエラーが発生することもあります。

- IRQL &gt;= ディスパッチ\_レベルで実行しているときに、カーネル定義のディスパッチャーオブジェクトの[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)または[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)を呼び出して、0以外の時間待機すると致命的なエラーが発生します。

- イベント、セマフォ、ミューテックス、タイマーがシグナル状態に設定されるのを安全に待つことができるドライバールーチンは、ドライバーによって作成されたスレッド、 **Driverentry、driverentry**など、IRQL パッシブ\_レベルの任意のスレッドコンテキストで実行されるドライバールーチンだけです。*再初期化*ルーチン、または本質的に同期 i/o 操作 (ほとんどのデバイス i/o 制御要求など) のディスパッチルーチン。

- IRQL がパッシブ\_レベルで実行されている場合でも、ページング可能なドライバーコードでは、input *Wait*パラメーターを**TRUE**に設定して[**KeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)、 [**KeReleaseSemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasesemaphore)、または[**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)を呼び出すことはできません。 このような呼び出しでは、致命的なページフォールトが発生する可能性があります。

- IRQL が IRQL\_レベルを超えるルーチンでは、ページングプールからメモリを割り当てたり、ページプールのメモリに安全にアクセスしたりすることはできません。 APC\_レベルよりも大きい IRQL で実行されているルーチンが原因でページフォールトが発生した場合は、致命的なエラーになります。

- [**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)と[**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)を呼び出す場合、ドライバーは IRQL ディスパッチ\_レベルで実行されている必要があります。

  ドライバーは、 **KeAcquireSpinLock**を呼び出すときに、IRQL &lt;= ディスパッチ\_レベルで実行できますが、 **KeReleaseSpinLock**を呼び出すことによってそのスピンロックを解放する必要があります。 つまり、 **KeReleaseSpinLockFromDpcLevel**を呼び出すことによって、 **KeAcquireSpinLock**で取得したスピンロックを解放するプログラミングエラーになります。

  ドライバーは、 **KeAcquireSpinLockAtDpcLevel**、 **KeReleaseSpinLockFromDpcLevel**、 **KeAcquireSpinLock**、または**KERELEASESPINLOCK**を呼び出して、IRQL &gt; ディスパッチ\_レベルで実行する必要があります。

- スピンロックを使用するサポートルーチン ( **Exinterlocked ロック<em>Xxx</em>** ルーチンなど) を呼び出すと、呼び出し元が発生した irql でまだ実行されていない場合、\_レベルをディスパッチするために現在のプロセッサで IRQL が発生します。

- IRQL &gt; パッシブ\_レベルで実行されるドライバーコードは、できるだけ早く実行する必要があります。 ルーチンが実行される IRQL が高くなるほど、全体的なパフォーマンスが向上し、できるだけ早く実行するようにそのルーチンを調整することが重要になります。 たとえば、 **Keraiseirql**を呼び出すすべてのドライバーは、可能な限りすぐに**ke-irql**に対する相互呼び出しを行う必要があります。

優先順位の決定の詳細については、「[スケジュール、スレッドコンテキスト、および IRQL](https://go.microsoft.com/fwlink/p/?linkid=59757) 」ホワイトペーパーを参照してください。

 

 




