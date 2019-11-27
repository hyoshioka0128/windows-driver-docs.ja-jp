---
title: IoCompletion ルーチンの実装
description: IoCompletion ルーチンの実装
ms.assetid: 669860b1-5e85-4b28-a9b1-1ccf8c689b7a
keywords:
- IoCompletion ルーチン
- IoCompleteRequest ルーチン
- 優先順位が WDK Irp をブースト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f01e1982cbd6ee44170eb383659682a83e9fce23
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828310"
---
# <a name="implementing-an-iocompletion-routine"></a>IoCompletion ルーチンの実装





入力時、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンは*コンテキスト*ポインターを受け取ります。 ディスパッチルーチンが[**Ioset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出すと、*コンテキスト*ポインターを提供できます。 このポインターは、 *Iocompletion*ルーチンが IRP を処理するために必要なドライバーによって決定されたコンテキスト情報を参照できます。 *Iocompletion*ルーチンを IRQL = DISPATCH\_レベルで呼び出すことができるため、コンテキスト領域をページングできないことに注意してください。

**IoCompletion ルーチンには、次の実装ガイドラインを考慮してください。**

-   *Iocompletion*ルーチンは、IRP の[i/o 状態ブロック](i-o-status-blocks.md)を確認して、i/o 操作の結果を判断できます。

-   入力 IRP が[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)または[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)を使用してディスパッチルーチンによって割り当てられた場合、 *Iocompletion*ルーチンは[**iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)を呼び出してその irp を解放する必要があります。これは、可能であれば、元のIRP.

    -   *Iocompletion*ルーチンは、ディスパッチルーチンによってドライバー割り当ての irp に割り当てられた irp リソース (可能であれば、対応する irp を解放する前に) を解放する必要があります。

        たとえば、ディスパッチルーチンが[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)を使用して MDL を割り当て、それによって割り当てられる部分転送の IRP に対して[**Iobuildpartialmdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)を呼び出す場合、 *Iocompletion*ルーチンは、 [**iofreemdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl)で mdl を解放する必要があります。 元の IRP に関する状態を維持するためにリソースを割り当てる場合は、そのリソースを解放する必要があります。つまり、元の IRP で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出す前に、制御を返す前に確実にそのリソースを解放する必要があります。

        一般に、IRP を解放または完了する前に、 *Iocompletion*ルーチンは、ディスパッチルーチンによって割り当てられた irp ごとのリソースを解放する必要があります。 それ以外の場合、ドライバーは解放されるリソースについての状態を維持してから、 *Iocompletion*ルーチンが元の要求の完了から制御を返すようにする必要があります。

    -   *Iocompletion*ルーチンが、状態\_SUCCESS の元の irp を完了できない場合、元の irp の i/o 状態ブロックを、ドライブに割り当てられた irp で返される値に設定する必要があります。これにより、 *iocompletion*ルーチンは、元の要求。

    -   *Iocompletion*ルーチンが、状態\_保留中の元の要求を完了する場合、 **IoCompleteRequest**を呼び出す前に、元の IRP で[**終了する iomarkirppを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)呼び出す必要があります。

    -   *Iocompletion*ルーチンが、エラー状態\_*XXX*で元の IRP を失敗させる必要がある場合は、[エラーをログに記録](logging-errors.md)できます。 ただし、発生したデバイス i/o エラーをログに記録するのは、基になるデバイスドライバーの役割であるため、 *Iocompletion*ルーチンは通常、エラーをログに記録しません。

    -   *Iocompletion*ルーチンが処理され、ドライバーによって割り当てられた IRP が解放されると、ルーチンは状態\_制御を返す必要があり\_処理\_必要があります。

        状態を返す\_、 *iocompletion*ルーチンから必要な\_処理\_の数が増え、i/o マネージャーによるドライバーの割り当ておよび解放された IRP の完了処理が forestalls ます。 **IoCompleteRequest**への2回目の呼び出しでは、i/o マネージャーが IRP の完了ルーチンの呼び出しを再開します。これは、\_状態を返したルーチンのすぐ上の完了ルーチンから開始し、\_処理\_必要があります.

-   *Iocompletion*ルーチンが受信 IRP を再利用して1つまたは複数の要求を下位のドライバーに送信した場合、またはルーチンが失敗した操作を再試行した場合は、 *iocompletion*ルーチンが再利用または再試行のたびに保持するすべてのコンテキストを更新する必要があります。IRP. その後、次の下位にあるドライバーの i/o スタックの場所をもう一度設定し、独自のエントリポイントを使用して[**IosetIoCallDriver ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出し、IRP に対してを呼び出します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

    -   *Iocompletion*ルーチンは、IRP の再利用または再試行のたびに[**Iomarkirpp終了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出さないでください。

        ディスパッチルーチンでは、元の IRP が保留中として既にマークされています。 チェーン内のすべてのドライバーが**IoCompleteRequest**を使用して元の IRP を完了するまでは、保留中のままになります。

    -   要求を再試行する前に、 *Iocompletion*ルーチンは、状態\_が "成功" に設定され、返されたエラー情報を保存した後、**情報** **が0の**i/o 状態ブロックをリセットする必要があります。

        再試行のたびに、 *Iocompletion*ルーチンは通常、ディスパッチルーチンによって設定された再試行回数を減らします。 通常、 *Iocompletion*ルーチンは、一部の再試行が失敗した場合に、IRP を失敗させるために**IoCompleteRequest**を呼び出す必要があります。

    -   [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出し、再利用または再試行される IRP で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出した後で、必要な\_処理\_より多くの処理を実行するために、 *iocompletion*ルーチンは状態\_返す必要があります。

        状態を返す\_、 *iocompletion*ルーチンから必要な\_処理\_の数が増えると、i/o マネージャーによる再利用または再試行中の IRP の完了処理が forestalls されます。

    -   *Iocompletion*ルーチンが、状態\_SUCCESS の元の IRP を完了できない場合は、 *IOCOMPLETION*ルーチンが IRP を失敗させる再利用または再試行操作のために、低いドライバーによって返された i/o 状態ブロックのままにする必要があります。

    -   *Iocompletion*ルーチンが、状態\_保留中の元の要求を完了する場合、 **IoCompleteRequest**を呼び出す前に、元の IRP で**終了する iomarkirppを**呼び出す必要があります。
    -   *Iocompletion*ルーチンが、エラー状態\_*XXX*で元の IRP を失敗させる必要がある場合は、[エラーをログに記録](logging-errors.md)できます。 ただし、発生したデバイス i/o エラーをログに記録するのは、基になるデバイスドライバーの役割であるため、 *Iocompletion*ルーチンは通常、エラーをログに記録しません。

-   IRP で*iocompletion*ルーチンを設定し、その後、irp を下位のドライバーに渡すドライバーは、 *iocompletion*ルーチンで**irp&gt;pendingreturned た**フラグをチェックする必要があります。 フラグが設定されている場合、 *Iocompletion*ルーチンは、IRP を使用して**Iomarkirpp終了**を呼び出す必要があります。 ただし、IRP を通過してイベントを待機するドライバーは、保留中の IRP をマークしないことに注意してください。 代わりに、その*Iocompletion*ルーチンはイベントを通知し、必要な\_処理\_より多くの状態\_返す必要があります。

-   *Iocompletion*ルーチンは、ディスパッチルーチンが元の irp を処理するために割り当てられたすべてのリソースを解放する必要があります。これは、 *iocompletion*ルーチンが元の irp で**IoCompleteRequest**を呼び出す前に、確実に*Iocompletion*ルーチンは、元の IRP の完了を制御します。

上位レベルのドライバーで、その*Iocompletion*ルーチンが元の IRP に設定されている場合、すべての下位レベルのドライバーの*iocompletion*ルーチンが呼び出されるまで、そのドライバーの*iocompletion*ルーチンは呼び出されません。

### <a name="supplying-a-priority-boost-in-calls-to-iocompleterequest"></a>IoCompleteRequest の呼び出しで優先度を上げる

最下位レベルのデバイスドライバーがディスパッチルーチンで IRP を完了できる場合は、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)が呼び出され、IO の優先*順位*が\_\_インクリメントはありません。 ドライバーでは、元の要求元が i/o 操作の完了を待機していないと見なすことができるため、実行時の優先順位の増加は必要ありません。

それ以外の場合、最下位レベルのドライバーは、要求元がデバイス i/o 要求を待機した時間を補正するために、要求元の実行時の優先順位を増幅するシステム定義のデバイスタイプ固有の値を提供します。 値をブーストするには、「Ntddk」または「」を参照してください。

上位レベルのドライバーでは、 **IoCompleteRequest**を呼び出すと、基になる各デバイスドライバーと同じ優先*順位ブースト*が適用されます。

### <a name="effect-of-calling-iocompleterequest"></a>IoCompleteRequest を呼び出した場合の影響

ドライバーが**IoCompleteRequest**を呼び出すと、i/o マネージャーは、そのドライバーの i/o スタック位置をゼロで埋め、次に高いレベルのドライバー (存在する場合) を呼び出してから、IRP に対して呼び出される*iocompletion*ルーチンを設定します。

上位レベルのドライバーの*Iocompletion*ルーチンは、IRP の i/o 状態ブロックだけをチェックし、下位のすべてのドライバーが要求を処理した方法を確認できます。

**IoCompleteRequest**の呼び出し元は、完了した IRP にアクセスしようとすることはできません。 このような試みは、システムがクラッシュする原因となるプログラミングエラーです。

 

 




