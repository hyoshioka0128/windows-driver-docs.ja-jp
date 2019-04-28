---
title: UMDF で I/O 要求の完了
description: UMDF で I/O 要求の完了
ms.assetid: 3f8c7030-7c5d-4f65-8001-592af0b1d2de
keywords:
- I/O 要求の完了の WDK UMDF
- 要求の処理要求の完了の WDK UMDF
- WDK UMDF を要求する I/O の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de08ba935b045cc2c6e16f8ff8bf076374afdde1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376878"
---
# <a name="completing-io-requests-in-umdf"></a>UMDF で I/O 要求の完了


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

すべての I/O 要求は、UMDF ドライバーによって最終的に完了する必要があります。 要求を完了するには、ドライバー、呼び出す必要がありますか、 [ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)または[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)メソッド。 ドライバーでは、要求が完了したら、次のシナリオのいずれかを示します。

-   要求された I/O 操作が正常に完了しました。

-   要求された I/O 操作では、開始が完了する前に失敗しました。

-   要求された I/O 操作はサポートされていないか、デバイスと通信できないため、受信した時点では無効です。

-   I/O 操作が要求されました[キャンセル](canceling-i-o-requests.md)します。

ドライバーの呼び出し、 [ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)要求操作に関する追加情報を渡す方法です。 たとえば、読み取り操作では、ドライバーは、読み取られたバイト数を提供する必要があります。

ドライバー、I/O 要求を完了するに適切な完了状態を渡す必要があります、 *CompletionStatus*への呼び出しでパラメーター [ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)または[ **IWDFIoRequest::CompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff559074)します。 ドライバーは、完了した要求のステータスを通知するのに HRESULT コードを使用します。

[UMDF ドライバーのホスト プロセス](umdf-driver-host-process.md)reflector (Wudfrd.sys) に完了した要求を渡す前に、NTSTATUS コードを HRESULT コードに変換します。 Reflector は、オペレーティング システムに NTSTATUS コードを渡します。 オペレーティング システムは、呼び出し元アプリケーションに結果を表示する前に、Microsoft Win32 エラー コードに NTSTATUS コードを変換します。

ドライバーのエラー コードを正しく変換できることを確認するには、次の手法のいずれかでエラー コードを作成する必要があります。

-   Winerror.h からエラー コードを使用し、HRESULT を適用\_FROM\_WIN32 マクロ。

-   Ntstatus.h からエラー コードを使用し、HRESULT を適用\_FROM\_NT マクロ。

これらのマクロの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

次のコード例では、適切なエラー コードを使用して要求を完了する方法を示します。

```cpp
VOID
STDMETHODCALLTYPE
CMyQueue::OnWrite(
    __in IWDFIoQueue *pWdfQueue,
    __in IWDFIoRequest *pWdfRequest,
    __in SIZE_T BytesToWrite
    )
{
            -------------------- 
    if( BytesToWrite > MAX_WRITE_LENGTH ) {
        pWdfRequest->CompleteWithInformation(HRESULT_FROM_WIN32(ERROR_MORE_DATA), 0);
        return;
    }
            ---------------------
}
```

ドライバーでは、要求は正常に完了すると、それを返します S\_HRESULT 値は、[ok] です。 S\_ok を いいえは\_Winerror.h および状態のエラー\_Ntstatus.h、マクロが不要な変換に成功します。

場合[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)が有効になって、reflector 無効なステータス コードを識別し、システムでバグチェックが発生します。

**注**   Windows XP の Driver Verifier を誤る 1024 (1024 L) の 10 進数を超える値を持つ Win32 エラー コードのシステムでバグチェックが発生します。 ドライバーは、Windows XP で実行する場合の注意してくださいこの問題、reflector の Driver Verifier を有効にした場合。

 

場合は、ドライバーは、以前より低いレベルのドライバーに要求を送信、下位レベルのドライバーが要求を完了すると通知が ドライバーに必要です。 ドライバーの呼び出し通知に登録するのには、 [ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)ときにフレームワークから呼び出されるメソッドのインターフェイスを登録する方法、下位レベルのドライバー要求を完了します。 ドライバーの実装、 [ **IRequestCallbackRequestCompletion::OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)要求を完了に必要な操作を実行するコールバック関数。

ドライバーが呼び出すことで作成した I/O 要求が完了しない[ **IWDFDevice::CreateRequest**](https://msdn.microsoft.com/library/windows/hardware/ff557021)します。 代わりに、ドライバーを呼び出す必要があります[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210) I/O をターゲットには、要求が完了した後、通常、要求オブジェクトを削除します。

たとえば、ドライバーは、読み取りを受け取ることがあります。 またはをドライバーの I/O ターゲットを超えるデータ量の書き込み要求を同時に処理できます。 ドライバーは、いくつかの小さな要求にデータを分割し、1 つまたは複数の I/O ターゲットにこれらの小さい要求を送信する必要があります。 このような状況を処理するための手法は次のとおりです。

-   呼び出す[ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)小さな要求を表す 1 つの追加要求オブジェクトを作成します。

    ドライバーでは、I/O のターゲットに、この要求を同期的に送信できます。 小さな要求の[ **IRequestCallbackRequestCompletion::OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)コールバック関数を呼び出すことができます[ **IWDFIoRequest2::Reuse** ](https://msdn.microsoft.com/library/windows/hardware/ff559048)ドライバーが要求を再利用してもう一度 I/O ターゲットに送信できるようにします。 I/O ターゲットが小規模の要求の最後のタスクが完了したら、 **OnCompletion**コールバック関数を呼び出すことができます[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)を削除します要求のドライバーが作成したオブジェクトと、ドライバーが呼び出すことができます[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)元の要求を完了します。

-   呼び出す[ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)小さな要求を表すいくつかの追加の要求オブジェクトを作成します。

    ドライバーの I/O のターゲットは、これら複数の小さい要求を非同期的に処理できます。 ドライバーが登録できる、 [ **OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)小さな要求ごとのコールバック関数。 ごとに、 **OnCompletion**コールバック関数が呼び出されると、呼び出すことができます[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)ドライバーが作成した要求オブジェクトを削除します。 I/O のターゲットには、すべての小さい要求が完了すると、ドライバーを呼び出すことが[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)元の要求を完了します。

### <a name="obtaining-completion-information"></a>完了の情報を取得します。

別のドライバーが完了する I/O 要求に関する情報を取得するには、UMDF ドライバーでは次のことができます。

-   使用して、 [ **IWDFRequestCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff560292)インターフェイスには、I/O 要求の完了ステータスおよびその他の情報を取得します。

-   使用して、 [ **IWDFIoRequestCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff559055)インターフェイスは、I/O 要求のメモリ バッファーを取得します。

-   使用して、 [ **IWDFUsbRequestCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff560346) USB ターゲット パイプ オブジェクトに送信された要求に関連するメモリ バッファーとその他の情報を取得するインターフェイス。

UMDF ドライバーをさらに、使用することができます、 [ **IWDFIoRequest2::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559013)前に、か、要求が完了した後は、I/O 要求の現在の状態を取得します。

 

 





