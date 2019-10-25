---
title: I/O 要求の完了
description: I/O 要求の完了
ms.assetid: ec5aef7a-110e-430c-902d-669ccc7095ac
keywords:
- I/o 要求 WDK KMDF、完了
- i/o 要求の完了 (WDK KMDF)
- 要求の処理 WDK KMDF、要求の完了
- 状態情報 WDK KMDF、i/o 要求の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 778a52af7323c6968a93da2fc3ab6c6f5c17a74a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843647"
---
# <a name="completing-io-requests"></a>I/O 要求の完了





すべてのフレームワークベースのドライバーは、最終的に、フレームワークから受信したすべての i/o 要求を完了する必要があります。 要求を完了するには、要求オブジェクトの[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、または[**wdfrequestcompletewithの各ブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)を呼び出します。

### <a name="when-to-complete-a-request"></a>要求を完了するタイミング

次のいずれかのケースに該当する場合、ドライバーは要求を完了する必要があります。

-   要求された i/o 操作が正常に完了しました。

-   要求された i/o 操作は開始されましたが、完了する前に失敗しました。

-   要求された i/o 操作はサポートされていないか、受信時に無効であったか、開始できませんでした。

-   要求された i/o 操作が取り消されました。

デバイスで i/o アクティビティを作成することによってドライバーが i/o 要求を処理する場合、ドライバーは通常、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) Callback 関数から[**wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出します。

ドライバーがサポートされていない、または無効な要求を受け取った場合、通常は、要求を受け取った[要求ハンドラー](request-handlers.md)から[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出します。

I/o 操作が[取り消さ](canceling-i-o-requests.md)れた場合、ドライバーは通常、 [*Evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数から[**wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出します。

ドライバーが i/o 要求を i/o[ターゲット](using-i-o-targets.md)に[転送](forwarding-i-o-requests.md)する場合、ドライバーは、i/o ターゲットが要求を完了した後、次のように要求を完了します。

-   ドライバーで i/o 要求が i/o ターゲットに[同期的](sending-i-o-requests-synchronously.md)に転送される場合、ドライバーの i/o ターゲットへの呼び出しは、下位レベルのドライバーが要求を完了した後にのみ返されます (エラーが発生しない場合)。 I/o ターゲットからが返された後、ドライバーは[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出す必要があります。

-   ドライバーが i/o 要求を[非同期](sending-i-o-requests-asynchronously.md)に転送する場合は、下位レベルのドライバーが要求を完了したときに、ドライバーに通知されるようにします。 ドライバーが、完了[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数を登録した場合、このコールバック関数は、i/o ターゲットが要求を完了した後に呼び出されます。 通常、入力*ルーチン*のコールバック関数は、 [**wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出します。

[*補完ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数を登録するには、ドライバーは、i/o 要求を i/o ターゲットに転送する前に、 [**Wdfrequestset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)を呼び出す必要があります。

I/o ターゲットが非同期的に転送された i/o 要求を完了したときにドライバーに通知する必要がない場合、ドライバーは、完了[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数を登録する必要がありません。 代わりに、ドライバーは、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出すときに、送信[ **\_と\_忘れるフラグを\_送信\_オプションを\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags)するように、WDF\_要求を設定できます。 この場合、ドライバーは[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出しません。

ドライバーは、 [**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)または[**Wdfrequestcreatefromirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)を呼び出すことによって作成された i/o 要求を完了しません。 代わりに、ドライバーは[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出して要求オブジェクトを削除する必要があります。通常は、i/o ターゲットが要求を完了した後に、このオブジェクトを削除します。

たとえば、ドライバーは、ドライバーの i/o ターゲットよりも大きいサイズのデータの読み取りまたは書き込み要求を一度に処理できる場合があります。 ドライバーは、データをいくつかの小さな要求に分割し、これらの小さな要求を1つ以上の i/o ターゲットに送信する必要があります。 この状況に対処するための手法は次のとおりです。

-   [**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)を呼び出して、小さい要求を表す1つの追加の要求オブジェクトを作成します。

    ドライバーは、i/o ターゲットにこの要求を同期的に送信できます。 小さい要求の実行可能[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数は、 [**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)を呼び出して、ドライバーが要求を再利用し、再度 i/o ターゲットに送信できるようにします。 I/o ターゲットが小さい要求の最後に完了した後、入力候補*のコールバック*関数は、 [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出してドライバーで作成された要求オブジェクトを削除し、ドライバーは[**wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出して完了することができます。元の要求。

-   [**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)を呼び出して、より小さな要求を表すいくつかの追加の要求オブジェクトを作成します。

    ドライバーの i/o ターゲットは、これらの複数の小さな要求を非同期的に処理できます。 ドライバーは、小さい要求のそれぞれに対して、実行可能な[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数を登録できます。 実行可能*ルーチン*のコールバック関数が呼び出されるたびに、 [**wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出して、ドライバーによって作成された要求オブジェクトを削除することができます。 I/o ターゲットがすべての小さな要求を完了すると、ドライバーは[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出して元の要求を完了することができます。

### <a href="" id="providing-completion-information"></a>完了情報の提供

ドライバーは、要求を完了すると、他のドライバーがアクセスできる追加情報を必要に応じて提供できます。 たとえば、ドライバーは、読み取り要求または書き込み要求に対して転送されたバイト数を提供する場合があります。 この情報を提供するために、ドライバーは次のいずれかを実行できます。

-   [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出す前に、 [**Wdfrequestsetinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetinformation)を呼び出してください。

-   [**Wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)を呼び出します。

### <a href="" id="obtaining-completion-information"></a>完了情報の取得

別のドライバーが完了した i/o 要求に関する情報を取得するために、ドライバーは次のことができます。

-   [**WdfRequestGetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)を呼び出して、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出したときに指定された下位レベルのドライバーの完了状態の値を取得します。

-   [**Wdfrequestgetcompletion params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)を呼び出して、完了した要求に関する追加情報を含む[**WDF\_要求\_完了\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_completion_params)構造体を取得します。これには、要求のバッファー、またはバス固有の情報。

    ドライバーは[**Wdfrequestget補完 params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)を呼び出すことができるのは、 [**wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して i/o 要求を同期的または非同期的に i/o ターゲットに送信した後のみです。 I/o ターゲットに i/o 要求を同期的に送信するメソッドの1つ ( [**Wdfiotargetsendreadsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)など) を呼び出すと、ドライバーは**Wdfrequestget補完 params**を呼び出すことができません。

-   [**Wdfrequestgetinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetinformation)を呼び出して、ドライバー内のドライバーが[**Wdfrequestsetinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetinformation)または[**wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)を呼び出したときに指定された下位レベルのドライバーによって追加の i/o 完了情報を取得します。stack は、このような情報を提供します。

ドライバーが i/o 要求を同期的に送信する場合、通常は、同期呼び出しから制御が戻った後、 [**WdfRequestGetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)、 [**wdfrequestget補完 Params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)、および[**wdfrequestgetinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetinformation)を呼び出します。 ドライバーは、非同期的に i/o 要求を送信する場合、通常、これらのメソッドを、[*補完ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数内から呼び出します。

I/o 要求の完了の詳細については、「[キャンセルと完了コードの同期](synchronizing-cancel-and-completion-code.md)」を参照してください。

 

 





