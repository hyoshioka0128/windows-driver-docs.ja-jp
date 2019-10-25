---
title: Irp をドライバースタックに渡す
description: Irp をドライバースタックに渡す
ms.assetid: 69d912c5-83cf-4651-b379-de6baea8ddd0
keywords:
- Irp WDK カーネル、スタックを渡す
- Irp をドライバースタック WDK に渡す
- Irp を転送するドライバースタック
- I/o スタックの場所 (WDK カーネル)
- スタックの場所 (WDK カーネル)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddfe0ef558fce7fc8f0b4d752600a87d919e2b26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838514"
---
# <a name="passing-irps-down-the-driver-stack"></a>Irp をドライバースタックに渡す





ドライバーのディスパッチルーチンが IRP を受信するときは、 [**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)を呼び出して、独自の i/o スタックの場所を確認し、パラメーターが有効であることを確認できるようにする必要があります。 ドライバーが要求を満たすことができない場合は、次のいずれかの操作を実行できます。

-   下位レベルのドライバーでさらに処理を行うには、IRP をに渡します。

-   1つまたは複数の新しい Irp を作成し、下位レベルのドライバーに渡します。

### <a name="a-higher-level-driver-should-pass-an-io-request-on-to-a-next-lower-driver-as-follows"></a>上位レベルのドライバーは、次のように、i/o 要求を次の下位のドライバーに渡す必要があります。

1.  ドライバーが入力 IRP を次の下位レベルのドライバーに渡す場合、ディスパッチルーチンでは、Ioskipによって、次の下位にあるドライバーの i/o スタックの[**場所を設定するために**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)、 [**ioskipを entiに**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)設定します。

    ドライバーが[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)を呼び出して下位のドライバーに対して1つまたは複数の追加の irp を割り当てる場合、ディスパッチルーチンは、「 [」の「irp の処理」で説明されている手順に従って、次の下位にあるドライバーの i/o スタックの場所を初期化する必要があります。中間レベルのドライバー](processing-irps-in-an-intermediate-level-driver.md)。

    ディスパッチルーチンは、特定の要求について、次に小さいドライバーの i/o スタックの場所にあるパラメーターの一部を変更できます。 たとえば、上位レベルのドライバーでは、基になるデバイスで転送容量に既知の制限がある場合に、大規模な転送要求のパラメーターが変更される可能性があります。また、IRP を再利用して、基になるデバイスドライバーに部分転送要求を送信します。

2.  [**Ioset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出します。

    ディスパッチルーチンが、受信した IRP を次の下位のドライバーに渡す場合は、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンの設定は省略可能です。ただし、ルーチンは、要求を完了するまでの間に、irp を再利用することにより、このようなタスクを実行できます。部分的な転送。 Irp を追跡し、エラーで返された要求を再試行する場合に、ドライバーが保持するすべての状態を更新します。

    ディスパッチルーチンによって新しい Irp が割り当てられている場合は、少ないドライバーが完了した後に各 IRP を解放する必要があるため、 *Iocompletion*ルーチンを設定する必要があります。

    *Iocompletion*ルーチンの詳細については、「 [irp の完了](completing-irps.md)」を参照してください。

3.  各 IRP で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、下位のドライバーによって処理されるようにします。

4.  次のように、適切な NTSTATUS 値を返します。
    -   状態\_保留中

        通常、このドライバーは、入力 IRP が非同期要求 ( [**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[**irp\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)など) の場合に、ステータス\_保留状態を返します。

    -   **IoCallDriver**の呼び出しの結果

        入力 IRP が同期要求 ( [**irp\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)など) の場合、ドライバーは**IoCallDriver**への呼び出しの結果を頻繁に返します。

### <a name="a-lowest-level-device-driver-passes-any-irp-that-it-cannot-complete-in-its-dispatch-routine-on-to-other-driver-routines-as-follows"></a>最下位レベルのデバイスドライバーは、ディスパッチルーチンで完了できない任意の IRP を、次のように他のドライバールーチンに渡します。

1.  入力 IRP で[**終了する Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)呼び出します。

2.  ドライバーによって管理される[Irp キュー](driver-managed-irp-queues.md)に関するページで説明されているように、ドライバーが独自の内部 IRP キューを管理する場合を除き、 [**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)を呼び出して Irp をドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンに渡すか、キューに入れます。

    ドライバーに*StartIo*ルーチンがなく、取り消し可能な irp を処理する場合は、[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを登録するか、[キャンセルセーフの irp キュー](cancel-safe-irp-queues.md)を実装する必要があります。 *キャンセル*ルーチンの詳細については、「 [irp の取り消し](canceling-irps.md)」を参照してください。

3.  ステータスを返す\_保留中です。

 

 




