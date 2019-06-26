---
title: IoCompletion ルーチンの実装
description: IoCompletion ルーチンの実装
ms.assetid: 669860b1-5e85-4b28-a9b1-1ccf8c689b7a
keywords:
- IoCompletion ルーチン
- IoCompleteRequest ルーチン
- 優先順位の WDK Irp ブーストします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a38ec71556eac99cddf9ca99df5d2686e7785fca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365817"
---
# <a name="implementing-an-iocompletion-routine"></a>IoCompletion ルーチンの実装





開始時、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンを受け取る、*コンテキスト*ポインター。 ディスパッチ ルーチンを呼び出すと[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)を指定できます、*コンテキスト*ポインター。 このポインターは、すべてのドライバーが指定したコンテキスト情報を参照できます、 *IoCompletion*ルーチンが IRP を処理する必要があります。 ページング可能なコンテキストの領域であることに注意してください。 ため、 *IoCompletion* IRQL でルーチンを呼び出すことができます = ディスパッチ\_レベル。

**IoCompletion ルーチンに関する次の実装のガイドラインを考慮してください。**

-   *IoCompletion*ルーチンが IRP を確認できます[状態の I/O ブロック](i-o-status-blocks.md)I/O 操作の結果を判定します。

-   入力の IRP がディスパッチ ルーチンを使用して、によって割り当てられた場合[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)または[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)、 *IoCompletion*ルーチンを呼び出す必要があります[ **IoFreeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)元 IRP の完了前に可能であれば、その IRP を解放します。

    -   *IoCompletion*ルーチンが割り当てられた IRP がドライバーに割り当てられた、可能であれば、対応する IRP を解放する前に、ディスパッチ ルーチンには IRP あたりリソースの解放する必要があります。

        たとえば、ディスパッチ ルーチンは割り当てで MDL [ **IoAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl)と呼び出し[ **IoBuildPartialMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)のこれによって割り当てられる部分転送 IRP、 *IoCompletion*ルーチンと MDL をリリースする必要があります[ **IoFreeMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)します。 IRP が元の状態を維持するためにリソースを割り当てることがある場合にする必要がありますそれらのリソースを解放可能であればを呼び出す前に[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)元 IRP と確実に返す前にコントロール。

        一般に、解放または、IRP の完了前に、 *IoCompletion*ルーチンは、ディスパッチ ルーチンによって割り当てられた、IRP ごとのリソースを解放する必要があります。 ドライバーが前に解放するためのリソースについての状態を維持する必要がありますそれ以外の場合、その*IoCompletion*ルーチンでは、コントロールを返しますが、元の要求を完了します。

    -   場合、 *IoCompletion*ルーチンを完了できません状態が元の IRP\_成功した場合、原因となったドライバーに割り当てられた IRP の戻り値を元の IRP で状態の I/O ブロックを設定があります、  *。IoCompletion*ルーチンを元の要求は失敗します。

    -   場合、 *IoCompletion*ルーチンは、元の要求の状態を完了\_保留中、呼び出す必要があります[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)元 IRP に呼び出す前に**IoCompleteRequest**します。

    -   場合、 *IoCompletion*ルーチンがエラー状態で元の IRP に失敗する必要があります\_*XXX*、可能な[エラー ログに記録](logging-errors.md)します。 ただし、そのため、発生したデバイス I/O エラーをログに、基になるデバイス ドライバーの必要があります*IoCompletion*ルーチンは、通常はエラーをログしないようにします。

    -   ときに、 *IoCompletion*ルーチンは、コントロールの状態を返す必要があります、ルーチンが処理され、解放 IRP がドライバーに割り当てられた\_詳細\_処理\_必要な作業です。

        状態を返す\_詳細\_処理\_から必要な*IoCompletion*ルーチン forestalls I/O マネージャーの完了がドライバー割り当ておよび解放された IRP の処理します。 2 番目の呼び出し**IoCompleteRequest**原因 IRP の完了のルーチン、すぐ上に状態が返されましたルーチン完了ルーチンの以降の呼び出しを再開する I/O マネージャー\_複数\_処理\_必要な作業です。

-   場合、 *IoCompletion*ルーチンには、ドライバーを削減する 1 つまたは複数の要求を送信する受信の IRP が再利用されますまたは、どのようなコンテキストを更新する必要があります、日常的な再試行操作に失敗した場合、 *IoCompletion* 。各再利用性や IRP の再試行についてルーチンを保持します。 次の下位ドライバーの I/O スタックの場所、もう一度の呼び出しを設定し、 [ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)独自のエントリ ポイントと呼び出し[**保留** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRP の。

    -   *IoCompletion*ルーチンを呼び出す必要がありますいない[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)再利用または IRP の再試行ごとにします。

        ディスパッチ ルーチンには、元の IRP 保留中として既にマークされています。 チェーン内のすべてのドライバーで元の IRP の完了まで**IoCompleteRequest**、保留中のままにします。

    -   要求を再試行する前に、 *IoCompletion*ルーチンがステータスの I/O のステータスのブロックをリセットする必要があります\_の成功を**状態**の場合は 0 と**情報**、返されたエラー情報を保存した後可能性があります。

        各再試行のため、 *IoCompletion*日常的なは、通常、再試行カウントをデクリメント セット ディスパッチ ルーチンによって。 通常、 *IoCompletion*ルーチンを呼び出す必要があります**IoCompleteRequest** IRP をいくつかの限られた数の再試行が失敗したときに失敗します。

    -   *IoCompletion*ルーチンは、状態を返す必要があります\_詳細\_処理\_呼び出し後に必要な[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)と[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)されている IRP で再利用または再試行します。

        状態を返す\_詳細\_処理\_から必要な*IoCompletion*ルーチン forestalls I/O マネージャーの完了を再利用または再試行 IRP の処理します。

    -   場合、 *IoCompletion*ルーチンを完了できません状態が元の IRP\_成功すると、その必要がありますのままに状態の I/O ブロックにより、再利用性や再試行操作の下位のドライバーによって返される、  *。IoCompletion* IRP が失敗するルーチン。

    -   場合、 *IoCompletion*ルーチンは、元の要求の状態を完了\_保留中、呼び出す必要があります**IoMarkIrpPending**を呼び出す前に元の IRP に**IoCompleteRequest**します。
    -   場合、 *IoCompletion*ルーチンがエラー状態で元の IRP に失敗する必要があります\_*XXX*、可能な[エラー ログに記録](logging-errors.md)します。 ただし、そのため、発生したデバイス I/O エラーをログに、基になるデバイス ドライバーの必要があります*IoCompletion*ルーチンは、通常はエラーをログしないようにします。

-   設定するドライバー、 *IoCompletion* IRP し、パスで日常的な IRP が下位のドライバーに確認する必要があります、 **IRP -&gt;PendingReturned**フラグ、 *IoCompletion*ルーチン。 フラグが設定されている場合、 *IoCompletion*ルーチンを呼び出す必要があります**IoMarkIrpPending** IRP にします。 ただし、ドライバーは IRP を渡し、イベントを待機し、保留中の IRP がマークする必要がありますに注意してください。 代わりに、その*IoCompletion*ルーチンが、イベント通知し、状態を返す必要があります\_詳細\_処理\_必要な作業です。

-   *IoCompletion*ルーチンが可能であれば、前に元の IRP の処理に割り当てられたディスパッチ ルーチンにはリソースの解放する必要があります、 *IoCompletion*ルーチンの呼び出し**IoCompleteRequest**元 IRP と前に間違いなく、 *IoCompletion*ルーチンは、元の IRP の完了からコントロールを返します。

高度なドライバーを設定した場合、 *IoCompletion* 、元、そのドライバーの IRP で日常的な*IoCompletion*ルーチンはまで呼び出されません、 *IoCompletion*ルーチン下位レベルのすべてのドライバーが呼び出されています。

### <a name="supplying-a-priority-boost-in-calls-to-iocompleterequest"></a>IoCompleteRequest への呼び出しで優先順位を指定します。

呼び出す場合、最下位レベルのデバイス ドライバーは IRP のディスパッチ ルーチンで完了できます[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)で、 *PriorityBoost* IO の\_ありません\_増分値です。 ドライバーは元の要求者は、I/O 操作を完了するが待機しないことを想定できますので、実行時の優先順位の引き上げは必要ありません。

それ以外の場合、最下位レベルのドライバーは、システム定義とデバイスの種類に固有の値で、要求元がそのデバイスの I/O 要求の待機時間を補正するために、要求者の実行時の優先度の向上を提供します。 参照してください Wdm.h または Ntddk.h のブースト値。

高度なドライバーにも同じ*PriorityBoost*それぞれ基になるデバイス ドライバーの呼び出し時として**IoCompleteRequest**します。

### <a name="effect-of-calling-iocompleterequest"></a>IoCompleteRequest を呼び出すことの影響

ドライバーを呼び出すと**IoCompleteRequest**、I/O マネージャーがあるように設定する場合は、次のより高度なドライバーを呼び出す前に 0 でそのドライバーの I/O スタックの場所を入力、 *IoCompletion*ルーチンをIRP について呼び出されます。

高度なドライバーの*IoCompletion* IRP の I/O 状態ブロックだけを下位のすべてのドライバーを確認要求を処理するルーチンを確認できます。

呼び出し元**IoCompleteRequest**完了したばかりの IRP にアクセスしようとはする必要があります。 このような試行は、システムのクラッシュの原因となるプログラミング エラーです。

 

 




