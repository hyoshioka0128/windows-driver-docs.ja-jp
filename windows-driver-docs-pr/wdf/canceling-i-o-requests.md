---
title: I/O 要求をキャンセルします。
description: I/O 要求をキャンセルします。
ms.assetid: 9a486fa4-7fd3-4433-88aa-34a54d9b1e16
keywords:
- 要求の WDK KMDF、キャンセル要求を処理します。
- I/O 要求のキャンセルの WDK KMDF
- WDK KMDF を要求する I/O のキャンセル
- 配信されなかった I/O 要求の WDK KMDF
- WDK KMDF を要求する I/O の転送
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b6859211afb123d3bc10039a67a203fe4490892
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551343"
---
# <a name="canceling-io-requests"></a>I/O 要求をキャンセルします。





アプリケーションやシステム、ドライバーでは、(いくつかのブロックをディスクから読み取る要求) などのデバイスの進行中の I/O 操作をキャンセルできます。 デバイスの I/O 操作が取り消された場合、I/O マネージャーは、I/O 操作に関連付けられているすべての未処理 I/O 要求をキャンセルしようとします。 デバイスのドライバーが I/O マネージャーが、I/O 要求をキャンセルしようとして、ドライバーは、自分が所有する要求をキャンセルできるときに通知を登録できます[完了](completing-i-o-requests.md)ステータスの完了ステータスに\_取り消されました。

フレームワークは、フレームワークに基づいたドライバーの取り消し処理の一部を処理します。 フレームワークには、次の I/O 要求が完了すると、デバイスの I/O 操作が取り消された場合 (状態を表す完了状態で\_CANCELLED) が取り消された操作に関連付けられています。

-   未配信 I/O は、I/O キュー、ドライバーの既定値にフレームワークが格納されたことを要求します。

-   フレームワークは、ドライバーが呼び出されるために、別のキューに転送する I/O 要求を配信できなかった[ **WdfDeviceConfigureRequestDispatching**](https://msdn.microsoft.com/library/windows/hardware/ff545920)します。

フレームワークは、これらの要求をキャンセルしたため、いないドライバーに配信には。

フレームワークには、ドライバーのドライバーに、I/O 要求が配信された後[所有](request-ownership.md)要求と、フレームワークはこれで取り消すことはできません。 この時点では、ドライバーのみが、I/O 要求をキャンセルできますが、フレームワークは、ドライバーを通知する必要があります、要求を取り消す必要があります。 ドライバーが提供することでこの通知を受信する[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)コールバック関数。

場合があります、ドライバー、I/O キューから I/O 要求を受信するが、要求を処理するのではなく、ドライバー キューに再登録を同じまたは別の要求後で処理するための I/O キュー。 このような状況の例については、次のとおりです。

-   フレームワークのドライバーのいずれかに、I/O 要求を提供する[要求ハンドラー](request-handlers.md)、ドライバーが、その後いずれかを呼び出すと[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958) (または[**WdfRequestForwardToParentDeviceIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549959)) 要求を別のキューに配置するか、 [ **WdfRequestRequeue** ](https://msdn.microsoft.com/library/windows/hardware/ff550012)を配置する、同じキューに要求します。

-   フレームワークは、ドライバーに、I/O 要求を配信[ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764)コールバック関数では、ドライバー呼び出し[ **WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945)フレームワークにバックアップ要求を渡すし、その後、フレームワークは、ドライバーの I/O キューのいずれかで要求を配置します。

このような場合は、フレームワークは、要求が、I/O キューであるため、I/O 要求をキャンセルできます。 ただし、ドライバーが登録されている場合、 [ *EvtIoCanceledOnQueue* ](https://msdn.microsoft.com/library/windows/hardware/ff541756)要求が存在する I/O キューのコールバック関数、フレームワークの呼び出しをキャンセルではなく、コールバック関数、関連する I/O 操作がキャンセルされた場合に要求します。 フレームワークは、ドライバーの場合*EvtIoCanceledOnQueue*コールバック関数では、ドライバーの必要があります[完了](completing-i-o-requests.md)要求。

要約すると、I/O 操作が取り消されたときに、フレームワークがドライバーに配信されたことはありませんすべての関連する I/O 要求にキャンセルする常にします。 ドライバーが要求を受信し、そのキューに再登録する場合、framework 要求をキャンセルします (要求がキューにある場合)、ドライバーを提供しない限り、 [ *EvtIoCanceledOnQueue* ](https://msdn.microsoft.com/library/windows/hardware/ff541756)用コールバック関数I/O キューです。

### <a name="calling-wdfrequestmarkcancelable-or-wdfrequestmarkcancelableex"></a>WdfRequestMarkCancelable または WdfRequestMarkCancelableEx を呼び出す

ドライバーが呼び出せる[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)または[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)を登録する、 [ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)コールバック関数。 ドライバーが呼び出された場合**WdfRequestMarkCancelable**または**WdfRequestMarkCancelableEx**要求に関連付けられている I/O 操作が取り消された場合、フレームワーク、ドライバーのと*EvtRequestCancel*コールバック関数のため、ドライバーは、I/O 要求を取り消すことができます。

ドライバーを呼び出す必要があります[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)または[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)の要求を所有する場合、比較的時間。 たとえば、ドライバーは、デバイスが応答を待機する必要がありますまたは一連のドライバーを作成する要求を完了する下位のドライバーを待つ場合が 1 つの要求を受け取ったとき。

ドライバーが要求されていない場合[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)または[ **WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)ドライバーがを呼び出す場合、または[ **WdfRequestUnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff550035)呼び出した後**WdfRequestMarkCancelable**または**WdfRequestMarkCancelableEx**、ドライバーキャンセルを認識しないと、したがって通常どおり要求を処理します。

### <a name="calling-wdfrequestiscanceled"></a>WdfRequestIsCanceled を呼び出す

ドライバーが呼び出されていない場合[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)または[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)を登録する、 [*EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)呼び出すことができるコールバック関数、 [ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976) I/O マネージャーがしようとかどうかを判断するにはI/O 要求をキャンセルします。 場合**WdfRequestIsCanceled**返します**TRUE**ドライバーは、要求を所有しているとは、ドライバーは、要求をキャンセルする必要があります。 呼び出す必要がありますいない場合は、ドライバーが要求を所有していない**WdfRequestIsCanceled**します。

呼び出されていないドライバー [ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)または[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)呼び出す[**WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)次の状況で。

-   デバイスの割り込みを呼び出すを待機するドライバー [ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)からその[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数。

-   そのデバイスをポーリングするドライバーを呼び出すことができます[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)ポーリング スレッドから。

-   分割するドライバー、 [DMA トランザクション](dma-transactions-and-dma-transfers.md)小さいいくつかの転送に呼び出すことができます[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)各転送の完了後します。

-   受け取る、大規模なドライバーの読み取りまたは書き込み要求をいくつかの小さな要求に分割が呼び出す可能性があります[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)ドライバーの I/O のターゲットが各小規模の要求が完了したらドライバーが呼び出されていない場合[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)または[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)受信用要求。

### <a name="canceling-the-request"></a>要求をキャンセル

I/O 要求をキャンセル、次のいずれかがあります。

-   進行中の I/O 操作を停止しています。

-   I/O のターゲットに要求を転送できません。

-   呼び出す[ **WdfRequestCancelSentRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff549941)しようとすると、ドライバーが I/O のターゲットに送信された以前の要求をキャンセルします。

ドライバーが呼び出してで要求を完了する必要があります常に場合は、ドライバーのドライバーが、framework から受信した要求オブジェクトの I/O 要求をキャンセル、 [ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)で、 *の状態*パラメーターの状態の\_キャンセルします。 (ドライバーが呼び出された場合[ **WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951)ドライバー呼び出し、要求オブジェクトを作成する[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)の代わりに要求を完了します。)

### <a name="synchronizing-cancellation"></a>同期のキャンセル

同期 I/O 要求をキャンセルするコードについてを参照してください。

-   [キャンセルおよび終了コードを同期します。](synchronizing-cancel-and-completion-code.md)

-   [同期送信済み要求の取り消し](synchronizing-cancellation-of-sent-requests.md)

 

 





