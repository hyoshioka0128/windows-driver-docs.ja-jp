---
title: UMDF で I/O 要求をキャンセルします。
description: UMDF で I/O 要求をキャンセルします。
ms.assetid: 4f69903b-00ef-4b47-a564-aaa7d076481b
keywords:
- I/O 要求のキャンセルの WDK UMDF
- 要求の WDK UMDF、キャンセル要求を処理します。
- WDK UMDF を要求する I/O のキャンセル
- 実行中の要求 WDK UMDF
- I/O 要求の WDK UMDF、状態
- 要求の WDK UMDF、状態の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dae2371b14dac04042f3fa0b13291a698d064acc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376908"
---
# <a name="canceling-io-requests-in-umdf"></a>UMDF で I/O 要求をキャンセルします。


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

アプリケーションやシステム、ドライバーでは、(いくつかのブロックをディスクから読み取る要求) などのデバイスの進行中の I/O 操作をキャンセルできます。 デバイスの I/O 操作が取り消された場合、I/O マネージャーは、I/O 操作に関連付けられているすべての未処理 I/O 要求をキャンセルしようとします。 デバイスのドライバーが I/O マネージャーが、I/O 要求をキャンセルしようとして、ドライバーは、自分が所有する要求をキャンセルできるときに通知を登録できます[完了](completing-i-o-requests.md)HRESULT の完了ステータスに\_FROM\_WIN32 (エラー\_操作\_ABORTED)。

フレームワークは、フレームワークに基づいたドライバーの取り消し処理の一部を処理します。 デバイスの I/O 操作が取り消された場合、フレームワークになって完了--HRESULT の完了ステータス\_FROM\_WIN32 (エラー\_操作\_ABORTED)--次の I/O 要求に関連付けられている、取り消された操作:

-   未配信 I/O は、I/O キュー、ドライバーの既定値にフレームワークが格納されたことを要求します。

-   フレームワークは、ドライバーが呼び出されるために、別のキューに転送する I/O 要求を配信できなかった[ **IWDFIoQueue::ConfigureRequestDispatching**](https://msdn.microsoft.com/library/windows/hardware/ff558946)します。

フレームワークは、これらの要求をキャンセルしたため、いないドライバーに配信には。

フレームワークは、ドライバーに、I/O 要求を配信するが後、は、ドライバーは、要求を所有し、フレームワークで取り消すことはできません。 この時点では、ドライバーのみが、I/O 要求をキャンセルできますが、フレームワークは、ドライバーを通知する必要があります、要求を取り消す必要があります。 ドライバーが提供することでこの通知を受信する[ **IRequestCallbackCancel::OnCancel** ](https://msdn.microsoft.com/library/windows/hardware/ff556903)コールバック関数。

場合があります、ドライバー、I/O キューから I/O 要求を受信するが、要求を処理するのではなく、ドライバー キューに再登録を同じまたは別の要求後で処理するための I/O キュー。 たとえば、フレームワークは、ドライバーの要求ハンドラーのいずれかに、I/O 要求を配信する可能性があり、ドライバーがいずれかを呼び出す、その後[ **IWDFIoRequest::ForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff559081)要求を配置するには別のキューでまたは[ **IWDFIoRequest2::Requeue** ](https://msdn.microsoft.com/library/windows/hardware/ff559028)要求を同じキューに配置します。

このような場合は、フレームワークは、要求が、I/O キューであるため、I/O 要求をキャンセルできます。 ただし、ドライバーが、コールバック関数が、要求が存在する I/O キューの登録と、フレームワークは、関連する I/O 操作がキャンセルされた場合、要求をキャンセルではなく、コールバック関数を呼び出します。 フレームワークでは、ドライバーのコールバック関数を呼び出し、ドライバーは、要求を取り消す必要があります。

要約すると、I/O 操作が取り消されたときに、フレームワークがドライバーに配信されたことはありませんすべての関連する I/O 要求にキャンセルする常にします。 ドライバーが要求を受信し、そのキューに再登録する場合フレームワーク要求をキャンセルします (要求がキューにある場合)、ドライバーは、I/O キューのコールバック関数を提供しない限り、します。

### <a name="calling-markcancelable"></a>MarkCancelable を呼び出す

ドライバーを呼び出すことができます[ **IWDFIoRequest::MarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff559146)を登録する、 [ **IRequestCallbackCancel::OnCancel** ](https://msdn.microsoft.com/library/windows/hardware/ff556903)コールバック関数。 ドライバーが呼び出された場合**MarkCancelable**、ドライバーのフレームワーク、要求に関連付けられている I/O 操作が取り消された場合と**OnCancel**コールバック関数のドライバーを取り消すことが、I/O 要求。

ドライバーを呼び出す必要があります**MarkCancelable**のに比較的長い時間の要求を所有している場合。 たとえば、ドライバーは、デバイスが応答を待機する必要がありますまたは下位のドライバーを一連のドライバーを作成する要求を完了するまで待機する必要が 1 つの要求を受け取ったとき。

ドライバーが要求されていない場合**MarkCancelable**、ドライバーを呼び出す場合、または[ **IWDFIoRequest::UnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff559163)呼び出した後**MarkCancelable**したがってハンドル、要求される通常のプログラムと、ドライバーは、キャンセルの認識しません。

### <a name="calling-iscanceled"></a>IsCanceled を呼び出す

ドライバーが呼び出されていない場合**MarkCancelable**を登録する、 **OnCancel**呼び出すことができるコールバック関数、 [ **IWDFIoRequest2::IsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff559018)I/O マネージャーが I/O 要求をキャンセルしようとしたかどうかを判断します。 場合**IsCanceled**返します**TRUE**ドライバーは、要求をキャンセルする必要があります。

たとえば、大きなを受信するドライバーの読み取りまたはいくつかの小さな要求に分割書き込み要求を呼び出すことができます**IsCanceled**ドライバーが呼び出されていない場合、小さな要求の各ドライバーのI/Oターゲット完了後**MarkCancelable**受信した要求。

### <a name="canceling-the-request"></a>要求をキャンセル

I/O 要求をキャンセル、次のいずれかがあります。

-   進行中の I/O 操作を停止しています。

-   I/O のターゲットに要求を転送できません。

-   呼び出す[ **IWDFIoRequest::CancelSentRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559067)しようとすると、ドライバーが I/O のターゲットに送信された以前の要求をキャンセルします。

ドライバーが呼び出してで要求を完了する必要があります常に場合は、ドライバーのドライバーが、framework から受信した要求オブジェクトの I/O 要求をキャンセル、 [ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)または[ **IWDFIoRequest::CompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff559074)で、 *CompletionStatus*の HRESULT パラメーター\_FROM\_WIN32(ERROR\_操作\_ABORTED)。 (ドライバーが呼び出された場合[ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)ドライバー呼び出し、要求オブジェクトを作成する[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)要求を完了するのではなく)。

 

 





