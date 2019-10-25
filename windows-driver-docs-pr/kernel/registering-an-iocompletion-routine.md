---
title: IoCompletion ルーチンの登録
description: IoCompletion ルーチンの登録
ms.assetid: 413d8463-b2ce-44b6-846c-f853b5cd580e
keywords:
- IoCompletion ルーチン
- IoCompletion ルーチンを登録しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a68722e5287668feab988b5a8abafa04b5a4a4c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838471"
---
# <a name="registering-an-iocompletion-routine"></a>IoCompletion ルーチンの登録





[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを登録するために、ディスパッチルーチンは[**iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出します。 *iocompletion*ルーチンのアドレスと、後で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して下位のドライバーに渡す IRP を渡します。

**Iosetcompletion ルーチン**を呼び出す場合、ディスパッチルーチンは、i/o マネージャーが指定された*iocompletion*ルーチンを呼び出す必要がある状況を指定します。 低いレベルのドライバーが IRP を正常に完了した場合 (*InvokeOnSuccess*)、エラー状態の値 (*invokeonerror*) を使用して irp を完了するか、irp をキャンセルする (InvokeOnCancel) 場合は、 *iocompletion*ルーチンを呼び出すことができます。)、任意の組み合わせ。

*Iocompletion*ルーチンの目的は、IRP で実行された下位レベルのドライバーを監視し、必要に応じて追加の完了処理を実行することです。 具体的には、ドライバーの*Iocompletion*ルーチンの最も一般的な用途は次のとおりです。

-   ドライバーが[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)または[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)を使用して割り当てた IRP を破棄するには

    これらのサポートルーチンのいずれかを使用して IRP を割り当てる上位レベルのドライバーは、その IRP の*Iocompletion*ルーチンを提供する必要があります。 *Iocompletion*ルーチンは[**Iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)を呼び出して、ドライバーによって割り当てられた irp を破棄する必要があります。

-   受信 IRP を再利用して、より低いドライバーが一部の操作 (部分的な転送など) を完了するように要求するには、 *Iocompletion*ルーチンによって元の要求が満たされて完了するまでの間、

-   下位のドライバーがエラーで完了したことを要求を再試行するには

    ファイルシステムなどの最上位レベルのドライバーは、厳密に結合されたポートドライバーの上に階層化されている場合を除き、中間ドライバーよりも要求の再試行を試みる*Iocompletion*ルーチンを持つ可能性が高くなります。 ただし、中間ドライバーでは、 *Iocompletion*ルーチンを使用して要求を再試行します。

最高レベルまたは中間ドライバーの[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 *iocompletion*ルーチンを必要とする irp を処理する可能性が最も高いものの、irp を下位のドライバーに渡すすべてのドライバーのディスパッチルーチンは、 *IoCompletion*ルーチン。

ドライバーによって割り当てられる Irp と再利用される Irp の場合、ディスパッチルーチンは、次のブール型パラメーターを使用して**Ioset補完ルーチン**を呼び出す必要があります。

-   *InvokeOnSuccess*が**TRUE**に設定される

-   *Invokeonerror*を**TRUE**に設定

-   *InvokeOnCancel*は、チェーン内の下位のドライバーがキャンセル可能な irp を処理する可能性がある場合に**TRUE**に設定されます。

    通常、 *InvokeOnCancel*が**TRUE**に設定されているかどうかに関係なく、状態\_がキャンセルされた irp が返されるかどうかにかかわらず、 *iocompletion*ルーチンが各ドライバー割り当ての IRP を解放するか、それぞれの完了状態を確認します。IRP を再利用します。

**Ioallocateirp**または[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)を使用して下位のドライバーの irp を割り当てるディスパッチルーチンでは、ドライバーによって割り当てられた各 IRP に*iocompletion*ルーチンを設定する必要があります。

-   ディスパッチルーチンは、使用する*Iocompletion*ルーチンに対して、元の irp とその割り当てられた irp の両方について状態を設定する必要があります。 少なくとも、 *Iocompletion*ルーチンは、元の irp と、割り当てられた追加の irp の数に対するアクセス権を必要とします。

-   ディスパッチルーチンは、割り当てられる IRP に対して、すべての*Invokeonxxx*パラメーターを**TRUE**に設定して**ioset補完ルーチン**を呼び出す必要があります。

一連の操作に対して Irp を再利用したり、i/o 操作を再試行したりするディスパッチルーチンは、再利用または再試行される各 IRP に対して**Iosetてルーチン**を呼び出す必要があります。

-   ディスパッチルーチンは、後で*Iocompletion*ルーチンが使用できるように、元の IRP の状態情報を保存する必要があります。

    たとえば、 [*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、その irp 内の次に低いドライバーの部分転送を設定する前に、 *iocompletion*ルーチンの入力 IRP の関連する転送パラメーターを保存する必要があります。 パラメーターの保存は、 *DispatchReadWrite*ルーチンによって、元の要求が満たされたときに*iocompletion*ルーチンが決定する必要があるパラメーターを変更する場合に特に重要です。

-   *Iocompletion*ルーチンが要求を再試行できる場合は、ディスパッチルーチンで、待機の回数の上限を設定する必要があります。これにより、最初の IRP がエラーで完了する前に、 *iocompletion*ルーチンが試行する再試行回数が制限されます。

-   IRP を再利用する場合、ディスパッチルーチンは、すべての*Invokeonxxx*パラメーターを**TRUE**に設定して**ioset補完ルーチン**を呼び出す必要があります。

-   非同期要求の場合、中間ドライバーのディスパッチルーチンは、元の IRP に対して[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出す必要があります。 その後、IRP を下位のドライバーに送信した後に、状態\_PENDING を返す必要があります。

 

 




