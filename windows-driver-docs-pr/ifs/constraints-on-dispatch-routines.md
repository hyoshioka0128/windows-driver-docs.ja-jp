---
title: ディスパッチ ルーチンに関する制約
description: ディスパッチ ルーチンに関する制約
ms.assetid: 5b2acaea-1f66-4285-9a36-5ab0f440f6b4
keywords:
- IRP ディスパッチルーチン WDK ファイルシステム、制約
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f66b0157403f9e202d983ca929f7cf9f86fa59bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841454"
---
# <a name="constraints-on-dispatch-routines"></a>ディスパッチ ルーチンに関する制約


## <span id="ddk_constraints_on_dispatch_routines_if"></span><span id="DDK_CONSTRAINTS_ON_DISPATCH_ROUTINES_IF"></span>


次のガイドラインでは、ファイルシステムフィルタードライバーのディスパッチルーチンでの一般的なプログラミングエラーを回避する方法について簡単に説明します。

### <a name="span-idirql-related_constraintsspanspan-idirql-related_constraintsspanspan-idirql-related_constraintsspanirql-related-constraints"></a><span id="IRQL-Related_Constraints"></span><span id="irql-related_constraints"></span><span id="IRQL-RELATED_CONSTRAINTS"></span>IRQL に関連する制約

注: ページング i/o で使用される Irp の種類の詳細については、「[ディスパッチルーチンの IRQL とスレッドコンテキスト](dispatch-routine-irql-and-thread-context.md)」を参照してください。

-   ページング i/o パスのディスパッチルーチンでは、APC\_レベルより上の IRQL で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すことはできません。 ディスパッチルーチンが IRQL を発生させる場合は、 **IoCallDriver**を呼び出す前にディスパッチルーチンの値を小さくする必要があります。

-   読み取りや書き込みなどのページングパスにあるディスパッチルーチンは、呼び出し元\_を必要とするカーネルモードルーチンを安全に呼び出すことができません。

-   ページングファイル i/o パスにあるディスパッチルーチンでは、呼び出し元が実行されている必要のあるカーネルモードルーチンを安全に呼び出すことができません。そのためには、IRQL &lt; ディスパッチ\_レベルを使用します。

-   ページング i/o パスにないディスパッチルーチンは、パッシブ\_レベル上の IRQL で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すことはできません。 ディスパッチルーチンが IRQL を発生させる場合は、 **IoCallDriver**を呼び出す前にディスパッチルーチンの値を小さくする必要があります。

### <a name="span-idconstraints_on_processing_irpsspanspan-idconstraints_on_processing_irpsspanspan-idconstraints_on_processing_irpsspanconstraints-on-processing-irps"></a><span id="Constraints_on_Processing_IRPs"></span><span id="constraints_on_processing_irps"></span><span id="CONSTRAINTS_ON_PROCESSING_IRPS"></span>処理の Irp に対する制約

-   IRP パラメーターにユーザー領域のアドレスが含まれている場合は、それらを使用する前に検証する必要があります。 詳細については、「バッファリングされた[i/o のエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-buffered-i-o)」を参照してください。

-   さらに、IRP に32ビットプラットフォームから64ビットプラットフォームに送信された IOCTL または FSCTL バッファーが含まれている場合は、バッファーの内容を thunked にする必要がある場合があります。 詳細については、「 [64 ビットドライバーでの32ビット i/o のサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-32-bit-i-o-in-your-64-bit-driver)」を参照してください。

-   ファイルシステムとは異なり、ファイルシステムフィルタードライバーは、 [**ExAcquireFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544340(v=vs.85))または[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)を呼び出す前を除き、 [**fsrtlenterfilesystem**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)または[**fsrtlenterfilesystem**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)を呼び出すことはできません。 **Fsrtlenterfilesystem**および**Fsrtlenterfilesystem**は、ほとんどのファイルシステムで必要とされる通常のカーネル apc を無効にします。

### <a name="span-idconstraints_on_completing_irpsspanspan-idconstraints_on_completing_irpsspanspan-idconstraints_on_completing_irpsspanconstraints-on-completing-irps"></a><span id="Constraints_on_Completing_IRPs"></span><span id="constraints_on_completing_irps"></span><span id="CONSTRAINTS_ON_COMPLETING_IRPS"></span>Irp の完了に関する制約

-   Irp を完了する場合、ファイルシステムフィルタードライバーは成功とエラーの状態の値のみを使用する必要があります。

-   STATUS\_PENDING は成功した NTSTATUS 値ですが、状態\_保留中の IRP を完了するには、プログラミングエラーになります。

-   ディスパッチルーチンが[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出すと、IRP ポインターは無効になり、安全に逆参照できなくなります。

### <a name="span-idconstraints_on_setting_a_completion_routinespanspan-idconstraints_on_setting_a_completion_routinespanspan-idconstraints_on_setting_a_completion_routinespanconstraints-on-setting-a-completion-routine"></a><span id="Constraints_on_Setting_a_Completion_Routine"></span><span id="constraints_on_setting_a_completion_routine"></span><span id="CONSTRAINTS_ON_SETTING_A_COMPLETION_ROUTINE"></span>完了ルーチンの設定に関する制約

注: 完了ルーチンの設定の詳細については、「[完了ルーチンの使用](using-irp-completion-routines.md)」を参照してください。

-   ディスパッチルーチンが[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出す場合、必要に応じて、指定された IRP を処理するときに使用する完了ルーチンの構造体に*コンテキスト*ポインターを渡すことができます。 完了ルーチンを IRQL ディスパッチ\_レベルと呼び出すことができるため、この構造体を非ページプールから割り当てる必要があります。

-   ディスパッチルーチンによって、\_状態を返す可能性のある完了ルーチンが設定されている場合は\_処理\_必要があります。 i/o マネージャーが IRP を途中で完了しないようにするには、次のいずれかを行う必要があります。
    -   IRP を pending としてマークし、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出し、状態を返す\_保留中にします。
    -   [**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出して、完了ルーチンの実行を待機してから、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して IRP を完了します。

### <a name="span-idconstraints_on_passing_irps_downspanspan-idconstraints_on_passing_irps_downspanspan-idconstraints_on_passing_irps_downspanconstraints-on-passing-irps-down"></a><span id="Constraints_on_Passing_IRPs_Down"></span><span id="constraints_on_passing_irps_down"></span><span id="CONSTRAINTS_ON_PASSING_IRPS_DOWN"></span>Irp を渡すときの制約

-   ディスパッチルーチンが[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すと、IRP ポインターは無効になり、安全に逆参照できなくなります。ただし、ディスパッチルーチンが、呼び出しが完了したことを通知するために完了ルーチンが待機する場合を除きます。

-   ファイルシステムフィルタードライバーから[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を呼び出すと、プログラミングエラーになります。 (**Pocalldriver**は、IRP\_MJ\_の電源要求を下位レベルのドライバーに渡すために使用されます。 ファイルシステムフィルタードライバーは、IRP\_MJ\_の電源要求を受信することはありません)。

### <a name="span-idconstraints_on_returning_statusspanspan-idconstraints_on_returning_statusspanspan-idconstraints_on_returning_statusspanconstraints-on-returning-status"></a><span id="Constraints_on_Returning_Status"></span><span id="constraints_on_returning_status"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS"></span>ステータスを返す場合の制約

-   IRP を完了する場合を除き、完了ルーチンを設定しないディスパッチルーチンは、常に[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)から返された NTSTATUS 値を返す必要があります。 この値が [\_保留中] の場合を除き、irp を完了したドライバーによって設定された**irp&gt;IoStatus. status**の値と一致する必要があります。

-   [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)が\_pending を返した場合、ディスパッチルーチンは、完了ルーチンがイベントを通知するまで待機しない限り、状態\_pending を返す必要があります。

-   後で処理するために IRP をワーカーキューにポストする場合、ディスパッチルーチンは、IRP pending および return STATUS\_PENDING としてマークする必要があります。

-   後で処理するために IRP をワーカーキューに post する可能性のある完了ルーチンを設定する場合、ディスパッチルーチンは、IRP pending および return STATUS\_PENDING とマークする必要があります。

-   保留中の IRP をマークするディスパッチルーチンは、状態\_PENDING を返す必要があります。

-   Oplock 操作を保留 (worker キューに投稿) することはできません。また、ディスパッチルーチンは、保留中のステータス\_を返すことはできません。

### <a name="span-idconstraints_on_posting_irps_to_a_work_queuespanspan-idconstraints_on_posting_irps_to_a_work_queuespanspan-idconstraints_on_posting_irps_to_a_work_queuespanconstraints-on-posting-irps-to-a-work-queue"></a><span id="Constraints_on_Posting_IRPs_to_a_Work_Queue"></span><span id="constraints_on_posting_irps_to_a_work_queue"></span><span id="CONSTRAINTS_ON_POSTING_IRPS_TO_A_WORK_QUEUE"></span>Irp を作業キューに投稿する際の制約

-   ディスパッチルーチンが Irp を作業キューにポストする場合は、各 IRP をワーカーキューにポストする前に、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出す必要があります。 それ以外の場合は、IRP をデキューして別のドライバールーチンによって完了し、 **Iomarkirppending**の呼び出しが発生する前にシステムによって解放され、クラッシュが発生する可能性があります。

 

 




