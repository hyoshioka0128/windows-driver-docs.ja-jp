---
title: UMDF で i/o 要求を完了しています
description: UMDF で i/o 要求を完了しています
ms.assetid: 3f8c7030-7c5d-4f65-8001-592af0b1d2de
keywords:
- I/o 要求 WDK UMDF、完了
- WDK UMDF の要求処理、要求の完了
- i/o 要求の完了 (WDK UMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96b3c35aaa7e0a1d0227e5eac6d017a08fffeb20
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210234"
---
# <a name="completing-io-requests-in-umdf"></a>UMDF で i/o 要求を完了しています


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

すべての i/o 要求は、最終的には、UMDF ドライバーによって完了される必要があります。 要求を完了するには、ドライバーは[**IWDFIoRequest:: complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)または[**IWDFIoRequest:: completewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)メソッドのいずれかを呼び出す必要があります。 ドライバーが要求を完了すると、次のいずれかのシナリオが示されます。

-   要求された i/o 操作が正常に完了しました。

-   要求された i/o 操作は開始されましたが、完了する前に失敗しました。

-   要求された i/o 操作はサポートされていないか、受信時に無効であるため、デバイスと通信できません。

-   要求された i/o 操作が[取り消さ](canceling-i-o-requests.md)れました。

ドライバーは、 [**IWDFIoRequest:: CompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)メソッドを呼び出して、要求操作に関する追加情報を渡します。 たとえば、読み取り操作の場合、ドライバーは読み取ったバイト数を提供する必要があります。

I/o 要求を完了するには、ドライバーは、 [**IWDFIoRequest:: complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)または[**IWDFIoRequest:: completewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)の呼び出しで、適切な完了ステータスを completion *status*パラメーターに渡す必要があります。 ドライバーは、HRESULT コードを使用して、完了した要求の状態を通知します。

[UMDF driver ホストプロセス](umdf-driver-host-process.md)は、完了した要求をリフレクタ (Wudfrd .sys) に渡す前に、HRESULT コードを NTSTATUS コードに変換します。 リフレクターは、NTSTATUS コードをオペレーティングシステムに渡します。 オペレーティングシステムは、呼び出し元のアプリケーションに結果を表示する前に、NTSTATUS コードを Microsoft Win32 エラーコードに変換します。

ドライバーのエラーコードを正しく変換できるようにするには、次のいずれかの方法でエラーコードを作成する必要があります。

-   Winerror.h からのエラーコードを使用し、\_WIN32 マクロから HRESULT\_を適用します。

-   Ntstatus からのエラーコードを使用し、\_NT マクロから HRESULT\_を適用します。

これらのマクロの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

次のコード例は、適切なエラーコードを使用して要求を完了する方法を示しています。

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

ドライバーが要求を正常に完了すると、S\_OK が返されます。これは HRESULT 値です。 \_OK は、Winerror.h では\_エラーと同じであり、Ntstatus で成功\_場合は、変換マクロは必要ありません。

[ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)がリフレクターに対して有効になっている場合は、無効なステータスコードが識別され、システムのバグチェックが発生します。

**注**   Windows XP のドライバーの検証ツールでは、10進 1024 (1024l) を超える値を持つ Win32 エラーコードに対してシステムのバグチェックが正しく行われないことに注意してください。 ドライバーが Windows XP で実行されている場合、この問題については、リフレクタのドライバーの検証機能を有効にする必要があります。

 

ドライバーが以前に下位レベルのドライバーに要求を送信した場合、ドライバーは下位レベルのドライバーが要求を完了したときに通知を必要とします。 通知を登録するために、ドライバーは[**IWDFIoRequest:: Set callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)メソッドを呼び出して、下位レベルのドライバーが要求を完了したときにフレームワークが呼び出すメソッドのインターフェイスを登録します。 ドライバーは、要求を完了するために必要な操作を実行するために、 [**Irequestcallback Requestcompletion:: OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)コールバック関数を実装します。

ドライバーは、 [**Iwdfdevice:: CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)を呼び出すことによって作成された i/o 要求を完了しません。 代わりに、ドライバーは[**Iwdfobject::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を呼び出す必要があります。これは通常、i/o ターゲットが要求を完了した後に要求オブジェクトを削除するために行います。

たとえば、ドライバーは、ドライバーの i/o ターゲットよりも大きいサイズのデータの読み取りまたは書き込み要求を一度に処理できる場合があります。 ドライバーは、データをいくつかの小さな要求に分割し、これらの小さな要求を1つ以上の i/o ターゲットに送信する必要があります。 この状況に対処するための手法は次のとおりです。

-   [**Iwdfdevice:: CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)を呼び出して、より小さな要求を表す1つの追加の要求オブジェクトを作成します。

    ドライバーは、i/o ターゲットにこの要求を同期的に送信できます。 小さい要求の[**IrequestIWDFIoRequest2 Requestcompletion:: OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)コールバック関数は、ドライバーが要求を再利用して、再度 i/o ターゲットに送信できるように、 [**:: 再利用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)を呼び出すことができます。 I/o ターゲットがより小さな要求の最後に完了した後、 **Oncompletion**コールバック関数は[**iwdfobject::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を呼び出して、ドライバーによって作成された要求オブジェクトを削除します。ドライバーは[**IWDFIoRequest:: Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)を呼び出して元の要求を完了できます。

-   [**Iwdfdevice:: CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)を呼び出して、より小さな要求を表すいくつかの追加の要求オブジェクトを作成します。

    ドライバーの i/o ターゲットは、これらの複数の小さな要求を非同期的に処理できます。 ドライバーは、小さい要求ごとに[**Oncompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)コールバック関数を登録できます。 **Oncompletion**コールバック関数が呼び出されるたびに、 [**iwdfobject::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を呼び出して、ドライバーによって作成された要求オブジェクトを削除できます。 I/o ターゲットがすべての小さな要求を完了すると、ドライバーは[**IWDFIoRequest:: Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)を呼び出して元の要求を完了することができます。

### <a name="obtaining-completion-information"></a>完了情報の取得

他のドライバーが完了した i/o 要求に関する情報を取得するために、UMDF ベースのドライバーは次のことが可能です。

-   [**Iwdfrequestcompletion params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfrequestcompletionparams)インターフェイスを使用して、i/o 要求の完了ステータスとその他の情報を取得します。

-   [**IWDFIoRequestCompletionParams**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequestcompletionparams)インターフェイスを使用して、i/o 要求のメモリバッファーを取得します。

-   [**IWDFUsbRequestCompletionParams**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbrequestcompletionparams)インターフェイスを使用して、USB ターゲットパイプオブジェクトに送信された要求に関連するメモリバッファーおよびその他の情報を取得します。

さらに、UMDF ベースのドライバーでは、 [**IWDFIoRequest2:: GetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-getstatus)メソッドを使用して、要求の完了前または完了後に i/o 要求の現在の状態を取得できます。

 

 





