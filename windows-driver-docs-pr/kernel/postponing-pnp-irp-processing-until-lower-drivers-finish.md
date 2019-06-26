---
title: 下位のドライバーが完了するまで PnP IRP 処理を延期する
description: 下位のドライバーが完了するまで PnP IRP 処理を延期する
ms.assetid: 5bd9f3aa-30d5-4c45-afec-3e5ae0264f4a
keywords:
- WDK カーネルの PnP IRP の処理を延期すること、
- IRP の処理を延期するプラグ アンド プレイの WDK のカーネル
- WDK PnP Irp
- I/O 要求パケット PnP WDK
- 処理 WDK PnP IRP を延期しています
- 処理 WDK PnP IRP の遅延
- DispatchPnP ルーチン
- IoCompletion ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b728f295412af77dc652289ae4c5c12c82323fd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369700"
---
# <a name="postponing-pnp-irp-processing-until-lower-drivers-finish"></a>下位のドライバーが完了するまで PnP IRP 処理を延期する





いくつか PnP ドライバー パッケージとデバイスの親のバス ドライバー、続いてデバイス スタックの上位の各ドライバー、電源 Irp を最初処理する必要があります。 たとえば、親のバス ドライバーがデバイスの場合は、その開始操作を実行する最初のドライバーをする必要があります ([**IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))、その後に各次に高いドライバー。 関数とフィルター ドライバーが I/O 完了ルーチンを設定する必要があります、このような IRP には、次の下位のドライバーに IRP を渡すし、下位のドライバーが IRP に完了するまで、IRP を処理するすべてのアクティビティを延期します。

[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRQL ディスパッチでルーチンを呼び出すことができます\_レベルでは、関数またはフィルター ドライバーは、IRQL で IRP を処理する必要があります = パッシブ\_レベル。 パッシブに戻る\_からレベル、 *IoCompletion* 、日常的なドライバーはカーネル イベントを使用できます。 ドライバーのレジスタを*IoCompletion*カーネル モード イベントが設定されたルーチンと、ドライバーが内のイベントで待機し、その[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 イベントが設定されている場合は、下位のドライバーは IRP を完了したし、ドライバーが IRP を処理できます。

ドライバーが低いドライバー power IRP の完了を待機するでこの手法を使用する必要がありますしないことに注意してください ([**IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power))。 内のイベントを待機している、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンで設定されている、 *IoCompletion*ルーチン デッドロックが発生することができます。 参照してください[Power Irp を渡して](passing-power-irps.md)詳細についてはします。

次の 2 つの図は、PnP IRP の完了に下位のドライバーのドライバーが待機する方法の例を示します。 この例では、どのような関数とバス ドライバーする必要がありますに加えて、PnP マネージャーや I/O マネージャーとやり取りする方法を示します。

![第 1 部の処理を延期するプラグ アンド プレイ irp を示す図](images/delay1.png)

次のノートは、前の図の丸の番号に対応しています。

1.  PnP マネージャーでは、マネージャーにデバイス スタックの最上位のドライバーは IRP を送信する、I/O を呼び出します。

2.  I/O マネージャーの呼び出し、 *DispatchPnP*上のドライバーの日常的な。 この例では、デバイス スタック (関数ドライバーと親のバス ドライバー) の 2 つのドライバーがあるし、関数ドライバーは、最上位ドライバー。

3.  関数ドライバーが宣言しカーネル モード イベントを初期化します、次の下位のドライバーのスタックの場所を設定および設定、 *IoCompletion*この IRP のルーチンです。

    関数のドライバーを使用して[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)スタックの場所を設定します。

    呼び出しで[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)、関数のドライバー セット*InvokeOnSuccess*、 *InvokeOnError*、および*InvokeOnCancel*に**TRUE**し、コンテキスト パラメーターの一部として、カーネル モード イベントを渡します。

4.  関数のドライバーが使用してデバイス スタックを IRP を渡す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRP を処理するために、操作を実行する前にします。

5.  I/O マネージャー デバイス スタックの次の下位のドライバーを呼び出してドライバーの IRP を送信する*DispatchPnP*ルーチン。

6.  この例では、次の下位ドライバーは、デバイス スタック、親のバス ドライバーで最も低いドライバーです。 バス ドライバーは、デバイスを開始するには、その操作を実行します。 バス ドライバーのセット**Irp -&gt;IoStatus.Status**、設定**Irp -&gt;IoStatus.Information**場合、この IRP に関連する IRP を呼び出すことで完了と[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。

    バス ドライバーでは、他のドライバーのルーチンを呼び出してまたはそれを開始するには、デバイスに I/O を送信、バス ドライバーが完了しない場合の PnP IRP の*DispatchPnP*ルーチン。 保留中の IRP でをマークする必要があります代わりに、 [ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)状態を返すと\_から PENDING その*DispatchPnP*ルーチン。 ドライバーを後で呼び出す**IoCompleteRequest**から別のドライバーのルーチン、DPC ルーチン可能性があります。

次の図は、デバイス スタックの上位のドライバーが IRP、延期されたこれらの処理を再開の例では、2 番目の部分を示しています。

![処理、第 2 部を延期するプラグ アンド プレイ irp を示す図](images/delay2.png)

次のノートは、前の図の丸の番号に対応しています。

1.  バス ドライバーを呼び出すと**IoCompleteRequest**、I/O マネージャーが、ドライバーのスタックの場所に調べいずれかを呼び出す*IoCompletion*見つけたルーチン。 この例では、I/O マネージャーが検索し、呼び出します、 *IoCompletion*関数ドライバー、ドライバーが次に高いのルーチンです。

2.  関数のドライバーの*IoCompletion*ルーチンは、コンテキスト パラメーターで指定されたカーネル モード イベントを設定し、状態を返します\_詳細\_処理\_必要な作業です。

    IoCompletion ルーチンは、状態を返す必要があります\_詳細\_処理\_I/O マネージャーを呼び出し元に防ぐために必要な作業*IoCompletion*ルーチンがこの時点で、ドライバーによって設定します。 *IoCompletion*ルーチンでは、この状態を使用して、そのため完了が呼び出されないように、ドライバーの*DispatchPnP*ルーチンを抑制します。 I/O マネージャーは上位のドライバーの呼び出しを再開*IoCompletion*この IRP のルーチンときにこのドライバーの*DispatchPnP*ルーチンが IRP を完了します。

3.  I/O マネージャーが IRP の完了を停止し、呼び出されるルーチンに制御を戻します**IoCompleteRequest**、この例では、バス ドライバーの*DispatchPnP*ルーチン。

4.  バス ドライバーを返します、 *DispatchPnP* IRP の処理の結果を示すステータスの日常的な: いずれかの状態\_成功またはエラー状態です。

5.  **保留**をこの例では、関数のドライバーは、その呼び出し元に制御を戻します*DispatchPnP*ルーチン。

6.  関数のドライバーの*DispatchPnP*ルーチンが IRP の処理を再開します。

    場合**保留**ステータスを返します\_、PENDING、 *DispatchPnP*ルーチンには、前に実行が再開その*IoCompletion*ルーチンが呼び出されました。 *DispatchPnP*したがって、ルーチンがカーネル イベントによって通知を待機する必要があります、 *IoCompletion*ルーチン。 これにより、 *DispatchPnP*ルーチンは下のすべてのドライバーでは、これが完了するまで、IRP の処理を続行できません。

    場合**Irp -&gt;IoStatus.Status**設定されている下位のドライバーには、エラーに IRP が失敗したし、関数ドライバーでは、(を除くすべての必要なクリーンアップ) IRP の処理は続行する必要があります。

7.  下位のドライバーは IRP を正常に完了が、関数のドライバーは IRP を処理します。

    Irp のによって処理されている最初に親バス ドライバー、バス ドライバー通常設定正常な状態**Irp -&gt;IoStatus.Status**オプションの値を設定および**Irp-&gt;IoStatus.Information**します。 関数とフィルター ドライバーの値のままに**IoStatus** IRP が失敗した限りです。

    関数のドライバーの*DispatchPnP*ルーチンの呼び出し**IoCompleteRequest** IRP を完了します。 I/O マネージャーは、I/O 完了処理を再開します。 この例で、関数のドライバーと以上のための上のフィルター ドライバーがない*IoCompletion*ルーチンを呼び出します。 ときに**IoCompleteRequest**関数ドライバーにコントロールを返します*DispatchPnP* 、ルーチン、 *DispatchPnP*ルーチンがステータスを返します。

一部の Irp の関数またはフィルター ドライバーが IRP がデバイス スタックをバックアップする方法が失敗した場合、PnP マネージャーは下位のドライバーを通知します。 たとえば、関数またはフィルター ドライバーが失敗した場合、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)、PnP マネージャーに送信、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)デバイス スタックにします。

 

 




