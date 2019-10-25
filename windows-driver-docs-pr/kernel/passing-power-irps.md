---
title: 電源 Irp の受け渡し
description: 電源 Irp の受け渡し
ms.assetid: 01473eb0-ae60-4a95-9ae7-97b2b982d3d1
keywords:
- 電源 Irp WDK カーネル、成功
- Irp をデバイススタック WDK に渡す
- DispatchPower ルーチン
- ディスパッチルーチン WDK 電源管理
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: de8f938e955f5f8ef06170009c9ddb71afa36c5a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838515"
---
# <a name="passing-power-irps"></a>電源 Irp の受け渡し





電源の遷移が正常に管理されるようにするには、デバイススタックのすべての方向に、電力の Irp を渡す必要があります。 ドライバーは、IRP がデバイススタックを通過するときにデバイスの電源を短縮する IRP を処理します。 ドライバーは、IRP がデバイススタックをバックアップするときに[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンのデバイス電源を適用する irp を処理します。

次の図は、Windows 7 および Windows Vista で電源 IRP をデバイススタックに渡すためにドライバーが実行する必要がある手順を示しています。

![windows vista で電源 irp を渡す方法を示す図](images/passirpvista.png)

前の図に示すように、Windows 7 と Windows Vista では、ドライバーは次の操作を行う必要があります。

1.  Iocompletion のルーチンを設定する場合は[**Iocopyを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)呼び出し 、 *iocompletion*ルーチンを設定しない場合は[**ioskiplocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)呼び出します。

    これら2つのルーチンは、次に低いドライバーの IRP スタックの場所を設定します。 現在のスタック位置をコピーすることで、 *Iocompletion*ルーチンの実行時に、IRP スタックポインターが正しい場所に設定されるようになります。

    正しく記述されていないドライバーによって**Ioskipに**よって処理が失敗し、完了ルーチンが設定された場合、このドライバーは、その下のドライバーによって設定された完了ルーチンを上書きする可能性があります。

2.  Complete ルーチンが必要な場合は、 [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して*iocompletion*ルーチンを設定します。

3.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、IRP をスタック内の次の下位のドライバーに渡します。

次の図は、Windows Server 2003、Windows XP、および Windows 2000 で電源 IRP をデバイススタックに渡すためにドライバーが実行する必要がある手順を示しています。

![電源 irp を渡す (windows server 2003、windows xp、および windows 2000)](images/passirp.png)

前の図に示すように、ドライバーは次の操作を行う必要があります。

1.  ドライバーの種類によっては、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出すこともできます。 詳細については、「 [PoStartNextPowerIrp の呼び出し](calling-postartnextpowerirp.md)」を参照してください。

2.  Iocompletion のルーチンを設定する場合は[**Iocopyを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)呼び出し 、 *iocompletion*ルーチンを設定しない場合は[**ioskiplocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)呼び出します。

    これら2つのルーチンは、次に低いドライバーの IRP スタックの場所を設定します。 現在のスタック位置をコピーすることで、 *Iocompletion*ルーチンの実行時に、IRP スタックポインターが正しい場所に設定されるようになります。

3.  [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して*iocompletion*ルーチンを設定します。 *Iocompletion*ルーチンでは、ほとんどのドライバーは[PoStartNextPowerIrp を呼び出し](calling-postartnextpowerirp.md)て、次の電源 IRP を処理する準備ができていることを示します。

4.  [**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を呼び出して、IRP をスタック内の次の下位のドライバーに渡します。

    ドライバーは、システムが電源 Irp を適切に同期させるために、 **IoCallDriver** (他の irp の場合と同様) ではなく**pocalldriver**を使用する必要があります。 詳細については、「 [IoCallDriver の呼び出しと PoCallDriver の呼び出し](calling-iocalldriver-versus-calling-pocalldriver.md)」を参照してください。

*Iocompletion*ルーチンは、IRQL = ディスパッチ\_レベルで呼び出すことができることに注意してください。 したがって、ドライバーが IRQL = パッシブ\_レベルで IRP を終了した後に、追加の処理が必要な場合、ドライバーの完了ルーチンは作業項目をキューに置いて、ステータス\_より多くの\_処理を返す必要があり\_が必要です。 ワーカースレッドが IRP を完了する必要があります。

Windows 98/Me では、ドライバーは IRQL = パッシブ\_レベルで電源 Irp を完了する必要があります。

### <a name="do-not-change-the-function-codes-in-a-power-irp"></a>Power IRP の関数コードを変更しない

Irp の処理を制御する通常のルールに加えて、 [**irp\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)irp には次の特別な要件があります。電源 irp を受信するドライバーは、の i/o スタックの場所にあるメジャーおよびマイナー関数のコードを変更することはできません。電源マネージャーまたは上位レベルのドライバーによって設定された IRP。 これらの関数コードは、IRP が完了するまで変更されません。 この規則に違反すると、デバッグが困難な問題が発生する可能性があります。 たとえば、オペレーティングシステムが応答を停止したり、"ハング" したりする可能性があります。

### <a name="do-not-block-while-handling-a-power-irp"></a>電源 IRP の処理中にブロックしない

ドライバーでは、電源 Irp の処理中に長い遅延が発生しないようにする必要があります。

電源 IRP を渡す場合、ドライバーは、 **IoCallDriver** (windows 7 および windows Vista の場合) または**Pocalldriver** (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出した後、できるだけ早く[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから戻る必要があります. ドライバーは、カーネルイベントを待機したり、それ以外の場合はを返す前に遅延させたりすることはできません。 ドライバーが短時間に電源 IRP を処理できない場合は、状態\_PENDING を返し、電源 IRP が完了するまですべての受信 Irp をキューに入れます。 (この動作は、ブロックすることが許可されている PnP Irp と[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンの動作とは異なります)。

ドライバーが別のドライバーによる電源操作の待機をデバイススタックの下で待機する必要がある場合は、 *DispatchPower*ルーチンから状態\_PENDING を返し、電源 IRP の*iocompletion*ルーチンを設定する必要があります。 ドライバーは、 *Iocompletion*ルーチンで必要な任意のタスクを実行し、 **Postartnextpowerirp** (Windows SERVER 2003、Windows XP、および windows 2000 のみ) と[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。

たとえば、デバイスの電源ポリシー所有者は、通常、システム電源 IRP を保持しながらデバイスの電源 IRP を送信し、要求されたシステムの電源状態に適したデバイスの電源状態を設定します。

このような状況では、電源ポリシーの所有者がシステム電源 irp に*Iocompletion*ルーチンを設定し、その後のドライバーにシステム電源を渡し、 *DISPATCHPOWER*ルーチンから状態\_PENDING に戻す必要があります。

*Iocompletion*ルーチンでは、 **PoRequestPowerIrp**を呼び出してデバイスの電源 IRP を送信し、要求のコールバックルーチンへのポインターを渡します。 *Iocompletion*ルーチンは、必要な\_処理\_をより多く\_ステータスを返す必要があります。

最後に、ドライバーは、コールバックルーチンからシステム IRP を渡します。 ドライバーは、 *DispatchPower*ルーチン内のカーネルイベントを待機し、現在処理中の IRP の*iocompletion*ルーチンを使用してシグナルを送る必要があります。システムのデッドロックが発生する可能性があります。 詳細については、「[デバイスの電源ポリシー所有者におけるシステムセット-電源 IRP の処理](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)」を参照してください。

同様の状況で、システムがスリープ状態になると、電源ポリシーの所有者はデバイスの IRP を送信してデバイスの電源を切る前に、保留中の i/o を完了することが必要になる場合があります。 I/o が完了し、 *DispatchPower*ルーチンを待機しているときにイベントを通知するのではなく、ドライバーは作業項目をキューに置いて、 *DISPATCHPOWER*ルーチンから状態\_PENDING を返します。 ワーカースレッドでは、i/o が完了するまで待機してから、デバイスの電源 IRP を送信します。 詳細については、「 [**Ioallocateworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)」を参照してください。

 

 




