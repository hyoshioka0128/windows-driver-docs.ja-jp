---
title: IRP_MN_QUERY_STOP_DEVICE 要求の処理 (Windows 98/Me)
description: IRP_MN_QUERY_STOP_DEVICE 要求の処理 (Windows 98/Me)
ms.assetid: 2a12af98-c5ed-4a24-b957-b363683cc491
keywords:
- IRP_MN_QUERY_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fc2a7682541ff599f4336ab4d7d1499b179c4b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551698"
---
# <a name="handling-an-irpmnquerystopdevice-request-windows-98me"></a>IRP の処理\_MN\_クエリ\_停止\_デバイス要求 (Windows 98/Me)





[ **IRP\_MN\_クエリ\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551725)デバイス スタックの最上位のドライバーによって、各 [次へ] の下のドライバーでし、要求が最初に処理します。 ドライバーのハンドルに Irp の停止、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

応答、 **IRP\_MN\_クエリ\_停止\_デバイス**ドライバーは、次を実行する必要があります。

1.  悪影響ことがなく、デバイスを停止できるかどうかを決定します。

    ドライバーは、次のいずれかに該当する場合、クエリ停止 IRP を失敗する必要があります。

    -   ドライバーに通知されました (を通じて[ **IRP\_MN\_デバイス\_使用状況\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841)) デバイスがページング、休止状態のパスであります。、またはクラッシュ ダンプ ファイル。

    -   デバイスのハードウェア リソースを解放することはできません。

    -   デバイスに開いているハンドルがあります。

    ドライバーが、次の条件が true の場合、クエリ停止 IRP が失敗する可能性があります。

    -   ドライバーは、I/O 要求を削除しない必要があります。

2.  デバイスを停止できない場合は、クエリ停止 IRP に失敗します。

    設定**Irp -&gt;IoStatus.Status** 、該当するエラー状態を呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IO と\_いいえ\_インクリメント、ドライバーからの戻り値および[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 [次へ] の下のドライバーに IRP を渡さないでください。

3.  呼び出す場合は、デバイスを停止することができます、 [ **IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)と[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)を無効にし、登録解除任意のユーザー モード インターフェイス。 デバイスへのアクセスを必要とするすべての受信 I/O 要求の失敗を開始します。

    または、デバイスのドライバーがドライバーは、それ以降受信されるまで、デバイスを完全に一時停止を延期することができます**IRP\_MN\_停止\_デバイス**要求。 このようなドライバーでは、ただし、するおよび無効にするが、デバイスに、追加の処理の開始を防ぐためにクエリの停止要求を処理中に、ユーザー モード インターフェイスを登録解除する必要があります。

    さらに、このようなドライバーから到着した時点ですぐに停止 IRP を指すようにすべての要求が失敗する必要があります。 デバイスが再起動されるまで、このようなドライバーは、次のよう要求を失敗する必要があります。

    -   **IRP\_MN\_デバイス\_使用状況\_通知**要求 (たとえば、デバイス上のページング ファイルを配置する場合)。

    -   アイソクロナス転送の要求数。

    -   停止 IRP を指すからドライバーを妨げる要求を作成します。

4.  デバイスは、失敗する進行状況では IRP を許可することはできない場合、は、その他のドライバー ルーチンとドライバーの削減に渡された未処理の要求が完了したことを確認します。

    これをドライバーで達成する方法の 1 つは、参照カウントとイベントを使用して、すべての要求が完了したことを確認します。

    -   その[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521) 、日常的なドライバー デバイス拡張機能で I/O の参照カウントを定義し、数を 1 つを初期化します。

    -   また、その*AddDevice*ドライバー作成イベントを日常的な[ **KeInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff552137)を非シグナル状態イベントの初期化と[**KeClearEvent**](https://msdn.microsoft.com/library/windows/hardware/ff551980)します。

    -   毎回 IRP の処理、ドライバーと参照カウントをインクリメントする[ **InterlockedIncrement**](https://msdn.microsoft.com/library/windows/hardware/ff547910)します。

    -   要求を完了するたびに、ドライバー、参照カウントをデクリメントを[ **InterlockedDecrement**](https://msdn.microsoft.com/library/windows/hardware/ff547871)します。

        参照カウント ドライバー デクリメント、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)要求は、1 つある場合は、ルーチンまたはへの呼び出しの直後後に[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)ドライバーなしを使用している場合*IoCompletion*要求のルーチンです。

    -   ドライバーが受信すると、 **IRP\_MN\_クエリ\_停止\_デバイス**、ことで、参照がカウントをデクリメント**InterlockedDecrement**します。 未処理の要求はありません、この参照カウントを 0 に減少します。

    -   参照カウントがゼロに達すると、ドライバーを持つイベントを設定[ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)シグナリング クエリ停止コードを継続できます。

    上記の手順を代わりに、ドライバーをシリアル化できる、 **IRP\_MN\_クエリ\_停止\_デバイス**IRP が進行中の任意の Irp の背後にあります。

5.  その他のデバイスを停止保留中の状態にするために必要な手順を実行します。

    正常に準備する必要が、クエリ停止 IRP がドライバーに成功した後、 **IRP\_MN\_停止\_デバイス**します。

6.  IRP を終了します。

    関数またはフィルター ドライバーでは。

    -   設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

    -   [次へ] スタックの場所を設定[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)で [次へ] の下位のドライバーに IRP を渡すと[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336).

    -   状態を反映**保留**から戻り値の状態として、 *DispatchPnP*ルーチン。

    -   IRP を実行しないでください。

    バス ドライバー。

    -   設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

        ただし、バス上のデバイスは、ハードウェア リソースを使用して場合は、バスと子デバイスのリソース要件を再評価します。 要件のいずれかが変更された場合は、状態を返す\_リソース\_要件\_状態ではなく変更\_成功します。 この状態は成功を示しますが、PnP マネージャーが停止 IRP を送信する前に、リソースを再要求します。

    -   IRP の完了 ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) IO と\_いいえ\_インクリメントします。

    -   戻り値、 *DispatchPnP*ルーチン。

デバイス スタック内の任意のドライバーが失敗した場合、 **IRP\_MN\_クエリ\_停止\_デバイス**、PnP マネージャーに送信する[ **IRP\_MN\_キャンセル\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff550826)デバイス スタックにします。 これにより、ドライバーを必要とする、 *IoCompletion*下位のドライバーが IRP を失敗するかどうかを検出するために、クエリ停止 IRP のルーチンです。

 

 




