---
title: I/O 要求の例 - 詳細
description: I/O 要求の例 - 詳細
ms.assetid: 480db6a1-2a13-4f1a-87ff-c3bd37aa79be
keywords:
- I/o スタックの場所 (WDK カーネル)
- 階層型ドライバーの IRP 処理 (WDK カーネルを)
- スタックの場所 (WDK カーネル)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e07f56c44cc326b0a664eb97f4c7562575a9dbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836728"
---
# <a name="example-io-request---the-details"></a>I/O 要求の例 - 詳細


## <a href="" id="ddk-example-i-o-request---the-details-kg"></a>


ファイルオブジェクトを開くことを示す図は、2つの i/o スタック位置を持つ IRP を示していますが、特定の要求を処理する階層化ドライバーの数によっては、IRP は任意の数の i/o スタックの場所を持つことができます。

次の図は、[[ファイルオブジェクトを開く](example-i-o-request---an-overview.md)] のドライバーで i/o サポートルーチン (**Io * Xxx*** ルーチン) を使用して、読み取りまたは書き込みの要求に対して IRP を処理する方法をより詳しく説明しています。

![階層化されるドライバーでの処理の irp を示す図](images/2girpeg.png)

1. I/o マネージャーは、サブシステムの読み取り/書き込み要求に割り当てられた IRP を使用して、ファイルシステムドライバー (FSD) を呼び出します。 FSD は、IRP 内の i/o スタックの場所にアクセスして、実行する操作を決定します。

2. FSD は、1回以上の i/o サポートルーチン ([**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)) を呼び出して追加の irp を割り当てることにより、元の要求を小さな要求 (場合によっては複数のデバイスドライバー) に分割できます。 追加の Irp が、下位レベルのドライバーに対してゼロで埋められた i/o スタック位置を持つ FSD に返されます。 必要に応じて、FSD は、前の図に示すように、元の irp を割り当てるのではなく、元の irp を再利用することができます。これは、元の IRP で次の下位のドライバーの i/o スタック位置を設定し、それを下位のドライバーに渡すことによって行います。

3. 前の図の FSD は、ドライバーによって割り当てられたそれぞれの IRP について、FSD が提供する完了ルーチンを登録するための i/o サポートルーチンを呼び出します。完了ルーチンでは、FSD が下位のドライバーが要求を満たしているかどうかを判断し、ドライバーが割り当てられている各 IRP が下位のドライバーによって完了したときに解放することができます。 I/o マネージャーは、ドライバーで割り当てられた各 IRP が正常に完了したか、エラー状態で完了したか、または取り消されたかどうかにかかわらず、FSD が提供する完了ルーチンを呼び出します。 上位レベルのドライバーは、割り当てられているすべての Irp を解放し、下位レベルのドライバーに代わって設定を行います。 I/o マネージャーは、すべてのドライバーが完了した後に割り当てられる Irp を解放します。

   次に、FSD は、次の下位のドライバーの要求を設定するために、次の下位レベルのドライバーの i/o スタックの場所にアクセスするために i/o サポートルーチン ([**Iogetnextiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)ドの場所) を呼び出します。 (前の図では、次の下位のドライバーは最下位レベルのドライバーになります)。次に、FSD は i/o サポートルーチン ([**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)) を呼び出して、その IRP を次の下位のドライバーに渡します。

4. これが IRP で呼び出されると、最下位レベルのドライバーは、i/o スタックの場所を調べて、ターゲットデバイスで実行する必要がある ( **IRP\_MJ\_* XXX*** 関数コードによって示される) 操作を判別します。 ターゲットデバイスは、指定された i/o スタックの場所にあるデバイスオブジェクトによって表され、IRP と共にドライバーに渡されます。 最下位レベルのドライバーでは、i/o マネージャーが irp を、 **irp\_MJ\_* XXX*** 操作用に定義されているエントリポイントにルーティングしたと仮定できます (ここでは、 [**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[**IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)) と、上位レベルのドライバーが要求の他のパラメーターの有効性をチェックしていることを確認します。

   上位レベルのドライバーがない場合、最下位レベルのドライバーは、 **IRP\_MJ\_* XXX*** 操作の入力パラメーターが有効かどうかを確認します。 そのような場合、ドライバーは通常、i/o サポートルーチンを呼び出して、デバイスの操作が IRP で保留されていることを i/o マネージャーに伝えます。また、IRP をキューに入れたり、ターゲットデバイスにアクセスする別のドライバー提供のルーチンに渡したりします (こちらを参照してください)。物理デバイスまたは論理デバイス (ディスクまたはディスク上のパーティション)。

5. I/o マネージャーは、ドライバーがターゲットデバイスに対して別の IRP の処理を既にビジー状態になっているかどうかを判断し、IRP が存在する場合はキューに登録し、を返します。 それ以外の場合、i/o マネージャーは、デバイス上で i/o 操作を開始するドライバー提供のルーチンに、IRP をルーティングします。 (この段階では、前の図の両方のドライバーと i/o マネージャーが制御を返します)。

6. デバイスで割り込みが行われた場合、ドライバーの割り込みサービスルーチン (ISR) は、デバイスが中断されないようにし、操作に必要なコンテキストを保存する必要があるため、非常に多くの作業を行います。 次に、ISR は、IRP を使用して i/o サポートルーチン ([**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)) を呼び出し、要求された操作を isr よりも低いハードウェア優先度で完了するように、IRP をキューに置いています。

7. ドライバーの DPC が制御を取得すると、コンテキスト (ISR の[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)への呼び出しで渡されます) を使用して i/o 操作を完了します。 DPC はサポートルーチンを呼び出して、次の IRP (存在する場合) をデキューし、その IRP を、デバイスで i/o 操作を開始するドライバー提供のルーチンに渡します (手順5を参照)。 次に、DPC は、IRP の i/o 状態ブロック内の完了した操作に関する状態を設定し、それを[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)と共に i/o マネージャーに返します。

8. I/o マネージャーは、IRP 内の最下位レベルのドライバーの i/o スタックの場所をゼロにし、ファイルシステムの登録完了ルーチンを呼び出します (手順3を参照)。これは、FSD によって割り当てられる IRP です。 この完了ルーチンは、i/o 状態ブロックを調べて、要求を再試行するか、元の要求について管理されている内部状態を更新するか、またはドライバーによって割り当てられた IRP を解放するかを判断します。 ファイルシステムは、下位レベルのドライバーに送信されるすべてのドライバーが割り当てられた Irp の状態情報を収集できます。これにより、i/o ステータスを設定し、元の IRP を完了できます。 ファイルシステムが元の IRP を完了すると、i/o マネージャーは i/o 操作の元の要求元 (サブシステムのネイティブ関数) に値を返します。

階層化された[ドライバーの処理 irp](#ddk-example-i-o-request---the-details-kg)に表示されるファイルシステムドライバーと同様に、既存のドライバーのチェーンに新しいドライバーを追加すると、次のすべてを実行できます。

-   独自の完了ルーチンを IRP に設定します。 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンは、i/o 状態ブロックを調べて、下位のドライバーが irp を正常に完了したか、irp をキャンセルしたか、またはエラーで完了したかを確認します。 また、この完了ルーチンは、ドライバーによって保存された可能性があるすべての IRP 固有の状態を更新したり、ドライバーが割り当てた可能性のある操作固有のリソースを解放したりすることもできます。 さらに、完了ルーチンは irp の完了を延期することができます (i/o マネージャーに対してより多くの処理が必要であることが通知されます)。また、irp の完了を許可する前に、次の下位レベルのドライバーに別の要求を送信することができます。

-   次の下位レベルのドライバーの i/o スタック位置を、割り当てられる Irp 内に設定し、要求を次の下位レベルのドライバーに送信します。

-   各 IRP で次の下位のドライバーの i/o スタックの場所を設定し、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すことにより、すべての受信要求を下位のドライバーに渡します。 (主要な関数コード[**irp\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)を持つ irp の場合、ドライバーは[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を使用する必要があることに注意してください)。

ドライバーによって作成された各デバイスオブジェクトは、特定のドライバーが i/o 要求を実行する物理デバイス、論理デバイス、または仮想デバイスを表します。 デバイスオブジェクトの作成と設定の詳細については、「[デバイスオブジェクトとデバイススタック](device-objects-and-device-stacks.md)」を参照してください。

階層化された[ドライバーの処理 irp](#ddk-example-i-o-request---the-details-kg)でも示されているように、ほとんどのドライバーは、ドライバーが提供するシステム定義の*標準ルーチン*のセットを通じて各 IRP を段階的に処理しますが、チェーン内のさまざまなレベルのドライバーは、必ず異なる標準ルーチン。 たとえば、最下位レベルのドライバーのみが物理デバイスからの割り込みを処理するので、下位レベルのドライバーのみが、ISR と、割り込みドリブン i/o 操作を完了する DPC を持つことになります。 一方、このようなドライバーは、デバイスから割り込みを受信したときに i/o が完了したことを認識しているため、完了ルーチンは必要ありません。 上位レベルのドライバーのみが、この図の FSD のような1つ以上の完了ルーチンを持つことになります。

 

 




