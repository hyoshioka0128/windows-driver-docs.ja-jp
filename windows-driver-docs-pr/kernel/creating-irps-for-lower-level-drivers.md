---
title: 下位レベル ドライバー用 IRP の作成
description: 下位レベル ドライバー用 IRP の作成
ms.assetid: 2d298eb1-6169-4742-80c1-200223a2d4fa
keywords:
- Irp WDK のカーネルを作成します。
- WDK Irp の非同期要求
- Irp WDK カーネルでは、非同期の要求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65597f654cc496aa5b23dcb4d9c5df4dea7e11cc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377151"
---
# <a name="creating-irps-for-lower-level-drivers"></a>下位レベル ドライバー用 IRP の作成





IRP を低いドライバーによって任意のスレッド コンテキストで処理は、非同期の要求を割り当て、 [ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、次のサポート ルーチンのいずれかを呼び出すことができます。

-   [**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)IRP とゼロに初期化 I/O スタックの場所の番号を割り当てる

    ディスパッチ ルーチンは、IRP が元のスタックの場所は、独自の情報を (場合によっては変更) をコピーして通常新しく割り当てられた IRP では、次の下位ドライバーの I/O スタックの場所を設定する必要があります。 高度なドライバーが IRP を新しく割り当ての独自の I/O スタックの場所を割り当てた場合、ディスパッチ ルーチンは、要求あたりのコンテキスト情報がありますを設定できます、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンを使用するには.

-   [**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)、呼び出し元が、呼び出し元が指定したパラメーターに従って、次の下位ドライバーの I/O スタックの場所を設定します。

    高度なドライバーは Irp の割り当てにこのルーチンを呼び出すことができます[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)、 [ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)、 [ **IRP\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)、および[ **IRP\_MJ\_シャット ダウン**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)要求。

    ときに、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)このような IRP のルーチンを呼び出す、状態の I/O のブロックを確認できます、次の下位ドライバーの I/O を設定、必要に応じて (または可能な) IRP 内の場所をもう一度スタックを再試行して場合、要求またはそれを再利用します。 ただし、 *IoCompletion*ルーチンを持たないローカル コンテキストの記憶域自体の IRP のため、ドライバーがメモリ常駐で元の要求に関するコンテキストを他の場所で維持する必要があります。

-   [**IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iomakeassociatedirp)、IRP とゼロに初期化の I/O スタックの場所の番号を割り当てるし、で IRP を関連付けます、*マスター* IRP します。

    中間ドライバーを呼び出すことはできません[ **IoMakeAssociatedIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iomakeassociatedirp) Irp を下位のドライバーを作成します。

    呼び出す任意の最上位レベルのドライバー **IoMakeAssociatedIrp**下位のドライバーは、I/O マネージャーにコントロール関連付けられているその Irp を送信して、呼び出しの後に戻ることができますの Irp の作成に[ **IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)元の IRP をマスターします。 最上位レベルのドライバーは、下位のドライバーが完了した IRP Irp が関連付けられているすべての場合、マスターを完了する I/O マネージャーを使用できます。

    ドライバーのほとんどの設定、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)が関連付けられている IRP のルーチンです。 最上位レベルのドライバーを呼び出す場合[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)が作成されますが関連付けられている IRP の I/O マネージャーが完了しないマスター IRP、ドライバーは、状態を返す場合\_複数\_処理\_から必要なその*IoCompletion*ルーチン。 このような場合、ドライバーの*IoCompletion*ルーチンがでマスター IRP を明示的に完了する必要があります[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。

ディスパッチ ルーチンを呼び出す必要があります、ドライバーが IRP を新しい独自の I/O スタックの場所を割り当てた場合[ **IoSetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetnextirpstacklocation)を呼び出す前に[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)の I/O スタックの場所、独自のコンテキストを設定する、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン。 詳細については、次を参照してください。 [、中間レベルのドライバーでの処理の Irp](processing-irps-in-an-intermediate-level-driver.md)します。

ディスパッチ ルーチンを呼び出す必要があります[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)元の IRP がいずれかではなくため Irp のドライバーに割り当てられた、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンが解放されます。

ディスパッチ ルーチンにある値から、新しく割り当てられた Irp のスレッド コンテキストを設定する必要がありますディスパッチ ルーチンは部分的な転送の Irp の割り当てと、基になるデバイス ドライバーをリムーバブル メディア デバイスで制御できるよう、 **Tail.Overlay.Thread**元の IRP でします。

リムーバブル メディア デバイス用の基になるドライバーが呼び出す可能性があります[ **IoSetHardErrorOrVerifyDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iosetharderrororverifydevice)にあるポインターを参照する**Irp-&gt;Tail.Overlay.Thread**、ドライバーによって割り当てられた IRP の。 ドライバーは、このサポート ルーチンを呼び出し、ファイル システム ドライバーは、キャンセル、再試行、またはドライバーを満たしていませんでしたが、操作に失敗するよう求める適切なユーザーのスレッドに ダイアログ ボックスを送信できます。 参照してください[リムーバブル メディアをサポートしている](supporting-removable-media.md)詳細についてはします。

ディスパッチ ルーチンは、状態を返す必要があります\_下位のドライバーにすべてのドライバーに割り当てられた Irp の送信後に保留します。

ドライバーの[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンですべてのドライバーに割り当てられた Irp を解放する必要があります[ **IoFreeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)を呼び出す前に[**IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)元 IRP の。 元の IRP の完了時に、 *IoCompletion*ルーチンは、コントロールを返します前にすべてのドライバーに割り当てられた Irp に解放する必要があります。

各上位レベルのドライバーの方法ではないこと素材基になるデバイス ドライバーを特定の要求から中間のドライバーやファイルなど、他のソースからかどうかの下位のドライバーのドライバーに割り当てられた (および再利用) Irp を設定します。システムまたはユーザー モード アプリケーション。

最上位レベルのドライバーが呼び出せる[ **IoMakeAssociatedIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iomakeassociatedirp) Irp の割り当てし、下位のドライバーのチェーンにセットアップします。 I/O マネージャーによって自動的に実行元の IRP、関連付けられているすべての Irp が完了したら、ドライバーを呼び出さない限り、 [ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)元 IRP またはいずれか関連付けられている Irp が割り当てられます。 最上位レベルのドライバーする必要があります、ただしを割り当てられません Irp が関連付けられているバッファー内の I/O 操作を要求する任意の IRP します。

中間レベル、ドライバーは、下位レベルのドライバーの Irp を呼び出すことによって割り当てることができません**IoMakeAssociatedIrp**します。 中間のドライバーを受け取る任意の IRP が既に、関連付けられている IRP をして、ドライバーは IRP のもう 1 つをこのような IRP に関連付けることはできません。

代わりに、中間のドライバーでは、下位のドライバーの Irp を作成する場合に呼び出す必要があります[ **IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)、 [ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)、 [ **IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)、または[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)します。 ただし、 **IoBuildSynchronousFsdRequest**次の状況でのみ呼び出すことができます。

-   読み取りの Irp をビルドまたはこのようなスレッド内で待機できる nonarbitrary スレッド コンテキスト (専用) ため、要求を記述するドライバーが作成したスレッドによってドライバー初期化などのディスパッチャー オブジェクトで*イベント*に渡される**IoBuildSynchronousFsdRequest**

-   初期化中またはアンロード中にシステム スレッドのコンテキストで

-   Irp 本質的に同期操作をビルドするには、作成など、フラッシュ、シャット ダウン、close、およびコントロールとデバイスの要求

ただし、ドライバーが呼び出す可能性の高い**IoBuildDeviceIoControlRequest**デバイス制御 Irp を割り当てるよりも**IoBuildSynchronousFsdRequest**します。

 

 




