---
title: DpcForIsr ルーチンの登録とキュー
description: DpcForIsr ルーチンの登録とキュー
ms.assetid: 32253573-842e-40bc-9616-8d1ccd7afa29
keywords:
- DpcForIsr
- DpcForIsr ルーチンを登録します。
- キューの DpcForIsr ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bf2bcacfd7cb5fb5c282cfb99bb6482575a608e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377108"
---
# <a name="registering-and-queuing-a-dpcforisr-routine"></a>DpcForIsr ルーチンの登録とキュー





ドライバーの登録、 [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)呼び出すことでデバイス オブジェクトの日常的な[ **IoInitializeDpcRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializedpcrequest)作成後、デバイス オブジェクト。 ドライバーからには、この呼び出しを行うことができます、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチンまたは[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)を処理するコード[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。

キューに、 *DpcForIsr*ルーチンを実行するため、ドライバーの ISR 呼び出し[ **IoRequestDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)直前に返します。 次の図は、これらのルーチンへの呼び出しを示しています。

![dpcforisr ルーチンの dpc オブジェクトを使用して説明する図](images/3dpcisr.png)

前の図に示すように呼び出す**IoInitializeDpcRequest** DPC オブジェクトはドライバーによって提供される関連付けます*DpcForIsr*ルーチンとデバイスのドライバーが作成したオブジェクト。 I/O マネージャーでは、メモリを割り当て、DPC オブジェクトと呼び出しの[ **KeInitializeDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializedpc)ドライバーの代わりにします。

ISR は DIRQL でデバイスの割り込みを処理するために呼び出されるは、コントロールをできるだけ早くドライバーのパフォーマンス向上の全体的なシステムに関するシステムに戻ります。 通常は、ISR だけで、割り込みをクリアします、どのようなコンテキスト情報を収集、 *DpcForIsr*ルーチンを呼び出し、割り込みの原因となった操作を完了する必要があります[ **IoRequestDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)、しを返します。

ISR を呼び出すと**IoRequestDpc**、デバイス オブジェクトへのポインターにポインターを渡す、*デバイス オブジェクト*-&gt;**CurrentIrp**、およびドライバーにより決定されたコンテキストへのポインター。 I/O マネージャー呼び出し[ **KeInsertQueueDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc) DPC オブジェクトをキューが、ドライバーの代わりにします。 IRQL がディスパッチを下回ったとき\_レベル プロセッサでは、カーネルがデキュー DPC オブジェクトと、ドライバーの実行*DpcForIsr* IRQL のディスパッチには、そのプロセッサの日常的な\_レベル。

*DpcForIsr*ルーチンは、I/O の現在の IRP で要求を完了するために必要なものが責任を負います。 エントリのルーチンが ISR の呼び出しで渡されたが、デバイス オブジェクト、IRP、およびコンテキスト領域へのポインターと共に、DPC オブジェクトへのポインターを受け取る**IoRequestDpc**します。 コンテキストの領域は、メモリ常駐型である必要があり、、通常、デバイスの拡張機能で。 ドライバーで使用する場合、ドライバーによってまたはコント ローラーの拡張機能を割り当てられた非ページ プールを指定できますも、[コント ローラー オブジェクト](using-controller-objects.md)します。

ISR と*DpcForIsr*ルーチンは、SMP コンピューターで同時に実行できる、これらのガイドラインに従う必要があります。

-   呼び出す必要があります、ISR **IoRequestDpc**直前にコントロールを返します。 それ以外の場合、 *DpcForIsr*ルーチンは ISR がコンテキストの領域を設定を完了する前に、別のプロセッサで実行する可能性があります、 *DpcForIsr*ルーチン。

-   *DpcForIsr*ルーチンと ISR とコンテキストの領域を共有する他のドライバー ルーチンを呼び出す必要があります[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)、ドライバーによって提供されるを指定します。[*SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチンをマルチプロセッサ セーフ方式での共有コンテキストの領域にアクセスします。

-   ドライバーは、そのデバイスの I/O 操作に関するコンテキストを維持するために、デバイスの拡張機能を使用している場合、 *DpcForIsr*ルーチンは呼び出さないで[**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)入力デバイス オブジェクト (もドライバーは、独自の IRP キューが管理する場合、入力デバイス オブジェクトの IRP のデキュー) を呼び出す前に、単になるまで[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。

    それ以外の場合、ドライバーの[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio) (またはキュー管理ルーチン) する前に、共有コンテキストの領域を上書きする別の I/O 操作を開始する可能性があります、 *DpcForIsr*ルーチンは、現在の操作を完了できます。 これは、中、または前に、デバイスが中断している場合、ISR をもう一度呼び出すことがあるため、 *DpcForIsr*ルーチンを実行します (割り込みがまだ有効になっていると仮定)。

単一プロセッサのコンピューター上でも ISR だった場合に呼び出されるもう一度デバイスの中断中に、または前に、 *DpcForIsr*ルーチンを実行します。 このような場合、 *DpcForIsr*ルーチンを 1 回だけ実行します。 つまりは 1 対 1 対応 ISR の呼び出しの間で**IoRequestDpc**のインスタンス化し、 *DpcForIsr*重なっている場合、ターゲット デバイスの I/O 操作は、ドライバーのルーチンオブジェクト。

 

 




