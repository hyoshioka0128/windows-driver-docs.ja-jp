---
title: IRP_MN_QUERY_STOP_DEVICE 要求 (Windows 2000 以降) の処理
description: IRP_MN_QUERY_STOP_DEVICE 要求 (Windows 2000 以降) の処理
ms.assetid: 668a920c-aadb-405a-9a1d-091982ca2c04
keywords:
- IRP_MN_QUERY_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cbf5855ee2768d9b3c5e43714a28c856df7630a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384235"
---
# <a name="handling-an-irpmnquerystopdevice-request-windows-2000-and-later"></a>IRP の処理\_MN\_クエリ\_停止\_デバイス (Windows 2000 以降) を要求します。





[ **IRP\_MN\_クエリ\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)デバイス スタックの最上位のドライバーによって、各 [次へ] の下のドライバーでし、要求が最初に処理します。 ドライバーのハンドルに Irp の停止、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

応答、 **IRP\_MN\_クエリ\_停止\_デバイス**ドライバーは、次を実行する必要があります。

1.  かどうか、デバイスを停止することができます、およびリリースされると、悪影響ことがなく、ハードウェア リソースを決定します。

    ドライバーは、次のいずれかに該当する場合、クエリ停止 IRP を失敗する必要があります。

    -   ドライバーに通知されました (を通じて[ **IRP\_MN\_デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)) デバイスがページング、休止状態のパスであります。、またはクラッシュ ダンプ ファイル。

    -   デバイスのハードウェア リソースを解放することはできません。

    ドライバーが、次の条件が true の場合、クエリ停止 IRP が失敗する可能性があります。

    -   ドライバーは、I/O 要求を削除する必要がありますしないと、キュー Irp のメカニズムはありません。

        停止状態では、デバイスが、ドライバーは Irp をデバイスへのアクセスを必要とするを保持する必要があります。 ドライバーは Irp を蓄積されません場合、停止するデバイスを許可する必要があり、そのため、クエリ停止 IRP に失敗する必要があります。

        このルールの例外は、I/O を削除する許可されているデバイスです。 このようなデバイスのドライバーは、クエリ停止を成功およびキュー Irp なし要求を停止できます。

2.  デバイスを停止できない場合は、クエリ停止 IRP に失敗します。

    設定**Irp -&gt;IoStatus.Status** 、該当するエラー状態を呼び出す**IoCompleteRequest** IO と\_いいえ\_増分値、およびドライバーのからの戻り値*DispatchPnP*ルーチン。 [次へ] の下のドライバーに IRP を渡さないでください。

3.  デバイスを停止して、ドライバーは Irp をキューする場合、ホールドを設定します。\_新規\_後続 Irp をキューに配置するため、デバイスの拡張機能の要求のフラグ (を参照してください[を保持している受信 Irp ときに、デバイスが一時停止](holding-incoming-irps-when-a-device-is-paused.md))。

    または、デバイスのドライバーがドライバーは、それ以降受信されるまで、デバイスを完全に一時停止を延期することができます[ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)要求。 ただし、このようなドライバーはから到着した時点ですぐに停止 IRP を指すようにすべての要求をキューする必要があります。 デバイスが再起動されるまでこのようなドライバーは、次の要求をキューする必要があります。

    -   [**IRP\_MN\_デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)要求 (たとえば、デバイス上のページング ファイルを配置する場合)。

    -   アイソクロナス転送の要求数。

    -   停止 IRP を指すからドライバーを妨げる要求を作成します。

4.  デバイスは、進行状況の失敗では IRP を含めることはできない場合、は、その他のドライバー ルーチンとドライバーの削減に渡された未処理の要求が完了したことを確認します。

    これをドライバーで達成する方法の 1 つは、参照カウントとイベントを使用して、すべての要求が完了したことを確認します。

    -   その[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device) 、日常的なドライバー デバイス拡張機能で I/O の参照カウントを定義し、数を 1 つを初期化します。

    -   また、その*AddDevice*ドライバー作成イベントを日常的な[ **KeInitializeEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializeevent)を非シグナル状態イベントの初期化と[**KeClearEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keclearevent)します。
    -   毎回 IRP の処理、ドライバーと参照カウントをインクリメントする[ **InterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedincrement)します。

    -   要求を完了するたびに、ドライバー、参照カウントをデクリメントを[ **InterlockedDecrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockeddecrement)します。

        参照カウント ドライバー デクリメント、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)場合は、要求がある 1 つは、日常的なまたは右への呼び出し後[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)ドライバーなしを使用している場合*IoCompletion*要求のルーチンです。

    -   ドライバーが受信すると、 **IRP\_MN\_クエリ\_停止\_デバイス**、ことで、参照がカウントをデクリメント**InterlockedDecrement**します。 未処理の要求はありません、この参照カウントを 0 に減少します。

    -   参照カウントがゼロに達すると、ドライバーを持つイベントを設定[ **KeSetEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)シグナリング クエリ停止コードを継続できます。

    上記の手順を代わりに、ドライバーをシリアル化できる、 **IRP\_MN\_クエリ\_停止\_デバイス**IRP が進行中の任意の Irp の背後にあります。

5.  その他のデバイスを停止保留中の状態にするために必要な手順を実行します。

    正常に準備する必要が、クエリ停止 IRP がドライバーに成功した後、 **IRP\_MN\_停止\_デバイス**します。

6.  IRP を終了します。

    関数またはフィルター ドライバーでは。

    -   設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

    -   [次へ] スタックの場所を設定[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で [次へ] の下位のドライバーに IRP を渡すと[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver).

    -   状態を反映**保留**から戻り値の状態として、 *DispatchPnP*ルーチン。

    -   IRP を実行しないでください。

    バス ドライバー。

    -   設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

        ただし、バス上のデバイスは、ハードウェア リソースを使用して場合は、バスと子デバイスのリソース要件を再評価します。 要件のいずれかが変更された場合は、状態を返す\_リソース\_要件\_状態ではなく変更\_成功します。 この状態は成功を示しますが、PnP マネージャーが停止 IRP を送信する前に、リソースを再要求します。

    -   IRP の完了 ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)) IO と\_いいえ\_インクリメントします。

    -   戻り値、 *DispatchPnP*ルーチン。

デバイス スタック内の任意のドライバーが失敗した場合、 **IRP\_MN\_クエリ\_停止\_デバイス**、PnP マネージャーに送信する[ **IRP\_MN\_キャンセル\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)デバイス スタックにします。 これにより、ドライバーを必要とする、 *IoCompletion*下位のドライバーが IRP を失敗するかどうかを検出するために、クエリ停止 IRP のルーチンです。

 

 




