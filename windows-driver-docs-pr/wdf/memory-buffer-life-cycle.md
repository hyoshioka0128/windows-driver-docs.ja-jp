---
title: メモリ バッファーのライフ サイクル
description: メモリ バッファーのライフ サイクル
ms.assetid: abf43bf5-a4a3-4aeb-9ec5-3458252933d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b33b3589b85adda19af69ec000e63499c7de84a6
ms.sourcegitcommit: e753fdd987a1bdbc4383704e18c2d81235fe9e05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65171945"
---
# <a name="memory-buffer-life-cycle"></a>メモリ バッファーのライフ サイクル


メモリ バッファーのライフ サイクルでは、バッファーの作成時に、削除からの時間にまたがります。 このトピックでは、バッファーの使用シナリオと、バッファーが削除された場合の影響について説明します。

カーネル モード ドライバー フレームワーク (KMDF) では、要求オブジェクトは、I/O 要求を表します。 すべての要求オブジェクトに関連付けられている 1 つ以上のメモリ オブジェクトと、各メモリ オブジェクトが入力に使用されるか、要求の出力をバッファーを表します。

フレームワークでは、受信の I/O 要求を表すオブジェクトを要求し、メモリを作成するときに要求オブジェクトが関連付けられているメモリ オブジェクトの親として設定します。 そのため、メモリ オブジェクトは、要求オブジェクトの有効期間を超えて保持できます。 フレームワーク ベースのドライバーには、I/O 要求が完了すると、フレームワークはこれら 2 つのオブジェクトへのハンドルが無効になるように、要求オブジェクトと、メモリ オブジェクトを削除します。

ただし、基になるバッファーでは異なります。 バッファー、バッファーとバッファーを作成する方法を作成するコンポーネントによって参照カウントがあり、メモリ オブジェクトによって所有される可能性があります-これがない場合もあります。 メモリ オブジェクトに、バッファーが所有している場合は、バッファーの参照カウントがし、その有効期間のメモリ オブジェクトの限定されます。 その他のいくつかのコンポーネントがバッファーを作成する場合、バッファーとメモリ オブジェクトの有効期間は関連しません。

フレームワーク ベースのドライバーは、I/O ターゲットに送信するための独自の要求オブジェクトを作成することもできます。 ドライバーが作成した要求は、ドライバーは、I/O 要求で受信した既存のメモリ オブジェクトを再利用できます。 ドライバーは、頻繁に I/O ターゲットに要求を送信できます[要求オブジェクトを再利用](reusing-framework-request-objects.md)を作成します。

要求オブジェクト、メモリ オブジェクト、および基になるバッファーの有効期間を理解することは、ドライバーはしないように、無効なハンドルまたはバッファー ポインターを参照する必要があります。

次の使用シナリオを検討してください。

-   シナリオ 1:[ドライバーは、KMDF から I/O 要求を受け取るし、処理するには、完了したら、その](#scenario-1-driver-receives-an-io-request-from-kmdf-handles-it-and-completes-it)します。
-   例 2:[ドライバーは、KMDF から I/O 要求を受け取るし、I/O をターゲットに転送](#scenario-2-driver-receives-an-io-request-from-kmdf-and-forwards-it-to-an-io-target)します。
-   例 3:[ドライバーは、既存のメモリ オブジェクトを使用する I/O 要求を発行](#scenario-3-driver-issues-an-io-request-that-uses-an-existing-memory-object)します。
-   シナリオ 4:[ドライバーは、新しいメモリ オブジェクトを使用する I/O 要求を発行します。](#scenario-4-driver-issues-an-io-request-that-uses-a-new-memory-object)
-   シナリオ 5:[ドライバーは、作成した要求オブジェクトを再利用します。](#scenario-5-driver-reuses-a-request-object-that-it-created)

## <a name="scenario-1-driver-receives-an-io-request-from-kmdf-handles-it-and-completes-it"></a>シナリオ 1:ドライバーは、KMDF から I/O 要求を受け取るを処理し、それを完了します。

最も単純なシナリオでは、KMDF は I/O を実行し、要求を完了すると、ドライバーへの要求をディスパッチします。 この場合は、基になるバッファーが作成された可能性がユーザー モード アプリケーションを別のドライバーまたはオペレーティング システム自体。 バッファーをアクセスする方法については、次を参照してください。 [Framework ベースのドライバーでのデータ バッファーへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff540701)します。

ときに、ドライバー[要求を完了](completing-i-o-requests.md)フレームワークは、メモリ オブジェクトを削除します。 バッファー ポインターは、し、無効です。

## <a name="scenario-2-driver-receives-an-io-request-from-kmdf-and-forwards-it-to-an-io-target"></a>例 2:ドライバーは、KMDF から I/O 要求を受信し、I/O をターゲットに転送します。

このシナリオでは、ドライバーで[要求を転送します](forwarding-i-o-requests.md)I/O のターゲットにします。 次のサンプル コードでは、どのドライバー入力方向の要求オブジェクトからメモリ オブジェクトへのハンドルを取得、I/O ターゲットに送信する要求を書式設定し、要求を送信を示します。

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

I/O のターゲットには、要求が完了したら、フレームワークは、ドライバーの設定要求の完了時のコールバックを呼び出します。 次のコードは、単純な完了コールバックを示しています。

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

ドライバーを呼び出すと[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)フレームワークを完了コールバックからには、メモリ オブジェクトを削除します。 ドライバーが取得されるメモリ オブジェクト ハンドルは、今すぐ無効です。

## <a name="scenario-3-driver-issues-an-io-request-that-uses-an-existing-memory-object"></a>例 3:ドライバーは、既存のメモリ オブジェクトを使用する I/O 要求を発行します。


一部のドライバーでは、独自の I/O 要求を発行し、I/O のターゲット オブジェクトで表される、I/O のターゲットに送ります。 ドライバーは、独自の要求オブジェクトを作成できますか、または[フレームワークが作成した要求オブジェクトを再利用](reusing-framework-request-objects.md)します。 ドライバーのいずれかの技法を使用して、前の要求からのメモリ オブジェクトが再利用できます。 ドライバーは、基になるバッファーを変更する必要がありますが、バッファーの新しい I/O 要求をフォーマットするときのオフセットを渡すことができます。

既存のメモリ オブジェクトを使用する新しい I/O 要求を書式設定する方法については、次を参照してください。[一般的な I/O ターゲットへの I/O 要求の送信](sending-i-o-requests-to-general-i-o-targets.md)します。

フレームワークは、I/O のターゲットに送信する要求を書式設定、ときに、I/O のターゲット オブジェクトの代わりにリサイクルされるメモリ オブジェクトの参照をかかります。 I/O のターゲット オブジェクトでは、次の操作のいずれかが発生するまで、この参照が保持されます。

-   要求が完了しました。
-   ドライバーを再フォーマット、要求オブジェクトもう一度の 1 つを呼び出すことによって、 *WdfIoTargetFormatRequestXxx*または*WdfIoTargetSendXxxSynchronously*メソッド。 これらのメソッドの詳細については、次を参照してください。 [Framework I/O ターゲット オブジェクトのメソッド](https://msdn.microsoft.com/library/windows/hardware/dn265644)します。
-   ドライバー呼び出し[ **WdfRequestReuse**](https://msdn.microsoft.com/library/windows/hardware/ff550026)します。

新しい I/O 要求が完了したら、フレームワークは、ドライバーは、この要求に設定する I/O 完了コールバックを呼び出します。 この時点では、I/O ターゲット オブジェクトは、メモリ オブジェクトの参照を保持するままにします。 そのため、I/O の完了時のコールバックで、ドライバー呼び出す必要があります[ **WdfRequestReuse** ](https://msdn.microsoft.com/library/windows/hardware/ff550026)の要求のドライバーが作成したオブジェクトのメモリを取得する元となる、元の要求を完了する前にオブジェクト。 ドライバーが要求されていない場合**WdfRequestReuse**、余分な参照が原因のバグ チェックが行われます。

## <a name="scenario-4-driver-issues-an-io-request-that-uses-a-new-memory-object"></a>シナリオ 4:ドライバーは、新しいメモリ オブジェクトを使用する I/O 要求を発行します。


フレームワークは、基になるバッファーのソースに応じて、新しいメモリ オブジェクトを作成するドライバーの 3 つの方法を提供します。 詳細については、次を参照してください。[メモリ バッファーを使用して](using-memory-buffers.md)します。

バッファーが割り当てられている、フレームワークによって、またはドライバー作成から[ルック アサイド リスト](using-memory-buffers.md#using-lookaside-lists)、メモリ オブジェクトが所有しているバッファー、バッファー ポインターは、メモリ オブジェクトが存在する限り有効です。 非同期 I/O 要求を発行するドライバーは、フレームワークは発行元のドライバーに、I/O 要求が完了するまで、バッファーを保持することを確認するためにメモリ オブジェクトによって所有されているバッファーを常に使用する必要があります。

場合は、ドライバーによって新しいメモリ オブジェクトを呼び出すことによって以前に割り当てられたバッファーが割り当てられます。 [ **WdfMemoryCreatePreallocated**](https://msdn.microsoft.com/library/windows/hardware/ff548712)、メモリ オブジェクトは、バッファーを所有していません。 この場合、メモリ オブジェクトの有効期間と基になるバッファーの有効期間は関連しません。 無効なバッファー ポインターを使用しよう必要があり、ドライバーは、バッファーの有効期間を管理する必要があります。

## <a name="scenario-5-driver-reuses-a-request-object-that-it-created"></a>シナリオ 5:ドライバーは、作成した要求オブジェクトを再利用します。


ドライバーは、作成する要求オブジェクトを再利用できますが、呼び出すことによってこのような各オブジェクトを再初期化する必要がありますが、 [ **WdfRequestReuse** ](https://msdn.microsoft.com/library/windows/hardware/ff550026)ごとの再利用する前にします。 詳細については、次を参照してください。 [Framework 要求オブジェクトを再利用](reusing-framework-request-objects.md)します。

要求オブジェクトを再初期化するサンプル コードについては、[トースター](https://go.microsoft.com/fwlink/p/?linkid=256195)と[NdisEdge](https://go.microsoft.com/fwlink/p/?linkid=256154) KMDF で提供されるサンプルのリリースします。









