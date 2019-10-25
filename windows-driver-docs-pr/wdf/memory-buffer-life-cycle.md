---
title: メモリ バッファーのライフ サイクル
description: メモリ バッファーのライフ サイクル
ms.assetid: abf43bf5-a4a3-4aeb-9ec5-3458252933d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 748483de4fddb8bb703571b62c7bdbd86b75b7eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843147"
---
# <a name="memory-buffer-life-cycle"></a>メモリ バッファーのライフ サイクル


メモリバッファーのライフサイクルは、バッファーが作成されてから削除されるまでの時間を範囲とします。 このトピックでは、バッファーの使用シナリオと、バッファーが削除されたときの影響について説明します。

カーネルモードドライバーフレームワーク (KMDF) では、要求オブジェクトは i/o 要求を表します。 すべての要求オブジェクトは1つ以上のメモリオブジェクトに関連付けられており、各メモリオブジェクトは、要求内の入力または出力に使用されるバッファーを表します。

フレームワークは、入力 i/o 要求を表す要求オブジェクトとメモリオブジェクトを作成するときに、関連付けられているメモリオブジェクトの親として要求オブジェクトを設定します。 そのため、メモリオブジェクトは、要求オブジェクトの有効期間よりも長く保持される可能性があります。 フレームワークベースのドライバーが i/o 要求を完了すると、フレームワークは要求オブジェクトとメモリオブジェクトを削除するので、これらの2つのオブジェクトのハンドルは無効になります。

ただし、基になるバッファーは異なります。 バッファーを作成したコンポーネントとバッファーの作成方法に応じて、バッファーには参照カウントがあり、メモリオブジェクトによって所有されている可能性があります。そうでない場合もあります。 メモリオブジェクトがバッファーを所有している場合、バッファーは参照カウントを持ち、その有効期間はメモリオブジェクトの有効期間に制限されます。 他のコンポーネントがバッファーを作成した場合は、バッファーの有効期間とメモリオブジェクトが関連付けられていません。

フレームワークベースのドライバーは、i/o ターゲットに送信する独自の要求オブジェクトを作成することもできます。 ドライバーによって作成された要求では、ドライバーが i/o 要求で受信した既存のメモリオブジェクトを再利用できます。 I/o ターゲットに頻繁に要求を送信するドライバーは、作成した[要求オブジェクトを再利用](reusing-framework-request-objects.md)できます。

ドライバーが無効なハンドルまたはバッファーポインターを参照しないようにするには、要求オブジェクト、メモリオブジェクト、および基になるバッファーの有効期間を理解することが重要です。

次の使用シナリオについて考えてみましょう。

-   シナリオ 1:[ドライバーは KMDF から i/o 要求を受け取り、それを処理し](#scenario-1-driver-receives-an-io-request-from-kmdf-handles-it-and-completes-it)て、完了します。
-   シナリオ 2:[ドライバーは KMDF から i/o 要求を受信し、i/o ターゲットに転送](#scenario-2-driver-receives-an-io-request-from-kmdf-and-forwards-it-to-an-io-target)します。
-   シナリオ 3:[ドライバーは、既存のメモリオブジェクトを使用する i/o 要求を発行](#scenario-3-driver-issues-an-io-request-that-uses-an-existing-memory-object)します。
-   シナリオ 4:[ドライバーは、新しいメモリオブジェクトを使用する i/o 要求を発行します。](#scenario-4-driver-issues-an-io-request-that-uses-a-new-memory-object)
-   シナリオ 5:[ドライバーは、作成した要求オブジェクトを再利用します。](#scenario-5-driver-reuses-a-request-object-that-it-created)

## <a name="scenario-1-driver-receives-an-io-request-from-kmdf-handles-it-and-completes-it"></a>シナリオ 1: ドライバーは KMDF から i/o 要求を受け取り、それを処理して、完了します。

最も単純なシナリオでは、KMDF はドライバーに要求をディスパッチします。これにより i/o が実行され、要求が完了します。 この場合、基になるバッファーは、ユーザーモードアプリケーション、別のドライバー、またはオペレーティングシステム自体によって作成されている可能性があります。 バッファーにアクセスする方法の詳細については、「[フレームワークベースのドライバーでのデータバッファー](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)へのアクセス」を参照してください。

ドライバーが[要求を完了](completing-i-o-requests.md)すると、フレームワークはメモリオブジェクトを削除します。 バッファーポインターは無効になります。

## <a name="scenario-2-driver-receives-an-io-request-from-kmdf-and-forwards-it-to-an-io-target"></a>シナリオ 2: ドライバーは KMDF から i/o 要求を受信し、i/o ターゲットに転送します。

このシナリオでは、ドライバーは i/o ターゲットに[要求を転送](forwarding-i-o-requests.md)します。 次のサンプルコードは、ドライバーが受信要求オブジェクトからメモリオブジェクトへのハンドルを取得し、i/o ターゲットに送信するように要求を書式設定して、要求を送信する方法を示しています。

```cpp
VOID
EvtIoRead(
    IN WDFQUEUE Queue,
    IN WDFREQUEST Request,
    IN size_t Length
    )
{
    NTSTATUS status;
    WDFMEMORY memory;
    WDFIOTARGET ioTarget;
    BOOLEAN ret;
    ioTarget = WdfDeviceGetIoTarget(WdfIoQueueGetDevice(Queue));

    status = WdfRequestRetrieveOutputMemory(Request, &memory);
    if (!NT_SUCCESS(status)) {
        goto End;
    }

    status = WdfIoTargetFormatRequestForRead(ioTarget,
                                    Request,
                                    memory,
                                    NULL,
                                    NULL);
    if (!NT_SUCCESS(status)) {
        goto End;
    }

    WdfRequestSetCompletionRoutine(Request,
                                    RequestCompletionRoutine,
                                    WDF_NO_CONTEXT);

    ret = WdfRequestSend (Request, ioTarget, WDF_NO_SEND_OPTIONS);
    if (!ret) {
        status = WdfRequestGetStatus (Request);
        goto End;
    }

    return;

End:
    WdfRequestComplete(Request, status);
    return;

}
```

I/o ターゲットが要求を完了すると、フレームワークは、ドライバーが要求に対して設定した完了コールバックを呼び出します。 次のコードは、単純な完了コールバックを示しています。

```cpp
VOID
RequestCompletionRoutine(
    IN WDFREQUEST                  Request,
    IN WDFIOTARGET                 Target,
    PWDF_REQUEST_COMPLETION_PARAMS CompletionParams,
    IN WDFCONTEXT                  Context
    )
{
    UNREFERENCED_PARAMETER(Target);
    UNREFERENCED_PARAMETER(Context);

    WdfRequestComplete(Request, CompletionParams->IoStatus.Status);

    return;

}
```

ドライバーが完了コールバックから[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出すと、フレームワークはメモリオブジェクトを削除します。 取得したドライバーが無効になっているメモリオブジェクトハンドル。

## <a name="scenario-3-driver-issues-an-io-request-that-uses-an-existing-memory-object"></a>シナリオ 3: ドライバーは、既存のメモリオブジェクトを使用する i/o 要求を発行します。


一部のドライバーは、独自の i/o 要求を発行し、i/o ターゲットオブジェクトによって表される i/o ターゲットに送信します。 ドライバーは、独自の要求オブジェクトを作成するか、[フレームワークによって作成された要求オブジェクトを再利用](reusing-framework-request-objects.md)することができます。 どちらの方法を使用しても、ドライバーは前の要求からメモリオブジェクトを再利用できます。 ドライバーは、基になるバッファーを変更する必要はありませんが、新しい i/o 要求をフォーマットするときにバッファーオフセットを渡すことができます。

既存のメモリオブジェクトを使用する新しい i/o 要求をフォーマットする方法の詳細については、「[一般的な I/o ターゲットへ](sending-i-o-requests-to-general-i-o-targets.md)の i/o 要求の送信」を参照してください。

I/o ターゲットに送信するように要求の形式を設定すると、i/o ターゲットオブジェクトに代わって、再利用されるメモリオブジェクトの参照を取得します。 I/o ターゲットオブジェクトは、次のいずれかのアクションが発生するまで、この参照を保持します。

-   要求が完了しました。
-   このドライバーは、 *Wdfiotargetformatrequestxxx*または*Wdfiotargetsendxxx*のいずれかの同期メソッドを呼び出すことによって、要求オブジェクトを再フォーマットします。 これらのメソッドの詳細については、「 [Framework I/o Target オブジェクトメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/)」を参照してください。
-   ドライバーは[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)を呼び出します。

新しい i/o 要求が完了すると、フレームワークは、この要求に対してドライバーが設定した i/o 完了コールバックを呼び出します。 この時点で、i/o ターゲットオブジェクトはメモリオブジェクトへの参照を保持しています。 そのため、i/o 完了コールバックでは、ドライバーが作成した要求オブジェクトで[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)を呼び出してから、メモリオブジェクトを取得した元の要求を完了する必要があります。 ドライバーが**WdfRequestReuse**を呼び出さない場合は、追加の参照が原因でバグチェックが行われます。

## <a name="scenario-4-driver-issues-an-io-request-that-uses-a-new-memory-object"></a>シナリオ 4: ドライバーは、新しいメモリオブジェクトを使用する i/o 要求を発行します。


フレームワークには、基になるバッファーのソースに応じて、ドライバーが新しいメモリオブジェクトを作成するための3つの方法が用意されています。 詳細については、「[メモリバッファーの使用](using-memory-buffers.md)」を参照してください。

バッファーがフレームワークまたはドライバーによって作成された[ルックアサイドリスト](using-memory-buffers.md#using-lookaside-lists)から割り当てられている場合、メモリオブジェクトはバッファーを所有しているため、メモリオブジェクトが存在する限り、バッファーポインターは有効なままです。 非同期 i/o 要求を発行するドライバーでは、メモリオブジェクトによって所有されているバッファーを常に使用する必要があります。これにより、i/o 要求が発行元ドライバーに戻されるまでバッファーが保持されるようにすることができます。

以前に割り当てられたバッファーを、ドライバーが[**Wdfmemorycreatepreallocated**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)割り当てを呼び出すことによって新しいメモリオブジェクトに割り当てた場合、メモリオブジェクトはバッファーを所有しません。 この場合、メモリオブジェクトの有効期間と基になるバッファーの有効期間は関連していません。 ドライバーは、バッファーの有効期間を管理する必要があり、無効なバッファーポインターを使用しないようにする必要があります。

## <a name="scenario-5-driver-reuses-a-request-object-that-it-created"></a>シナリオ 5: ドライバーは、作成した要求オブジェクトを再利用します。


ドライバーは、作成した要求オブジェクトを再利用できますが、再利用する前に[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)を呼び出すことによって、このようなオブジェクトを再初期化する必要があります。 詳細については、「[フレームワークの要求オブジェクト](reusing-framework-request-objects.md)の再利用」を参照してください。

要求オブジェクトを再初期化するサンプルコードについては、KMDF リリースで提供されている[トースター](https://go.microsoft.com/fwlink/p/?linkid=256195)と[NdisEdge](https://go.microsoft.com/fwlink/p/?linkid=256154)のサンプルを参照してください。









