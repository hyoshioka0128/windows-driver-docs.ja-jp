---
title: デバイス電源状態についての IRP_MN_QUERY_POWER の処理
description: デバイス電源状態についての IRP_MN_QUERY_POWER の処理
ms.assetid: 902619bc-068a-4613-b99d-78a243f7fee6
keywords:
- IRP_MN_QUERY_POWER
- デバイスの電源状態 WDK カーネル
- クエリ-電源 Irp の WDK 電源管理
- 電源 Irp WDK カーネル、デバイスクエリ
- 電源状態のクエリ
- キューの Irp
- デバイスクエリの電源 Irp WDK カーネル
- ディスパッチルーチン WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69d2e30a646d898d44d234683e9ca6bd6abede35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836499"
---
# <a name="handling-irp_mn_query_power-for-device-power-states"></a>デバイスの電源状態に対する IRP\_\_クエリ\_電力の処理





デバイスクエリ-電源 IRP は、1つのデバイスの状態の変更についてクエリを実行し、デバイスのスタック内のすべてのドライバーに送信されます。 このような IRP は、i/o スタックの場所の**DevicePowerState**メンバーにあるを指定**します。**

ドライバーは、スタック内を移動するときに、クエリのパワー Irp を処理します。

次のいずれかに該当する場合は、関数またはフィルタードライバーが[**IRP\_\_クエリ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)要求に失敗する可能性があります。

-   デバイスのウェイクアップが有効になっており、要求された電源の状態が、デバイスがシステムをスリープ解除できる状態を下回っています。 たとえば、D2 からシステムをスリープ解除できるが、D3 からは復帰できないデバイスは、D3 のクエリは失敗しますが、D2 のクエリは成功します。

-   要求された状態を入力すると、開いているモデム接続など、データを失う可能性のある操作がドライバーによって強制的に破棄されます。 ドライバーがこの理由でクエリに失敗することはめったにありません。ほとんどの場合、アプリケーションはこのような状況を処理します。

[**IRP\_\_クエリ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)要求に失敗するには、次の手順を実行します。

1.  [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して、ドライバーが次の電源 IRP を処理できるように準備されていることを示します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)。

2.  **Irp-&gt;iostatus. Status**をエラー状態に設定し、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。 IO\_\_増分を指定します。 ドライバーは、IRP をデバイススタックの下位に渡しません。

3.  [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンからエラー状態を返します。

ドライバーがクエリ-電源 IRP を正常に完了した場合は、操作を開始したり、後続の Irp\_が正常に完了しないようにするその他の操作を実行したりすることはできません。その場合は、クエリを実行した電源状態に **\_電源要求を設定\_** ます。

IRP に成功するドライバーは、次のように、クエリを実行した状態に対して set-power IRP を準備し、クエリの IRP を渡す必要があります。

1.  未処理の i/o 操作をすべて完了します。

2.  着信 i/o 要求をキューに挿入します。

3.  指定された電源状態への移行に干渉するその他の新しいアクティビティを開始しないようにします。 ただし、ドライバーは、デバイスコンテキストを保存したり、シャットダウンのために他の手順を実行したりしないでください。

4.  **Iocopy"enti"** を呼び出して、次に低いドライバーの IRP スタックの場所を設定します。

5.  [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定します。 *Iocompletion*ルーチンで、 **Postartnextpowerirp** (Windows SERVER 2003、Windows XP、および windows 2000 のみ) を呼び出して、次の電源 IRP を処理するドライバーの準備を示します。

6.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (windows 7 および windows Vista の場合) または[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出して、クエリの IRP を次の下位のドライバーに渡します。 IRP を完了しないでください。

7.  ステータスを返す\_保留中です。 ドライバーは、 **Irp-&gt;IoStatus. status**で値を変更することはできません。

クエリ電源の IRP がバスドライバーに到達すると、バスドライバーは**Postartnextpowerirp** (windows Server 2003、windows XP、および windows 2000 のみ) を呼び出し、 **IRP&gt;iostatus**\_をに設定します。ドライバーが指定された電源状態。できない場合は、エラー状態を設定します。 次に、バスドライバーは**IoCompleteRequest**を呼び出し、IO\_\_増分を指定します。

一般的なデバイススタック内のドライバーは、次のようにデバイスクエリを処理します。

-   ほとんどのフィルタードライバーは、IRP を次の下位のドライバーに渡し (「[電源 irp の受け渡し](passing-power-irps.md)」を参照してください)、ステータス\_PENDING を返します。 ただし、フィルタードライバーによっては、着信 Irp のキューやデバイスの電源状態の保存など、デバイス固有のタスクを最初に実行する必要がある場合があります。

-   関数ドライバーは、デバイス固有のタスク (保留中の i/o 要求の完了、着信 i/o 要求の処理、デバイスコンテキストの保存、デバイスの電源の変更など) を実行し、 *Iocompletion*ルーチンを設定し、デバイスの電源 IRP を次に低レベルのドライバー (「[電源 irp の受け渡し](passing-power-irps.md)」を参照してください)。 *DispatchPower*ルーチンから状態\_PENDING が返されます。

-   バスドライバーは、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) (windows Server 2003、windows XP、および windows 2000 のみ) を呼び出して、次の電源 IRP を開始します。 次に、IRP を完了し、IO\_\_増分を指定します。 ドライバーが IRP をすぐに完了できない場合は、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出し、 *DISPATCHPOWER*ルーチンから状態\_PENDING を返し、後で irp を完了します。

ターゲットデバイスが既にクエリされた電源の状態にある場合でも、各関数またはフィルタードライバーは i/o をキューに入れ、次の下位のドライバーに IRP を渡す必要があります。 IRP は、デバイススタックをすべて停止してから、バスドライバーを完了する必要があります。

**IRP\_\_クエリ\_電力**要求を処理するときに、ドライバーはできるだけ早く*DispatchPower*ルーチンからを返す必要があります。 ドライバーは、同じ IRP を処理するコードによってシグナルされたカーネルイベントの*DispatchPower*ルーチンを待機することはできません。 システム全体で電源 Irp が同期されるため、デッドロックが発生する可能性があります。

 

 




