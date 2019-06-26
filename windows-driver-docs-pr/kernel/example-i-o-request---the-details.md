---
title: I/O 要求の例 - 詳細
description: I/O 要求の例 - 詳細
ms.assetid: 480db6a1-2a13-4f1a-87ff-c3bd37aa79be
keywords:
- I/O スタックの場所の WDK カーネル
- 階層化ドライバー IRP の処理の WDK カーネル
- スタックの場所の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27dc594d26435f5b1d71a9542c57c837dd5106ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385118"
---
# <a name="example-io-request---the-details"></a>I/O 要求の例 - 詳細


## <a href="" id="ddk-example-i-o-request---the-details-kg"></a>


ファイル オブジェクトを開く方法を示す図は、I/O スタックの 2 つの場所で IRP を示していますが、IRP がレイヤード ドライバーの数は、特定の要求を処理することによって、I/O スタックの場所の任意の数を持つことができます。

次の図は、さらに詳しく示す方法でドライバー、[ファイル オブジェクトを開く](example-i-o-request---an-overview.md)図の使用 I/O サポート ルーチン (**Io * Xxx*** ルーチン) または書き込み要求を読み取り、IRP を処理します。

![階層型ドライバーで処理 irp を示す図](images/2girpeg.png)

1. I/O マネージャーは、サブシステムの読み取り/書き込み要求の割り当て済みの IRP で、ファイル システム ドライバー (FSD) を呼び出します。 FSD は IRP を実行するどのような操作を決定するまでに、I/O スタックの場所にアクセスします。

2. FSD は I/O サポート ルーチンを呼び出すことで (場合によっては、複数のデバイス ドライバー) の小さな要求に元の要求を分割することができます ([**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)) 追加 Irp を割り当てることの 1 つ以上の時間。 追加の Irp がドライバーの下位レベルの I/O スタック ロケーションをゼロで埋められますと FSD へ返されます。 でもその裁量において、FSD はによって元の IRP で、次の下位ドライバーの I/O スタックの場所を設定し、下位のドライバーに渡す前の図に示すように、割り当ての追加 Irp ではなく、元の IRP を再利用できます。

3. 各ドライバーに割り当てられた IRP の図の前の呼び出し、I/O で FSD が FSD が指定した完了ルーチンでは; を登録するルーチンをサポートします。完了ルーチンで FSD は下位のドライバーが要求を満たすかどうかを調べるし、下位のドライバーが完了した場合に、各ドライバーに割り当てられた IRP を解放できます。 各ドライバーに割り当てられた IRP が正常に完了しました、エラー状態では、正常に完了または取り消されたかどうか、I/O マネージャーは FSD が指定した完了ルーチンを呼び出します。 高度なドライバーは、割り当てし、自身が代理として低レベルのドライバーの設定、Irp を解放します。 I/O マネージャー解放 Irp を割り当てた後は、すべてのドライバーが完了しました。

   次に、FSD が I/O サポート ルーチンを呼び出します ([**IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation))、次の下位のドライバーの要求を設定するには、次の下位レベルのドライバーの I/O スタックの場所にアクセスします。 (前の図では、[次へ] の下位のドライバーたまたま、最下位レベルのドライバーです。)FSD を呼び出して I/O サポート ルーチン ([**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)) を次の下位ドライバーには、その IRP を渡します。

4. 最下位レベルのドライバーがどのような操作を決定する、I/O スタックの場所を確認します IRP が呼び出されると、(によって示される、 **IRP\_MJ\_* XXX*** 関数コード)、ターゲット デバイスに実施する必要があります。 ターゲット デバイスは、I/O スタックに関する指定された位置にデバイス オブジェクトによって表されるされ、ドライバーに IRP に渡されます。 最下位レベルのドライバーでは、I/O マネージャーが IRP のドライバーが定義されているエントリ ポイントがルーティングされると想定できます、 **IRP\_MJ\_* XXX*** 操作 (ここで[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)) より高度なドライバーがの有効性をチェック要求の他のパラメーター。

   最下位レベルのドライバーが確認はより高度なドライバーがない場合、かどうかの入力パラメーター、 **IRP\_MJ\_* XXX*** 操作は無効です。 ドライバーが、通常はデバイス操作が保留中 I/O マネージャーに指示する I/O サポート ルーチンを呼び出す場合は、IRP でとを IRP のキューまたは (ここで、ターゲット デバイスにアクセスする他のドライバーが指定したルーチンに渡す、物理的または論理的デバイス: ディスクまたはディスクのパーティション)。

5. I/O マネージャーは、ドライバーがキュー IRP が、返されるその場合、ターゲット デバイスのもう 1 つの IRP の処理でビジー状態で既にかどうかを判断します。 それ以外の場合、I/O マネージャーは、そのデバイス上の I/O 操作を開始するドライバー指定のルーチンに IRP をルーティングします。 (この段階で、前の図および I/O マネージャーの両方のドライバー制御を戻す。)

6. デバイスが割り込み、ずっととして作業する必要がありますを中断することからデバイスを停止し、操作に関する必要なコンテキストを保存するだけで、ドライバーの割り込みサービス ルーチン (ISR) ことができます。 ISR を呼び出して I/O サポート ルーチン ([**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)) キューの優先順位の低いハードウェアで要求された操作を完了するドライバーによって提供される DPC (遅延プロシージャ コール) ルーチンに IRP にISR より

7. コンテキストを使用して、ドライバーの DPC がコントロールを取得すると (ISR の呼び出しで渡される[ **IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)) I/O 操作を完了します。 DPC (ある場合)、[次へ] の IRP をキューから削除して、ドライバー指定のルーチンに、デバイスの I/O 操作を開始するには、その IRP を渡すには、サポート ルーチンを呼び出すと (手順 5 を参照してください)。 DPC が IRP の I/O の状態のブロック内で完了したばかりの操作に関する状態を設定し、I/O マネージャーを返します[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。

8. I/O マネージャー ゼロ IRP の最下位レベルのドライバーの I/O スタックの場所とファイル システムの登録完了ルーチンを呼び出す (手順 3 を参照してください) FSD に割り当てられた IRP にします。 この完了ルーチンは、要求を再試行するまたは元の要求の管理、内部状態を更新して、ドライバーによって割り当てられた IRP を解放するかどうかを判断する I/O のステータスのブロックを確認します。 ファイル システムには、I/O の状態を設定し、元の IRP の完了を下位レベルのドライバーに送信しますすべてのドライバーに割り当てられた Irp の状態情報を収集できます。 ファイル システムが完了すると元の IRP では、I/O マネージャーを返し、I/O 操作の元の要求者 (サブシステムのネイティブ関数) の NTSTATUS 値。

示すように、ファイル システム ドライバーなど、[ドライバーでの Irp の処理](#ddk-example-i-o-request---the-details-kg)図に、既存のドライバーのチェーンに追加される新しいドライバーは、次のすべてを実行できます。

-   IRP に独自の完了ルーチンを設定します。 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンが下位のドライバーに IRP を正常に完了し、IRP をキャンセルや、エラーが発生したことかどうかを判断する I/O のステータスのブロックを確認します。 完了ルーチンの IRP 固有更新も、ドライバーが保存した状態のリリース、ドライバーが割り当てられている可能性がありますが、任意の操作に固有のリソースと IRP を完了する前など。 さらに、完了ルーチンでは、(通知 I/O マネージャー IRP でより多くの処理が必要です) を IRP の完了を延期することができ、IRP が完了するまでに許可する前に、[次へ] の下位レベルのドライバーを別の要求を送信できます。

-   Irp を割り当てることで、[次へ] の下位レベルのドライバーの I/O スタックの場所を設定し、[次へ] の下位レベルのドライバーに要求を送信します。

-   各 IRP と呼び出し元で、次の下位ドライバーの I/O スタックの場所を設定して、下位のドライバーに着信要求を渡す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。 (Irp の主要な関数のコードで注意[ **IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)、ドライバーを使用する必要があります[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver).)

各デバイスのドライバーが作成したオブジェクトは、特定のドライバーが I/O 要求を実行する物理、論理、または仮想デバイスを表します。 作成、デバイス オブジェクトの設定の詳細については、次を参照してください。[デバイス オブジェクトとデバイス スタック](device-objects-and-device-stacks.md)します。

として、[ドライバーでの処理の Irp](#ddk-example-i-o-request---the-details-kg)図も示していますが、ほとんどのドライバー処理各 IRP ドライバーによって提供される一連のシステム定義によって段階的*標準ルーチン*でさまざまなドライバーが、チェーン内のレベルには、さまざまな標準ルーチンとは限りませんがあります。 たとえば、のみ、物理デバイスから最下位レベルのドライバー ハンドル割り込み、最下位レベルのドライバーのみになります ISR、DPC 割り込み駆動の I/O 操作を完了します。 その一方で、このようなドライバーは、そのデバイスからの割り込みを受け取ったときに I/O が完了したことを知っている、ため、不要になった完了ルーチン。 高度なドライバーのみでは、この図では、FSD のような完了ルーチンを 1 つ以上があります。

 

 




