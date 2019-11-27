---
title: IRP_MN_QUERY_STOP_DEVICE 要求の処理 (Windows 2000 以降)
description: IRP_MN_QUERY_STOP_DEVICE 要求の処理 (Windows 2000 以降)
ms.assetid: 668a920c-aadb-405a-9a1d-091982ca2c04
keywords:
- IRP_MN_QUERY_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e913c65594b193ea0ea2f4ce182a00229c611b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838665"
---
# <a name="handling-an-irp_mn_query_stop_device-request-windows-2000-and-later"></a>IRP\_の処理\_クエリ\_\_デバイスの要求の停止 (Windows 2000 以降)





[**IRP\_\_クエリ\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)の要求は、デバイススタック内の上位のドライバーによって最初に処理され、次に下位のドライバーごとに処理されます。 ドライバーは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで停止 irp を処理します。

**\_\_デバイスを停止する IRP\_\_** に応答して、ドライバーは次の操作を行う必要があります。

1.  デバイスを停止できるかどうか、およびハードウェアリソースが解放され、悪影響を及ぼすことがないかどうかを判断します。

    次のいずれかに該当する場合、ドライバーはクエリ停止の IRP を失敗させる必要があります。

    -   デバイスがページングファイル、休止状態、またはクラッシュダンプファイルのパスにあることを示す、( [**IRP\_\_デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)を介して) ドライバーに通知されました。

    -   デバイスのハードウェアリソースを解放できません。

    次の条件に該当する場合、ドライバーはクエリ停止の IRP を失敗させる可能性があります。

    -   ドライバーは、i/o 要求をドロップせず、Irp をキューに格納するメカニズムを備えていません。

        デバイスが停止状態にある間は、デバイスへのアクセスを必要とする Irp をドライバーが保持する必要があります。 ドライバーが Irp をキューに配置していない場合は、デバイスの停止を許可しないため、クエリ停止の IRP を失敗させる必要があります。

        このルールの例外は、i/o の削除が許可されているデバイスです。 このようなデバイスのドライバーは、キューの Irp を使用せずにクエリの停止と停止要求を正常に実行できます。

2.  デバイスを停止できない場合は、クエリ停止の IRP を失敗とします。

    **Irp&gt;iostatus. status**を適切なエラー状態に設定し、\_IO を使用して**IoCompleteRequest**を呼び出します。\_インクリメントはなく、ドライバーの*DispatchPnP*ルーチンから戻ります。 IRP を次の下位のドライバーに渡さないでください。

3.  デバイスを停止して、ドライバーが Irp をキューに入れる場合は、その後の Irp がキューに入れられるように、デバイス拡張で HOLD\_NEW\_REQUESTS フラグを設定します (「[デバイスが一時停止したときに受信 irp を保持する](holding-incoming-irps-when-a-device-is-paused.md)」を参照してください)。

    または、デバイスのドライバーが、デバイスの一時停止を遅延させることもできます。これにより、ドライバーは、その後の[**IRP\_完了\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)要求を受信します。 ただし、このようなドライバーは、受信時に停止 IRP の直後に到達できないようにする要求をキューに置いておく必要があります。 デバイスが再起動されるまで、このようなドライバーは次のような要求をキューに含める必要があります。

    -   [**IRP\_、デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)要求 (たとえば、ページングファイルをデバイスに配置するなど) を\_します。

    -   アイソクロナス転送の要求。

    -   停止 IRP でドライバーが停止するのを防ぐ要求を作成します。

4.  デバイスで IRP が進行中でない場合は、他のドライバールーチンに渡された未処理の要求と、ドライバーが下位にあるすべての要求が完了していることを確認します。

    ドライバーがこれを実現する方法の1つは、参照カウントとイベントを使用して、すべての要求が完了したことを確認することです。

    -   [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンでは、ドライバーはデバイス拡張機能の i/o 参照カウントを定義し、カウントを1に初期化します。

    -   また、 *AddDevice*ルーチンでは、ドライバーは[**keinitializeevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)を使用してイベントを作成し、 [**keclearevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent)を使用して、イベントを非シグナル状態に初期化します。
    -   IRP を処理するたびに、ドライバーは[**InterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)を使用して参照カウントをインクリメントします。

    -   要求が完了するたびに、ドライバーは[**InterlockedDecrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement)を使用して参照カウントをデクリメントします。

        ドライバーは、要求に対して*iocompletion*ルーチンが使用されていない場合、要求に1つ、または[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)の呼び出しの直後に、 [*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンの参照カウントをデクリメントします。

    -   ドライバーが IRP\_を受信すると **\_デバイス\_停止\_クエリ**を実行すると、参照カウントが**InterlockedDecrement**で減少します。 未処理の要求がない場合は、参照カウントを0に減らします。

    -   参照カウントが0になると、ドライバーは、クエリストップコードを続行できることを[**KeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)シグナリングでイベントに設定します。

    上記の手順の代わりに、ドライバーは**irp\_\_クエリ**をシリアル化して、進行中の任意の irp の背後にある\_デバイスの IRP を停止\_ことができます。

5.  デバイスを停止保留中状態にするために必要なその他の手順を実行します。

    ドライバーは、クエリ停止の IRP を正常に完了した後に、Irp\_完了する準備ができて **\_デバイスを停止\_** する必要があります。

6.  IRP を終了します。

    関数またはフィルタードライバーの場合:

    -   **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

    -   [**IoskipIoCallDriver Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を使用して次のスタックの場所を設定し、IRP を次の下位[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)のドライバーに渡します。

    -   **IoCallDriver**の状態を*DispatchPnP*ルーチンからの戻りステータスとして伝達します。

    -   IRP を完了しないでください。

    バスドライバーの場合:

    -   **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

        ただし、バス上のデバイスでハードウェアリソースを使用する場合は、バスと子デバイスのリソース要件を再評価します。 要件のいずれかが変更されている場合は、状態\_成功の状態ではなく、\_リソース\_要件\_変更されます。 この状態は成功を示しますが、stop IRP を送信する前に、PnP マネージャーがリソースを再実行するように要求します。

    -   IO\_\_を増やさずに、IRP ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了します。

    -   *DispatchPnP*ルーチンからを返します。

デバイススタック内のいずれかのドライバー **\_が\_クエリ\_\_デバイスを停止**しようとして失敗した場合、PnP マネージャーは\_デバイススタックへの\_を停止\_キャンセル\_[**irp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)を送信します。 これにより、ドライバーが IRP に障害が発生したかどうかを検出するために、クエリ停止の IRP に対して*Iocompletion*ルーチンが要求されるのを防ぐことができます。

 

 




