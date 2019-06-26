---
title: デバイス電源状態についての IRP_MN_QUERY_POWER の処理
description: デバイス電源状態についての IRP_MN_QUERY_POWER の処理
ms.assetid: 902619bc-068a-4613-b99d-78a243f7fee6
keywords:
- IRP_MN_QUERY_POWER
- デバイスの電源状態の WDK カーネル
- クエリ power Irp WDK の電源管理
- 電源 Irp WDK カーネル、デバイス クエリ
- 電源状態のクエリを実行します。
- キューの Irp
- デバイス クエリ power Irp WDK カーネル
- ディスパッチ ルーチン WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 027471da0c2e4b7889cc895ac97b1a03ce20ea88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383329"
---
# <a name="handling-irpmnquerypower-for-device-power-states"></a>IRP の処理\_MN\_クエリ\_電源状態のデバイスの電源





デバイス クエリ power IRP が 1 台のデバイスの状態の変更に関するクエリを実行およびデバイスのスタック内のドライバーのすべてに送信されます。 このような IRP を指定します**DevicePowerState**で、 **Power.Type** I/O スタックの場所のメンバー。

下位のスタックを移動する、ドライバーは Irp のクエリ機能を処理します。

関数またはフィルター ドライバーが失敗することが、 [ **IRP\_MN\_クエリ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)要求、次のいずれかが true のかどうか。

-   ウェイク アップのデバイスが有効にし、要求された電源の状態が、デバイスが、システムを起動状態下回る。 たとえば、D3 からではなく、D2 からのシステムをスリープ解除できるデバイス D3 のクエリが失敗するが、D2 のクエリが成功します。

-   要求された状態を入力することにより、開いているモデム接続などのデータが失われます操作を破棄するドライバー。 ドライバーことはほとんどありませんが失敗をクエリします。 このためほとんどの状況では、アプリケーションは、このような場合を処理します。

失敗する、 [ **IRP\_MN\_クエリ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)要求と、ドライバーは、次の手順。

1.  呼び出す[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)をドライバーが IRP の [次へ] のパワーを処理する準備が整っているかを示します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ。)

2.  設定**Irp -&gt;IoStatus.Status**障害状態と呼び出しに[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)、IO を指定する\_いいえ\_インクリメントします。 ドライバーは IRP デバイス スタックをさらに渡しません。

3.  エラー状態を返す、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

またはしない任意の操作を開始する必要があります、後続の成功した完了を妨げる他のアクションを実行、ドライバーには、クエリ性能 IRP が成功すると、 **IRP\_MN\_設定\_POWER**照会された電源の状態を要求します。

IRP が成功したドライバーの状態の照会や IRP、クエリを通過セット power IRP のよう準備する必要があります。

1.  すべて未処理の I/O 操作を完了します。

2.  キューの I/O 要求を受信します。

3.  指定された電源の状態への移行に支障をきたすを他の新しいアクティビティを開始しないでください。 ただし、ドライバーがデバイス コンテキストを保存しない、またはシャット ダウンに他の手順を実行する必要があります。

4.  呼び出す**IoCopyCurrentIrpStackLocationToNext**を次の下位のドライバーの IRP スタックの場所を設定します。

5.  設定、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン。 *IoCompletion* 、ルーチンの呼び出し**PoStartNextPowerIrp** (Windows Server 2003、Windows XP、および Windows 2000 のみ) [次へ] のパワー IRP を処理するために、ドライバーの表明します。

6.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) (で Windows 7 および Windows Vista の場合) または[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) (Windows Server 2003、Windows XP、Windows 2000 で)次の下位ドライバーには、クエリ IRP を渡す。 IRP を実行しないでください。

7.  状態を返す\_保留します。 ドライバーで値を変更する必要があります**Irp -&gt;IoStatus.Status**します。

バス ドライバーを呼び出すクエリ性能の IRP では、バス ドライバーに達すると、 **PoStartNextPowerIrp** (Windows Server 2003、Windows XP、および Windows 2000 のみ) を設定および**Irp -&gt;IoStatus.Status**にステータス\_成功ドライバーでできない場合は、エラー状態を設定または指定された電源の状態を変更できます。 バス ドライバーを呼び出して**IoCompleteRequest**、IO を指定する\_いいえ\_インクリメントします。

一般的なデバイス スタック ハンドル、デバイスのドライバー クエリ power IRP を次に示します。

-   ほとんどのフィルター ドライバーが次の下位ドライバーに IRP を渡す必要がありますだけです (を参照してください[Power Irp を渡す](passing-power-irps.md)) 状態を返すと\_保留します。 一部のフィルター ドライバーは、キュー受信 Irp など、デバイスの電源状態を保存またはデバイスに固有のタスクを実行する必要があります最初。

-   関数のドライバーは、(など、完了する保留中の I/O 要求では、キューの受信 I/O 要求すると、デバイス コンテキストを保存またはデバイスの電源を変更する) デバイスに固有のタスクを実行します設定、 *IoCompletion*ルーチン、デバイスを渡します。次の下位のドライバーに IRP の電源 (を参照してください[Power Irp を渡して](passing-power-irps.md))。 ステータスを返す\_PENDING からその*DispatchPower*ルーチン。

-   バス ドライバー呼び出し[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp) (Windows Server 2003、Windows XP、および Windows 2000 のみ) [次へ] のパワー IRP を開始します。 IRP、IO を指定し、完了\_いいえ\_インクリメントします。 呼び出す場合は、ドライバーは IRP をすぐに完了できず、 [ **IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)、ステータスを返します\_から PENDING その*DispatchPower*ルーチンとIRP を後で完了します。

場合でも、ターゲット デバイスは、クエリ対象の電源状態では既に、関数またはフィルター ドライバーごとが I/O をキューし、下ドライバー IRP を渡す必要があります。 IRP は、これが完了すると、バス ドライバーにデバイス スタックの一番下出張する必要があります。

処理中に、 **IRP\_MN\_クエリ\_POWER**要求からドライバーを返す必要があります、 *DispatchPower*できる限り迅速に日常的な。 ドライバーが待機する必要があります、 *DispatchPower*同じ IRP を処理するコードによってルーチンのカーネル イベントがシグナル状態します。 Power Irp がシステム全体で同期されるため、デッドロックが発生する可能性があります。

 

 




