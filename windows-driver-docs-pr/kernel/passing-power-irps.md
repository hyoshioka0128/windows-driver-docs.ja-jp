---
title: 電源 IRP の受け渡し
description: 電源 IRP の受け渡し
ms.assetid: 01473eb0-ae60-4a95-9ae7-97b2b982d3d1
keywords:
- Irp WDK のカーネルの電源を渡す
- デバイス スタック WDK ダウン Irp を渡す
- DispatchPower ルーチン
- ディスパッチ ルーチン WDK の電源管理
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37f3b8a27ecb4bfe841504a4c3a96e65a6089be5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384744"
---
# <a name="passing-power-irps"></a>電源 IRP の受け渡し





Power Irp PDO power 遷移が正常に管理されていることを確認するには、デバイス スタックの一番下渡す必要があります。 ドライバーは IRP がデバイス スタックを通ってとデバイスの電源を削減する IRP を処理します。 ドライバーの処理でデバイスの電源が適用される IRP [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)デバイス スタックをバックアップとして IRP のルーチンが送信されます。

次の図は、ドライバーが Windows 7 および Windows Vista デバイス スタックを power IRP を通過するために必要な手順を示します。

![windows vista の電源 irp を渡してを示す図します。](images/passirpvista.png)

Windows 7 および Windows Vista で、前の図に示すよう、ドライバー、次の操作する必要があります。

1.  呼び出す[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を設定する場合、 *IoCompletion*ルーチンまたは[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を設定しない場合、 *IoCompletion*ルーチン。

    これら 2 つのルーチンでは、次の下位のドライバーの IRP スタックの場所を設定します。 IRP スタック ポインターが正しい場所に設定されているにより現在のスタックの場所をコピーするときに、 *IoCompletion*ルーチンの実行。

    不完全なドライバーが呼び出し元の間違いを行った場合**IoSkipCurrentIrpStackLocation**完了ルーチンを設定し、このドライバーは、下にあるドライバーによって設定完了ルーチンを上書き可能性があります。

2.  呼び出す[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)を設定する、 *IoCompletion*ルーチン、完全なルーチンが必要な場合。

3.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRP をスタック内の次の下位ドライバーに渡す。

次の図は、ドライバーが Windows Server 2003、Windows XP、および Windows 2000 でのデバイス スタックを power IRP を渡すために必要な手順を示します。

![電源の irp (windows server 2003、windows xp、および windows 2000) を渡してください。](images/passirp.png)

前の図に示すよう、ドライバー、次の操作する必要があります。

1.  によって、ドライバーの種類を呼び出す可能性[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)します。 詳細については、次を参照してください。[呼び出す PoStartNextPowerIrp](calling-postartnextpowerirp.md)します。

2.  呼び出す[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を設定する場合、 *IoCompletion*ルーチンまたは[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を設定しない場合、 *IoCompletion*ルーチン。

    これら 2 つのルーチンでは、次の下位のドライバーの IRP スタックの場所を設定します。 IRP スタック ポインターが正しい場所に設定されているにより現在のスタックの場所をコピーするときに、 *IoCompletion*ルーチンの実行。

3.  呼び出す[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)を設定する、 *IoCompletion*ルーチン。 *IoCompletion*ルーチン、ほとんどのドライバー [PoStartNextPowerIrp を呼び出す](calling-postartnextpowerirp.md)を IRP の [次へ] のパワーを処理する準備ができたことを示します。

4.  呼び出す[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) IRP をスタック内の次の下位ドライバーに渡す。

    ドライバーを使用する必要があります**PoCallDriver**、なく**保留**(とその他の Irp) に、システムが電源 Irp を正しく同期するようにします。 詳細については、次を参照してください。[保留を呼び出すとします。呼び出す PoCallDriver](calling-iocalldriver-versus-calling-pocalldriver.md)します。

注意して*IoCompletion* IRQL でルーチンを呼び出すことができます = ディスパッチ\_レベル。 そのため、ドライバーは IRQL で追加の処理を必要とする場合は、= パッシブ\_レベルより低いレベルのドライバーはドライバーの IRP では、使用が完了した後完了ルーチンが作業項目のキューし、状態を返します\_詳細\_処理\_必要な作業です。 ワーカー スレッドは IRP を完了する必要があります。

Windows 98 では、ドライバーが完了する必要があります/IRQL で Irp の電源をパッシブ =\_レベル。

### <a name="do-not-change-the-function-codes-in-a-power-irp"></a>電源 IRP の関数コードを変更しないでください。

Irp の処理を制御する通常の規則だけでなく[ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) Irp に次の特別な要件があります。累乗を受け取るドライバー IRP では、I/O スタック内の場所に IRP 電源マネージャーによって、またはより高度なドライバーに設定されているメジャーおよびマイナーの関数コードを変更しないでください。 電源マネージャーは IRP が完了するまでそのまま残り、これらの関数コードに依存します。 この規則の違反をデバッグするが困難な問題が発生することができます。 たとえば、オペレーティング システムを応答を停止または「ハング」可能性があります。

### <a name="do-not-block-while-handling-a-power-irp"></a>電源 IRP の処理中にブロックしないで

ドライバーは、電源 Irp の処理中に長時間の遅延を発生しない必要があります。

IRP の電源を渡して、ドライバーから返す必要があります、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)呼び出した後、できるだけ早くルーチン**保留**(Windows 7、Windows Vista で)または**PoCallDriver** (Windows Server 2003、Windows XP、Windows 2000 で)。 ドライバーのカーネル イベントを待機またはそれ以外の場合に返す前に遅延する必要がありますされません。 ドライバーが power IRP を短い時間で処理できない場合の状態が返されます。\_PENDING を電源 IRP が完了するまでのすべての着信 Irp のキューに登録します。 (この動作は PnP Irp の場合と異なることに注意してくださいと[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンでは、ブロックすることができる)。

状態が返されます場合は、ドライバーは、デバイス スタックを別のドライバーをさらにして電源操作を待機する必要があります、\_PENDING からその*DispatchPower*ルーチンと設定、 *IoCompletion*電源 IRP のルーチンです。 ドライバーで必要なタスクを実行できます、 *IoCompletion*ルーチンと呼び出して**PoStartNextPowerIrp** (Windows Server 2003、Windows XP、および Windows 2000 のみ) と[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。

たとえば、デバイスの電源ポリシー所有者は、要求されたシステムの電源状態の適切なデバイスの電源状態を設定するには、システム電源 IRP を押しながら IRP のデバイスの電源を通常送信します。

このような状況で電源ポリシーの所有者を設定する必要があります、 *IoCompletion* IRP の電源をシステム電源 IRP を次の下位ドライバーに渡す、および状態を返す、システム内のルーチン\_PENDING からその*DispatchPower*ルーチン。

*IoCompletion*ルーチンを呼び出す**PoRequestPowerIrp**デバイスの電源のポインターを要求にコールバック ルーチンに渡す IRP を送信します。 *IoCompletion*ルーチンは、状態を返す必要があります\_詳細\_処理\_必要な作業です。

最後に、ドライバーは IRP のシステムをコールバック ルーチンから渡します。 ドライバーでのカーネル イベントを待つ必要がありますいないその*DispatchPower*ルーチンおよびのシグナル、 *IoCompletion* IRP の日常的なことは、現在処理; システム デッドロックが発生する可能性があります。 詳細については、次を参照してください。[電源ポリシー所有者のデバイスでシステム セット Power IRP の処理](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)します。

同様の状況では、システムがスリープ状態にするときに電源ポリシーの所有者が IRP のデバイスのデバイスの電源を送信するには、I/O の保留中の一部を完了する必要があります。 I/O が完了するときにイベントをシグナル通知とで待機しているのではなく、 *DispatchPower* 、日常的なドライバーする必要があります、作業項目をキューし、状態を返す\_から PENDING、 *DispatchPower*ルーチンです。 ワーカー スレッドでは、I/O の完了を待機して、IRP のデバイスの電源を送ります。 詳細については、次を参照してください。 [ **IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)します。

 

 




