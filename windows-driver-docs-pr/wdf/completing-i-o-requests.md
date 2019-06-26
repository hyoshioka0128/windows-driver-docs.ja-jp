---
title: I/O 要求の完了
description: I/O 要求の完了
ms.assetid: ec5aef7a-110e-430c-902d-669ccc7095ac
keywords:
- I/O 要求の完了の WDK KMDF
- WDK KMDF を要求する I/O の完了
- 要求の WDK KMDF、要求の完了を処理します。
- WDK KMDF、I/O 要求の完了の状態情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61160b7a8e251f0fa8f7fad6ed2c091cfb6edd67
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382879"
---
# <a name="completing-io-requests"></a>I/O 要求の完了





フレームワーク ベースのすべてのドライバーでは、フレームワークから受信したすべての I/O 要求が完了最終的にする必要があります。 ドライバーを呼び出して、要求オブジェクトの要求を完了する[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)メソッド。

### <a name="when-to-complete-a-request"></a>要求を完了するタイミング

ドライバーは、次のいずれかが true であると判断した場合、要求を完了する必要があります。

-   要求された I/O 操作は正常に完了しました。

-   要求された I/O 操作が開始したが、完了する前に失敗しました。

-   要求された I/O 操作では、サポートされていないか、開始できませんでしたし、受信した時点で有効でなかった。

-   要求された I/O 操作が取り消されました。

ドライバーが通常呼び出す場合は、ドライバーは、デバイスの I/O アクティビティを作成して、I/O 要求をサービス、 [ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)からその[ *EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数。

通常呼び出す場合は、ドライバーは、サポートされていないか、それ以外の場合に無効な要求を受け取る、 [ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)から、[要求ハンドラー](request-handlers.md)が要求を受信します。

I/O 操作があった場合[キャンセル](canceling-i-o-requests.md)、ドライバーは[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)からその[ *EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数。

場合、ドライバー[転送](forwarding-i-o-requests.md)I/O 要求を[I/O ターゲット](using-i-o-targets.md)ドライバーは、I/O ターゲットは次のように、要求を完了後に、要求を完了します。

-   ドライバーは、I/O 要求を転送する場合[同期的に](sending-i-o-requests-synchronously.md)下位レベルのドライバーは、(ない場合、エラーが発生します)、要求が完了した後にのみ、I/O ターゲットに I/O ターゲットへのドライバーの呼び出しを返します。 I/O ターゲットを返した後、ドライバーを呼び出す必要があります[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)します。

-   ドライバーは、I/O 要求を転送する場合[非同期的に](sending-i-o-requests-asynchronously.md)、ドライバーを下位レベルのドライバー、要求を完了するときに通知します。 場合は、ドライバーは、登録、 [ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数では、フレームワークからこのコールバック関数 I/O ターゲットが、要求を完了後します。 *CompletionRoutine*コールバック関数を呼び出す通常[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)します。

登録する、 [ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数では、ドライバーを呼び出す必要があります[ **WdfRequestSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)前にI/O のターゲットに I/O 要求を転送します。

登録するドライバーがない場合は、ドライバーは、I/O ターゲットを非同期的に転送された I/O 要求を完了するときに通知する必要はありません、 [ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数。 ドライバーを代わりに、設定することができます、 [ **WDF\_要求\_送信\_オプション\_送信\_AND\_破棄**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags)場合にフラグを設定呼び出す[ **WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)します。 この場合、ドライバーは呼び出しません[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)します。

ドライバーが呼び出すことで作成した I/O 要求が完了しない[ **WdfRequestCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)または[ **WdfRequestCreateFromIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)します。 代わりに、ドライバーを呼び出す必要があります[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete) I/O をターゲットには、要求が完了した後、通常、要求オブジェクトを削除します。

たとえば、ドライバーは、読み取りを受け取ることがあります。 またはをドライバーの I/O ターゲットを超えるデータ量の書き込み要求を同時に処理できます。 ドライバーは、いくつかの小さな要求にデータを分割し、1 つまたは複数の I/O ターゲットにこれらの小さい要求を送信する必要があります。 このような状況を処理するための手法は次のとおりです。

-   呼び出す[ **WdfRequestCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)小さな要求を表す 1 つの追加要求オブジェクトを作成します。

    ドライバーでは、I/O のターゲットに、この要求を同期的に送信できます。 小さな要求の[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数を呼び出すことができます[ **WdfRequestReuse** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestreuse)ドライバーを再利用できるように、要求し、もう一度 I/O ターゲットに送信します。 I/O ターゲットが小規模の要求の最後のタスクが完了したら、 *CompletionRoutine*コールバック関数を呼び出すことができます[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)ドライバー作成を削除するには要求オブジェクトと、ドライバーが呼び出せる[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)元の要求を完了します。

-   呼び出す[ **WdfRequestCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)小さな要求を表すいくつかの追加の要求オブジェクトを作成します。

    ドライバーの I/O のターゲットは、これら複数の小さい要求を非同期的に処理できます。 ドライバーが登録できる、 [ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)小さな要求ごとのコールバック関数。 ごとに、 *CompletionRoutine*コールバック関数が呼び出されると、呼び出すことができます[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)ドライバーが作成した要求オブジェクトを削除します。 I/O のターゲットには、すべての小さい要求が完了すると、ドライバーを呼び出すことが[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)元の要求を完了します。

### <a href="" id="providing-completion-information"></a> 完了の情報を提供します。

ドライバーには、要求が完了すると、その他のドライバーにアクセスできる追加情報も提供できます。 たとえば、ドライバーは、読み取りまたは書き込み要求の転送されたバイト数を提供する可能性があります。 この情報を提供するには、ドライバーは、次のいずれかで実行できます。

-   呼び出す[ **WdfRequestSetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetinformation)呼び出す前に[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)します。

-   呼び出す[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)します。

### <a href="" id="obtaining-completion-information"></a> 完了の情報を取得します。

別のドライバーが完了する I/O 要求に関する情報を取得するには、ドライバーでは次のことができます。

-   呼び出す[ **WdfRequestGetStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)下位レベルのドライバーでは、呼び出されたときに指定されている完了状態の値を取得する[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete).

-   呼び出す[ **WdfRequestGetCompletionParams** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)を取得する、 [ **WDF\_要求\_完了\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_completion_params)要求のバッファー、またはバスに固有の情報を表すオブジェクトをメモリへのハンドルなど、完了した要求に関する追加情報を含む構造体。

    ドライバーが呼び出せる[ **WdfRequestGetCompletionParams** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)呼び出した後にのみ[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend) I/O 要求を送信するには同期または非同期 I/O のターゲットにします。 ドライバーを呼び出してはならない**WdfRequestGetCompletionParams** I/O ターゲットにのみ同期的に I/O 要求を送信する方法のいずれかを呼び出した後 (など[ **WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)).

-   呼び出す[ **WdfRequestGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetinformation)下位レベルのドライバーが呼び出されたときに指定されている追加の I/O 完了の情報を取得する[ **WdfRequestSetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetinformation)または[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)ドライバー スタックのドライバーは、このような情報を提供する場合は、します。

ドライバーは、同期的に、I/O 要求を送信する場合、通常呼び出し[ **WdfRequestGetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)、 [ **WdfRequestGetCompletionParams** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)、および[ **WdfRequestGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetinformation)同期呼び出しが返された後にします。 通常内からこれらのメソッドを呼び出し、ドライバーは、非同期的に、I/O 要求を送信する場合、 [ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数。

I/O 要求を完了する詳細については、次を参照してください。[の同期をキャンセルし完了コード](synchronizing-cancel-and-completion-code.md)します。

 

 





