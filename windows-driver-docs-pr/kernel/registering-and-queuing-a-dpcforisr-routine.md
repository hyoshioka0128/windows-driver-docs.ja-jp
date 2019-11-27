---
title: DpcForIsr ルーチンの登録とキュー
description: DpcForIsr ルーチンの登録とキュー
ms.assetid: 32253573-842e-40bc-9616-8d1ccd7afa29
keywords:
- DpcForIsr
- DpcForIsr ルーチンを登録しています
- DpcForIsr ルーチンをキューに置いています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4db9544d8015cec00c5860b83b1f19690e89907a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827503"
---
# <a name="registering-and-queuing-a-dpcforisr-routine"></a>DpcForIsr ルーチンの登録とキュー





ドライバーは、デバイスオブジェクトを作成した後に[**IoDpcForIsr Edpcrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializedpcrequest)を呼び出すことによって、デバイスオブジェクトに対して[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンを登録します。 ドライバーは、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンからこの呼び出しを行うことができます。または、 [ **\_デバイス要求を開始\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を処理する[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)コードから呼び出すこともできます。

*DpcForIsr*ルーチンの実行をキューに記録するために、ドライバーの ISR は、制御が戻る直前に[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)を呼び出します。 次の図は、これらのルーチンの呼び出しを示しています。

![dpcforisr ルーチンで dpc オブジェクトを使用する方法を示す図](images/3dpcisr.png)

前の図に示すように、 **IoDpcForIsr Edpcreクエスト**を呼び出すと、DPC オブジェクトとドライバーによって作成されたデバイスオブジェクトが関連付けられます。 I/o マネージャーは、DPC オブジェクトにメモリを割り当て、ドライバーの代わりに[**Keinitializer Edpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)を呼び出します。

DIRQL でデバイスの割り込みを処理するために ISR が呼び出された場合、システム全体のパフォーマンスを向上させるために、できるだけ早くシステムに制御を返す必要があります。 通常、ISR は割り込みをクリアするだけで、割り込みの原因となった操作を完了するために*DpcForIsr*ルーチンが必要とするすべてのコンテキスト情報を収集し、 [**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)を呼び出し、を返します。

ISR は**IoRequestDpc**を呼び出すと、デバイスオブジェクトへのポインター、 *DeviceObject* **-&gt;の**ポインター、およびドライバーによって決定されたコンテキストへのポインターを渡します。 I/o マネージャーは、ドライバーの代わりに[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)を呼び出し、DPC オブジェクトをキューに入れます。 IRQL がプロセッサのディスパッチ\_レベルを下回ると、カーネルは DPC オブジェクトをデキューし、そのプロセッサ上で*DpcForIsr*ルーチンを irql ディスパッチ\_レベルで実行します。

*DpcForIsr*ルーチンは、現在の IRP で要求された i/o を完了するために必要な処理を行います。 入力時、ルーチンは、DPC オブジェクトへのポインターと共に、ISR の**IoRequestDpc**への呼び出しで渡されたデバイスオブジェクト、IRP、およびコンテキスト領域へのポインターを受け取ります。 コンテキスト領域は、常駐メモリ内に存在する必要があり、通常はデバイスの拡張機能にあります。 または、ドライバーによって割り当てられた非ページプール内、またはドライバーが[コントローラーオブジェクト](using-controller-objects.md)を使用している場合はコントローラー拡張機能にもできます。

ISR ルーチンと*DpcForIsr*ルーチンは SMP コンピューターで同時に実行できるため、次のガイドラインに従う必要があります。

-   ISR は、制御を返す直前に**IoRequestDpc**を呼び出す必要があります。 それ以外の場合、 *DpcForIsr*ルーチンは、ISR が*DpcForIsr*ルーチンのコンテキスト領域の設定を完了する前に、別のプロセッサで実行される可能性があります。

-   *DpcForIsr*ルーチンと、ISR とコンテキスト領域を共有するその他のドライバールーチンは[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を呼び出す必要があります。これは、の共有コンテキスト領域にアクセスするドライバーによって提供される[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを指定します。マルチプロセッサ-セーフな方法。

-   ドライバーがデバイスの i/o 操作に関するコンテキストを維持するためにデバイス拡張機能を使用する場合、 *DpcForIsr*ルーチンは、入力デバイスオブジェクトに対して[**Iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出すことはできません (ドライバーがは、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出す直前まで、独自の IRP キューを管理します)。

    それ以外の場合、ドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) (またはキュー管理ルーチン) は、 *DpcForIsr*ルーチンが現在の操作を完了する前に、共有コンテキスト領域を上書きする別の i/o 操作を開始することがあります。 これは、 *DpcForIsr*ルーチンの実行中または実行前にデバイスが中断した場合 (割り込みがまだ有効になっている場合)、ISR を再度呼び出すことができるためです。

ユニプロセッサコンピューターでも、 *DpcForIsr*ルーチンの実行中または実行前にデバイスで割り込みが発生した場合に、ISR を再度呼び出すことができます。 この場合、 *DpcForIsr*ルーチンは1回だけ実行されます。 つまり、ドライバーがターゲットデバイスオブジェクトの i/o 操作と重複する場合、 **IoRequestDpc**への ISR 呼び出しと*DpcForIsr*ルーチンのインスタンス化の間に1対1の対応はありません。

 

 




