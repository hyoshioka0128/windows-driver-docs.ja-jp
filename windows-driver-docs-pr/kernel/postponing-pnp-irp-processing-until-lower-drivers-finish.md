---
title: 下位のドライバーが完了するまで PnP IRP 処理を延期する
description: 下位のドライバーが完了するまで PnP IRP 処理を延期する
ms.assetid: 5bd9f3aa-30d5-4c45-afec-3e5ae0264f4a
keywords:
- PnP WDK カーネル、IRP 処理の延期
- WDK カーネルをプラグアンドプレイし、IRP 処理を延期する
- Irp WDK PnP
- I/o 要求パケットの WDK PnP
- IRP 処理を延期する WDK PnP
- IRP 処理の遅延 WDK PnP
- DispatchPnP ルーチン
- IoCompletion ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48245dcd7d57681299e91b1ccc094592d062eea6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827656"
---
# <a name="postponing-pnp-irp-processing-until-lower-drivers-finish"></a>下位のドライバーが完了するまで PnP IRP 処理を延期する





一部の PnP および電源 Irp は、デバイスの親バスドライバーによって最初に処理される必要があります。その後、デバイススタック内の次の上位のドライバーごとに処理する必要があります。 たとえば、親バスドライバーは、デバイスに対して開始操作を実行する最初のドライバーである必要があります ([**IRP\_は、\_デバイス\_起動**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)します)。その後、次の上位の各ドライバーが続きます。 このような IRP では、関数とフィルタードライバーが i/o 完了ルーチンを設定し、次の下位のドライバーに IRP を渡し、より低いドライバーが IRP を終了するまで IRP を処理するすべてのアクティビティを延期する必要があります。

[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンは、irql ディスパッチ\_レベルで呼び出すことができますが、関数またはフィルタードライバーは、IRQL = パッシブ\_レベルで IRP を処理する必要がある場合があります。 *Iocompletion*ルーチンからパッシブ\_レベルに戻るには、ドライバーでカーネルイベントを使用できます。 ドライバーは、カーネルモードイベントを設定する*Iocompletion*ルーチンを登録した後、ドライバーが[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン内のイベントを待機します。 イベントが設定されると、下位のドライバーが IRP を完了し、ドライバーが IRP を処理できるようになります。

ドライバーでは、この方法を使用して、低いドライバーが電源 IRP ([**irp\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)) を完了するのを待機することはできないことに注意してください。 *Iocompletion*ルーチンで設定された[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでイベントを待機すると、デッドロックが発生する可能性があります。 詳細については、「[電源 irp の受け渡し](passing-power-irps.md)」を参照してください。

次の2つの図は、ドライバーが小さいドライバーが PnP IRP を完了するのを待機する方法の例を示しています。 この例では、関数とバスドライバーが実行する必要がある操作と、PnP マネージャーおよび i/o マネージャーとの対話方法を示します。

![プラグアンドプレイの irp 処理の延期を示す図、パート1](images/delay1.png)

次の注意事項は、前の図の丸で囲まれた数値に対応しています。

1.  PnP マネージャーは、i/o マネージャーを呼び出して、IRP をデバイススタック内の上位のドライバーに送信します。

2.  I/o マネージャーは、上位ドライバーの*DispatchPnP*ルーチンを呼び出します。 この例では、デバイススタックにドライバーが2つだけ (関数ドライバーと親バスドライバー)、関数ドライバーが上位ドライバーです。

3.  関数ドライバーは、カーネルモードイベントを宣言して初期化し、次に低いドライバーのスタック位置を設定して、この IRP の*Iocompletion*ルーチンを設定します。

    関数ドライバーは、 [**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を使用して、スタックの場所を設定できます。

    [**IosetInvokeOnSuccess ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)の呼び出しでは、関数ドライバーは、、 *Invokeonerror*、および*InvokeOnCancel*を**TRUE**に設定し、コンテキストパラメーターの一部としてカーネルモードイベントを渡します。

4.  関数ドライバーは、irp を処理する操作を実行する前に、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して irp をデバイススタックに渡します。

5.  I/o マネージャーは、そのドライバーの*DispatchPnP*ルーチンを呼び出すことによって、IRP をデバイススタック内の次の下位のドライバーに送信します。

6.  この例の次の下位のドライバーは、デバイススタック (親バスドライバー) の最下位のドライバーです。 バスドライバーは、デバイスを起動する操作を実行します。 バスドライバーは、 **irp&gt;iostatus. status**を設定し、この irp に関連する場合は**Irp&gt;Iostatus. 情報**を設定して、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して irp を完了します。

    バスドライバーが他のドライバールーチンを呼び出すか、デバイスを起動するために i/o を送信する場合、バスドライバーは*DispatchPnP*ルーチンの PnP IRP を完了しません。 代わりに、 *DispatchPnP*ルーチンから保留中の[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)と戻り\_状態を pending として保留中の IRP をマークする必要があります。 ドライバーは、後で別のドライバールーチンから**IoCompleteRequest**を呼び出します (DPC ルーチンもあります)。

次の図は、この例の2番目の部分を示しています。この例では、デバイススタック内の上位のドライバーが、延期された IRP 処理を再開します。

![プラグアンドプレイの irp 処理の延期を示す図、パート2](images/delay2.png)

次の注意事項は、前の図の丸で囲まれた数値に対応しています。

1.  バスドライバーが**IoCompleteRequest**を呼び出すと、i/o マネージャーは、上位のドライバーのスタックの場所を調べ、検出された*iocompletion*ルーチンを呼び出します。 この例では、i/o マネージャーが、次に上位にあるドライバー (関数ドライバー) の*Iocompletion*ルーチンを検索して呼び出します。

2.  関数ドライバーの*Iocompletion*ルーチンは、コンテキストパラメーターに指定されたカーネルモードイベントを設定し、必要な\_処理\_より多くのステータス\_を返します。

    この時点で、i/o マネージャーがより高いドライバーによって設定された*Iocompletion*ルーチンを呼び出さないようにするために、iocompletion ルーチンはステータス\_\_処理\_必要があります。 *Iocompletion*ルーチンは、この状態を使用して、ドライバーの*DispatchPnP*ルーチンが制御を再び forestall できるように完了します。 I/o マネージャーは、このドライバーの*DispatchPnP*ルーチンが irp を完了すると、この irp に対するより高いドライバーの*iocompletion*ルーチンの呼び出しを再開します。

3.  I/o マネージャーは、IRP の完了を停止し、 **IoCompleteRequest**を呼び出したルーチン (この例ではバスドライバーの*DispatchPnP*ルーチン) に制御を戻します。

4.  バスドライバーは、 *DispatchPnP*ルーチンから、IRP 処理の結果を示す状態を返します。これは、状態\_成功またはエラー状態のいずれかになります。

5.  **IoCallDriver**は制御を呼び出し元に返します。この例では、関数ドライバーの*DispatchPnP*ルーチンが使用されています。

6.  関数ドライバーの*DispatchPnP*ルーチンは、IRP の処理を再開します。

    **IoCallDriver**が PENDING\_を返した場合、 *DispatchPnP*ルーチンは、 *iocompletion*ルーチンが呼び出される前に実行を再開しました。 したがって、 *DispatchPnP*ルーチンは、 *iocompletion*ルーチンによってカーネルイベントが通知されるまで待機する必要があります。 これにより、 *DispatchPnP*ルーチンは、すべての下位ドライバーが完了するまで IRP の処理を続行しません。

    **Irp&gt;iostatus. status**がエラーに設定されている場合、下位のドライバーが irp に障害を発生させ、関数ドライバーが irp の処理を続行しないようにする必要があります (必要なクリーンアップを除く)。

7.  低いドライバーが IRP を正常に完了すると、関数ドライバーは IRP を処理します。

    親バスドライバーによって最初に処理される Irp の場合、バスドライバーは通常、 **irp&gt;iostatus. status**の正常な状態を設定し、必要に応じて、 **Irp&gt;Iostatus. 情報**の値を設定します。 関数ドライバーとフィルタードライバーは、IRP に障害が発生しない限り、 **Iostatus**の値をそのままにします。

    関数ドライバーの*DispatchPnP*ルーチンは、IRP を完了するために**IoCompleteRequest**を呼び出します。 I/o マネージャーは、i/o 完了処理を再開します。 この例では、関数ドライバーの上にフィルタードライバーがないため、を呼び出す*Iocompletion*ルーチンがありません。 **IoCompleteRequest**が Function driver *DispatchPnP*ルーチンに制御を返すと、 *DispatchPnP*ルーチンは status を返します。

一部の Irp では、関数またはフィルタードライバーがデバイススタックをバックアップする方法で IRP に失敗した場合、ドライバーが小さいことが PnP マネージャーによって通知されます。 たとえば、関数またはフィルタードライバーが、 [ **\_デバイスを起動\_、irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)失敗した場合、PnP マネージャーは、デバイススタックに[ **\_デバイスを削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)して、irp\_を送信します。

 

 




