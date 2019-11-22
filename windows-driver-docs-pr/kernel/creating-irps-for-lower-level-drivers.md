---
title: 下位レベル ドライバー用 IRP の作成
description: 下位レベル ドライバー用 IRP の作成
ms.assetid: 2d298eb1-6169-4742-80c1-200223a2d4fa
keywords:
- Irp WDK カーネル、作成
- 非同期要求 WDK Irp
- Irp WDK カーネル、非同期要求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aa74f00abe201aca3b6f0ad76f1c200c77bd02a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828448"
---
# <a name="creating-irps-for-lower-level-drivers"></a>下位レベル ドライバー用 IRP の作成





非同期要求に対して IRP を割り当てるには、それが下位のドライバーによって任意のスレッドコンテキストで処理されます。 [*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、次のいずれかのサポートルーチンを呼び出すことができます。

-   [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)。 IRP と、ゼロで初期化された多数の i/o スタックの場所を割り当てます。

    ディスパッチルーチンでは、新しく割り当てられた IRP に対して、次に下位のドライバーの i/o スタックの場所を設定する必要があります。通常は、元の IRP 内の独自のスタックの場所から情報をコピー (変更された可能性があります) します。 上位レベルのドライバーが新しく割り当てられた IRP 用に独自の i/o スタック位置を割り当てる場合、ディスパッチルーチンは、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが使用するために、要求ごとのコンテキスト情報を設定できます。

-   [**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)。呼び出し元が指定したパラメーターに従って、次の下位にあるドライバーの i/o スタック位置を呼び出し元に対して設定します。

    上位レベルのドライバーは、このルーチンを呼び出して、 [**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)、 [**irp\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)、 [**irp\_MJ\_FLUSH\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)buffer、および[**irp\_MJ の irp を割り当てることができ\_シャットダウン**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)要求。

    このような IRP に対して[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが呼び出されると、i/o 状態ブロックを確認し、必要に応じて (または可能な場合は) irp 内の次の下位にあるドライバーの i/o スタックの場所を再度設定して、要求を再試行するか再利用することができます。 ただし、 *Iocompletion*ルーチンには IRP 内のローカルコンテキストストレージがないため、ドライバーは、常駐メモリ内の別の場所にある元の要求に関するコンテキストを維持する必要があります。

-   [**IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp)。 irp と、ゼロで初期化されたゼロの i/o スタックの場所を割り当て、irp を*マスター* irp に関連付けます。

    中間ドライバーは、 [**IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp)を呼び出して、下位ドライバーの irp を作成することはできません。

    **IoMakeAssociatedIrp**を呼び出して下位のドライバーの irp を作成する最上位レベルのドライバーは、関連する irp をに送信した後で i/o マネージャーに制御を返し、元のマスター IRP に対して[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出すことができます。 最上位レベルのドライバーでは、すべての関連する Irp が下位のドライバーによって完了された場合に、マスタ IRP を完了するために i/o マネージャーを利用できます。

    ドライバーは、関連する IRP に対して[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンをほとんど設定しません。 最上位レベルのドライバーが、作成した関連する IRP に対して[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出すと、ドライバーがステータス\_返す場合、i/o マネージャーはマスタ IRP を完了しません。これは、その*iocompletion*ルーチンから必要な\_\_処理が行われます。 このような場合、ドライバーの*Iocompletion*ルーチンは、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を使用してマスターの IRP を明示的に完了する必要があります。

ドライバーが独自の i/o スタックの場所を新しい IRP に割り当てる場合、ディスパッチルーチンは[**Iogetfromtiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetnextirpstacklocation)ドの場所を呼び出して、 [**Iogetの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)[*完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンに対して独自の i/o スタックの場所にコンテキストを設定する必要があります。 詳細については、「[中間レベルのドライバーでの irp の処理](processing-irps-in-an-intermediate-level-driver.md)」を参照してください。

ディスパッチルーチンでは、元の IRP で[**終了する Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)呼び出す必要がありますが、 [*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンでは解放されるので、ドライバーで割り当てられた irp は使用できません。

ディスパッチルーチンが部分的な転送に対して Irp を割り当てていて、基になるデバイスドライバーがリムーバブルメディアデバイスを制御する可能性がある場合、ディスパッチルーチンは、新しく割り当てられた Irp 内のスレッドコンテキストを、元の IRP の**末尾**の値から設定する必要があります。

リムーバブルメディアデバイス用の基になるドライバーは、 [**IoSetHardErrorOrVerifyDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetharderrororverifydevice)を呼び出すことがあります。これは、ドライバーによって割り当てられた Irp の**Irp-&gt;Tail. オーバーレイ. Thread**でポインターを参照します。 ドライバーがこのサポートルーチンを呼び出すと、ファイルシステムドライバーは、適切なユーザースレッドにダイアログボックスを送信することができます。このスレッドは、ユーザーに対して、ドライバーが満たすことのできない操作をキャンセル、再試行、または失敗するように求めるメッセージを表示します。 詳細については、「[リムーバブルメディアのサポート](supporting-removable-media.md)」を参照してください。

ディスパッチルーチンは、ドライバーによって割り当てられたすべての Irp を下位のドライバーに送信した後に、状態\_を返す必要があります。

ドライバーの[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンでは、元の Irp の[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出す前に、 [**iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)でドライバーによって割り当てられたすべての irp を解放する必要があります。 元の IRP が完了すると、 *Iocompletion*ルーチンは、制御を返す前に、ドライバーで割り当てられたすべての irp を解放する必要があります。

上位レベルの各ドライバーは、ドライバーによって割り当てられた (再利用された) Irp を下位ドライバーに対して設定します。これにより、特定の要求が中間ドライバーからのものであるか、ファイルなどの他のソースから送信されたものであるかにかかわらず、基になるデバイスドライバーに問題でます。システムまたはユーザーモードアプリケーション。

最上位レベルのドライバーは、 [**IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp)を呼び出して irp を割り当て、下位のドライバーのチェーン用に設定できます。 I/o マネージャーは、関連するすべての Irp が完了したときに、元の irp を自動的に完了します。ただし、ドライバーが、元の IRP または割り当てられている関連する任意の Irp で[**Iosetcompleted ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出すことはありません。 ただし、最高レベルのドライバーでは、バッファー i/o 操作を要求する任意の IRP に関連する Irp を割り当てることはできません。

中間レベルのドライバーでは、 **IoMakeAssociatedIrp**を呼び出すことによって下位レベルのドライバーの irp を割り当てることはできません。 中間ドライバーが受信する IRP は、既に関連付けられている IRP である可能性があります。ドライバーは、このような irp に別の IRP を関連付けることはできません。

代わりに、中間ドライバーが下位のドライバーに対して Irp を作成する場合は、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)、 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)、 [**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)、または[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)を呼び出す必要があります。 ただし、 **IoBuildSynchronousFsdRequest**は、次の状況でのみ呼び出すことができます。

-   ドライバーによって作成されたスレッドが、読み取りまたは書き込み要求の Irp を構築するために使用します。このようなスレッドは、 **IoBuildSynchronousFsdRequest**に渡されたドライバー初期化*イベント*など、ディスパッチャーオブジェクト上の任意のスレッドコンテキストで待機することがあります。

-   初期化中またはアンロード中のシステムスレッドコンテキスト内

-   作成、フラッシュ、シャットダウン、閉じる、デバイス制御要求など、本質的に同期操作のための Irp を構築するには

ただし、ドライバーは**IoBuildDeviceIoControlRequest**を呼び出して、 **IoBuildSynchronousFsdRequest**よりもデバイス制御の irp を割り当てる可能性が高くなります。

 

 




