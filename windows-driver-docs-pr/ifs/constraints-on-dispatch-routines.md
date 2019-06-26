---
title: ディスパッチ ルーチンに関する制約
description: ディスパッチ ルーチンに関する制約
ms.assetid: 5b2acaea-1f66-4285-9a36-5ab0f440f6b4
keywords:
- IRP ディスパッチ ルーチン WDK ファイル システム、制約
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5b9455fe984eea1169ba8881da49342112ad911
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363536"
---
# <a name="constraints-on-dispatch-routines"></a>ディスパッチ ルーチンに関する制約


## <span id="ddk_constraints_on_dispatch_routines_if"></span><span id="DDK_CONSTRAINTS_ON_DISPATCH_ROUTINES_IF"></span>


次のガイドラインでは、ファイル システム フィルター ドライバーのディスパッチ ルーチン内での一般的なプログラミング エラーを回避する方法について簡単に説明します。

### <a name="span-idirql-relatedconstraintsspanspan-idirql-relatedconstraintsspanspan-idirql-relatedconstraintsspanirql-related-constraints"></a><span id="IRQL-Related_Constraints"></span><span id="irql-related_constraints"></span><span id="IRQL-RELATED_CONSTRAINTS"></span>IRQL 関連の制約

注:ページングの入出力の Irp の型の使用については、次を参照してください。[ディスパッチ日常的な IRQL とスレッド コンテキスト](dispatch-routine-irql-and-thread-context.md)します。

-   ページング I/O パスのディスパッチ ルーチンは呼び出さないで[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) APC 上の任意の IRQL で\_レベル。 ディスパッチ ルーチンでは、IRQL が発生した場合は、呼び出す前に下げることが必要があります**保留**します。

-   ページング パスが、読み取りと書き込みなどのディスパッチ ルーチンは、IRQL パッシブでが実行されている呼び出し元を必要とする、カーネル モード ルーチンに安全に呼び出すことはできません\_レベル。

-   ページング ファイル I/O パス内にあるディスパッチ ルーチンは、IRQL でが実行されている呼び出し元を必要とする、カーネル モード ルーチンに安全に呼び出すことはできません&lt;ディスパッチ\_レベル。

-   ページング I/O パスにないディスパッチ ルーチンは呼び出さないで[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)パッシブ上の任意の IRQL で\_レベル。 ディスパッチ ルーチンでは、IRQL が発生した場合は、呼び出す前に下げることが必要があります**保留**します。

### <a name="span-idconstraintsonprocessingirpsspanspan-idconstraintsonprocessingirpsspanspan-idconstraintsonprocessingirpsspanconstraints-on-processing-irps"></a><span id="Constraints_on_Processing_IRPs"></span><span id="constraints_on_processing_irps"></span><span id="CONSTRAINTS_ON_PROCESSING_IRPS"></span>Irp の処理に関する制約

-   IRP パラメーターは、すべてのユーザー領域のアドレスを含める場合は、使用されるようにこれら検証する必要があります。 詳細については、次を参照してください。[バッファー i/o エラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-buffered-i-o)します。

-   さらに、IRP に 64 ビット プラットフォームを 32 ビットのプラットフォームから送信された IOCTL または FSCTL バッファーが含まれている場合、バッファーの内容は thunked する必要があります。 詳細については、次を参照してください。 [、64 ビット ドライバーをサポートしている 32 ビットの I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-32-bit-i-o-in-your-64-bit-driver)します。

-   ファイル システムとは異なりファイル システム フィルター ドライバーは呼び出す必要がありますしない[ **FsRtlEnterFileSystem** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)または[ **FsRtlExitFileSystem** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)以外呼び出しの前に[ **ExAcquireFastMutexUnsafe** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544340(v=vs.85))または[ **ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)します。 **FsRtlEnterFileSystem**と**FsRtlExitFileSystem**ほとんどのファイル システムで必要な通常のカーネル Apc を無効にします。

### <a name="span-idconstraintsoncompletingirpsspanspan-idconstraintsoncompletingirpsspanspan-idconstraintsoncompletingirpsspanconstraints-on-completing-irps"></a><span id="Constraints_on_Completing_IRPs"></span><span id="constraints_on_completing_irps"></span><span id="CONSTRAINTS_ON_COMPLETING_IRPS"></span>Irp の完了の制約

-   Irp の完了時に、ファイル システム フィルター ドライバーは、唯一の成功とエラー状態の値を使用してください。

-   状態\_PENDING は成功 NTSTATUS 値、状態が IRP を完了すると、プログラミング エラー\_保留します。

-   ディスパッチ ルーチンの呼び出し後[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)、IRP ポインターが無効にし、安全に逆参照することはできません。

### <a name="span-idconstraintsonsettingacompletionroutinespanspan-idconstraintsonsettingacompletionroutinespanspan-idconstraintsonsettingacompletionroutinespanconstraints-on-setting-a-completion-routine"></a><span id="Constraints_on_Setting_a_Completion_Routine"></span><span id="constraints_on_setting_a_completion_routine"></span><span id="CONSTRAINTS_ON_SETTING_A_COMPLETION_ROUTINE"></span>設定完了ルーチンの制約

注:設定完了ルーチンの詳細については、次を参照してください。[完了ルーチンを使用して](using-irp-completion-routines.md)します。

-   ディスパッチ ルーチンを呼び出すと[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)、オプションで渡すことができる、*コンテキスト*完了ルーチン処理に使用する構造体へのポインター特定の IRP では。 この構造体は、IRQL ディスパッチ完了ルーチンを呼び出すことができますので、非ページ プールから割り当てる必要がある\_レベル。

-   ディスパッチ ルーチンが状態を返す可能性のある完了ルーチンを設定するかどうかは\_詳細\_処理\_必要に応じてが行う必要があります、I/O マネージャーが IRP の途中で完了するを防ぐために、次のいずれか。
    -   IRP が保留中の呼び出しをマーク[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)、状態を返すと\_保留します。
    -   呼び出す[ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)し、呼び出しを実行する完了ルーチンを待つ[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)を完了する、IRP します。

### <a name="span-idconstraintsonpassingirpsdownspanspan-idconstraintsonpassingirpsdownspanspan-idconstraintsonpassingirpsdownspanconstraints-on-passing-irps-down"></a><span id="Constraints_on_Passing_IRPs_Down"></span><span id="constraints_on_passing_irps_down"></span><span id="CONSTRAINTS_ON_PASSING_IRPS_DOWN"></span>制約を Irp を渡す方法

-   ディスパッチ ルーチンの呼び出し後[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)がそのため完了ルーチンのディスパッチ ルーチンが待機する場合を除き、IRP ポインターが無効にし、安全に逆参照することはできません呼び出されています。

-   呼び出すと、プログラミング エラー [ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) 、ファイル システム フィルター ドライバーから。 (**PoCallDriver** IRP を渡すために使用\_MJ\_下位レベルのドライバーに電源要求。 ファイル システム フィルター ドライバーは IRP を受信しない\_MJ\_POWER 要求します)。

### <a name="span-idconstraintsonreturningstatusspanspan-idconstraintsonreturningstatusspanspan-idconstraintsonreturningstatusspanconstraints-on-returning-status"></a><span id="Constraints_on_Returning_Status"></span><span id="constraints_on_returning_status"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS"></span>制約の状態を返す

-   ディスパッチ ルーチン完了ルーチンが設定されていないことがによって返される NTSTATUS 値を返す必要があります常に IRP を完了したときに点を除いて[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。 この値が状態でない限り\_、保留中の値に一致する必要があります**Irp -&gt;IoStatus.Status** IRP の完了したドライバーで設定します。

-   ときに[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)ステータスを返します\_保留中、ディスパッチ ルーチン返す必要がありますも状態\_PENDING、イベントを通知する完了ルーチンの待機している場合を除き、します。

-   ディスパッチ ルーチンが IRP の保留をマークし、状態を返す IRP が後で処理するためワーカー キューに投稿してきた、\_保留します。

-   ディスパッチ ルーチンする必要があります IRP が保留中のマークし、状態を返す完了ルーチンの設定を後で処理するためワーカー キューに IRP 可能性があります転記、\_保留します。

-   保留中の IRP をマークするディスパッチ ルーチンは、状態を返す必要があります\_保留します。

-   Oplock の操作は保留 (ワーカー キューにポストされた)、することはできず、ディスパッチ ルーチンは、状態を返すことはできません\_保留にします。

### <a name="span-idconstraintsonpostingirpstoaworkqueuespanspan-idconstraintsonpostingirpstoaworkqueuespanspan-idconstraintsonpostingirpstoaworkqueuespanconstraints-on-posting-irps-to-a-work-queue"></a><span id="Constraints_on_Posting_IRPs_to_a_Work_Queue"></span><span id="constraints_on_posting_irps_to_a_work_queue"></span><span id="CONSTRAINTS_ON_POSTING_IRPS_TO_A_WORK_QUEUE"></span>Irp の作業キューに投稿の制約

-   ディスパッチ ルーチンの Irp 作業キューに投稿する場合を呼び出す必要[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)各 IRP ワーカー キューに送信する前にします。 それ以外の場合、IRP でしたデキューされた別のドライバーのルーチンで完了し、呼び出しの前に、システムによって解放**IoMarkIrpPending**原因となり、クラッシュが発生します。

 

 




