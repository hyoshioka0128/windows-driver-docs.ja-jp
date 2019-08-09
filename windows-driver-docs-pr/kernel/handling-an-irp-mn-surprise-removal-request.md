---
title: IRP_MN_SURPRISE_REMOVAL 要求の処理
description: IRP_MN_SURPRISE_REMOVAL 要求の処理
ms.assetid: 39a90617-40ad-4c10-95d3-2b618d66d70e
keywords:
- 突然の PnP WDK の削除
- IRP_MN_SURPRISE_REMOVAL
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c62730867b226430f37d6d2df9360cd9733a4b8f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386876"
---
# <a name="handling-an-irp_mn_surprise_removal-request"></a>IRP の処理\_MN\_突然\_削除要求





Windows 2000 および PnP マネージャー後で、デバイスが I/O 操作に使用できるが不要になったと、コンピューター (「突然削除」) から予期せずに削除された可能性がありますドライバーに通知するには、この IRP を送信します。

PnP マネージャーに送信、 [ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求は、次の理由。

-   バスに通知のホット プラグがある場合は、デバイスが表示されなくなったデバイスの親のバス ドライバーに通知します。 バス ドライバー呼び出し[ **IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)します。 PnP マネージャーがその子のバス ドライバーをクエリの応答、([**IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)の**BusRelations**)。 PnP マネージャーでは、デバイスが新しい子の一覧にないし、デバイスの場合は、その突然削除操作を開始します。 を決定します。

-   その他の理由、バスが列挙され、突然削除されたデバイスは、子の一覧には含まれません。 PnP マネージャーは、突然の削除操作を開始します。

-   (ため、たとえば、繰り返し、要求がタイムアウト時)、デバイスは存在しないデバイスの機能のドライバーを決定します。 バスは、列挙可能な可能性がありますが、ホット プラグ通知はありません。 この場合、関数のドライバーを呼び出す[ **IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicestate)します。 PnP マネージャーに送信、応答で、 [ **IRP\_MN\_クエリ\_PNP\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state)デバイス スタックを要求します。 関数ドライバー、PNP を設定する\_デバイス\_の失敗のフラグ、 [ **PNP\_デバイス\_状態**](#about-pnp_device_state)デバイスが失敗したことを示すビットマスク。

-   ドライバー スタックが正常に完了、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)要求が、その後、後続の失敗した[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。 このような場合、デバイスは接続されていると思います。

すべての PnP ドライバーは、この IRP を処理する必要があり、設定する必要があります**Irp -&gt;IoStatus.Status**ステータス\_成功します。 PnP デバイスのドライバーを処理するために準備する必要があります**IRP\_MN\_突然\_削除**ドライバーの後にいつでも[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチンが呼び出されます。 IRP の適切な処理は、ドライバー、PnP マネージャーを有効にします。

1.  まだ接続されている場合、デバイスを無効にします。

    ドライバー スタックが正常に完了した場合、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)要求が、その後、何らかの理由で失敗しました、後続[**IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求、デバイスを無効にする必要があります。

2.  デバイスに割り当てられたハードウェア リソースを解放し、別のデバイスに利用できるようにします。

    デバイスが使用できなくするとすぐにハードウェア リソースを解放する必要があります。 PnP マネージャーは、このユーザーがホット プラグ、マシンに、同じデバイスを含む別のデバイスにリソースを再割り当てしできます。

3.  データの損失やシステムの停止のリスクを最小限に抑えます。

    ホットプラグとそのドライバーをサポートするデバイスは、突然の削除を処理するために設計する必要があります。 ユーザーは、いつでもホットプラグ機能をサポートするデバイスを削除できるようにする予定です。

PnP マネージャーに送信、 **IRP\_MN\_突然\_削除**IRQL = パッシブ\_システム スレッドのコンテキスト内のレベル。

PnP マネージャーでは、ユーザー モード アプリケーションとその他のカーネル モード コンポーネントに通知する前に、この IRP がドライバーに送信します。 IRP が完了したら、PnP マネージャーに送信した後、 **EventCategoryTargetDeviceChange** GUID を持つ通知\_ターゲット\_デバイス\_削除\_カーネル モードの完了デバイスでは、このような通知に登録するコンポーネント。

**IRP\_MN\_突然\_削除**デバイス スタックの最上位のドライバー、続いて各 [次へ] の下のドライバー、IRP が最初に処理されます。

応答で**IRP\_MN\_突然\_削除**ドライバーが一覧表示されている順序で、以下を実行する必要があります。

1.  デバイスが削除されたかどうかを決定します。

    ドライバー常に、デバイスがまだ接続されているかどうかの判断を試みます。 場合は、ドライバーは、デバイスを停止および無効にすることを試みる必要があります。

2.  (割り込み、I/O ポート、メモリのレジスタおよび DMA チャネル) のデバイスのハードウェア リソースを解放します。

3.  親のバス ドライバー、バス スロット電源、ドライバーではこれを行う場合。 呼び出す[ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)電源マネージャーに通知します。 詳細については、次を参照してください。[電源管理](implementing-power-management.md)します。

4.  デバイスで新しい I/O 操作を防止します。

    ドライバーを後続処理[ **IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)、 [ **IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)、 [ **IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)、および[ **IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)要求ですが、ドライバーは、新しい I/O 操作を防ぐ必要があります。 ドライバーは、デバイスが閉じる、クリーンアップ、および PnP Irp だけでなく、存在していた場合、ドライバーは処理後の Irp で失敗する必要があります。

    ドライバーが、デバイスが突然削除されたことを示すデバイス拡張機能で少し設定できます。 ドライバーのディスパッチ ルーチンは、このビットをチェックする必要があります。

5.  デバイスで未処理の I/O 要求が失敗します。

6.  続行すると、デバイスのドライバーが処理しないすべての Irp を渡します。

7.  デバイスのインターフェイスを無効にする[ **IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)します。

8.  任意のデバイスに固有の割り当て、メモリ、イベント、またはその他のシステム リソースをクリーンアップします。

    それに続くを受信するまで、ドライバーはこのようなクリーンアップを延期でした[ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)レガシ コンポーネントの開いているハンドルである場合は、要求閉じることができません、削除の IRP は送信されません。

9.  デバイス スタックに接続されているデバイス オブジェクトのままにします。

    デタッチしてそれに続くまで、デバイス オブジェクトを削除しない**IRP\_MN\_削除\_デバイス**要求。

10. IRP を終了します。

    関数またはフィルター ドライバーでは。

    -   設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

    -   [次へ] スタックの場所を設定[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で [次へ] の下位のドライバーに IRP を渡すと[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver).

    -   状態を反映**保留**から戻り値の状態として、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

    -   IRP を実行しないでください。

    (子 PDO に対してこの IRP を処理) している、バス ドライバー。

    -   設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

    -   IRP の完了 ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)) IO と\_いいえ\_インクリメントします。

    -   戻り値、 *DispatchPnP*ルーチン。

PnP マネージャーが送信した後、この IRP が成功し、デバイスへのすべての開いているハンドルが閉じられている、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)デバイス スタックを要求します。 IRP の削除に応答してでは、ドライバーは、スタックからそれらのデバイス オブジェクトをデタッチし、それらを削除します。 レガシ コンポーネントが開き、デバイスにハンドルと外に出て、ハンドルを開く I/O の失敗にかかわらず、PnP マネージャー削除 IRP を送信しません。

すべてのドライバーでは、この IRP を処理する必要があり、マシンから、デバイスが物理的に削除されたことに注意してください。 一部のドライバーでは、ただしが有害な結果 IRP を処理しない場合。 たとえば、ハードウェア リソースは、消費しませんので、システムのハードウェア リソースを消費しませんされ、USB または 1394 などのプロトコルに基づくバス上に存在するデバイスをリンク付けできません。 ドライバーが、関数とフィルター ドライバー親バス ドライバーを介してのみ、デバイスをアクセスするため、削除された後、デバイスにアクセスしようとしてのリスクはありません。 バスは、削除の通知をサポートするため、親のバス ドライバー、デバイスが表示されなくなり、バス ドライバーには、デバイスにアクセスする後続のすべてが失敗したときに通知されます。

Windows 98 で、PnP マネージャーを送信しませんこの IRP/。 PnP マネージャーがのみに送信して、ユーザーは、最初に、適切なユーザー インターフェイスを使用せず、デバイスを削除した場合、 **IRP\_MN\_削除\_デバイス**デバイスのドライバーを要求します。 すべての WDM ドライバーは、両方を処理する必要があります**IRP\_MN\_突然\_削除**と**IRP\_MN\_削除\_デバイス**。 コードを**IRP\_MN\_削除\_デバイス**ドライバーが突然削除の前の IRP を受信し、両方のケースを処理する必要があるかどうかを確認する必要があります。

 ## <a name="using-guid_reenumerate_self_interface_standard"></a>GUID_REENUMERATE_SELF_INTERFACE_STANDARD を使用します。

GUID_REENUMERATE_SELF_INTERFACE_STANDARD インターフェイスでは、そのデバイスが再度列挙することを要求するためのドライバーを使用します。

このインターフェイスを使用するには、InterfaceType にバス ドライバーに IRP_MN_QUERY_INTERFACE IRP を送信 GUID_REENUMERATE_SELF_INTERFACE_STANDARD を = です。 バス ドライバーでは、インターフェイスの個々 のルーチンへのポインターを格納する REENUMERATE_SELF_INTERFACE_STANDARD 構造体へのポインターを提供します。 A [ReenumerateSelf ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-preenumerate_self)バス ドライバーに子デバイスが再列挙を要求します。


## <a name="about-pnp_device_state"></a>PNP_DEVICE_STATE について

PNP\_デバイス\_状態の種類は PnP デバイスの状態を記述するビットマスク。 ドライバーへの応答でこの型の値を返します、 **IRP\_MN\_クエリ\_PNP\_デバイス\_状態**要求。

``` syntax
typedef ULONG PNP_DEVICE_STATE, *PPNP_DEVICE_STATE;
```

フラグのビットで、PNP\_デバイス\_状態値は次のように定義されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>フラグのビット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PNP_DEVICE_DISABLED</td>
<td><p>デバイスが物理的に存在するが、ハードウェアでは無効です。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_DONT_DISPLAY_IN_UI</td>
<td><p>デバイスをユーザー インターフェイスに表示されません。 物理的に存在するラップトップ コンピューター、ラップトップがドッキングされていないときに、使用できないゲーム ポートなど、現在の構成では使用できませんが、デバイスの設定します。 (も参照してください、 <strong>NoDisplayInUI</strong>フラグ、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities" data-raw-source="[&lt;strong&gt;DEVICE_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)"> <strong>DEVICE_CAPABILITIES</strong> </a>構造です)。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_FAILED</td>
<td><p>デバイスがあり、正しく機能していません。</p>
<p>このフラグと PNP_DEVICE_RESOURCE_REQUIREMENTS_CHANGED の両方を設定すると、PnP マネージャー (途切れることがなく再調整は、デバイスのサポートされていません)、新しいハードウェア リソースを割り当てる前に、このデバイスを停止する必要があります。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_NOT_DISABLEABLE</td>
<td><p>コンピューターの起動時、デバイスが必要です。 このようなデバイスを無効にしない必要があります。</p>
<p>ドライバーは、デバイスのシステムの適切な操作に必要な場合、このビットを設定します。 ドライバーがページング パスでデバイスが通知を受け取る場合など (<a href="irp-mn-device-usage-notification.md" data-raw-source="[&lt;strong&gt;IRP_MN_DEVICE_USAGE_NOTIFICATION&lt;/strong&gt;](irp-mn-device-usage-notification.md)"><strong>IRP_MN_DEVICE_USAGE_NOTIFICATION</strong> </a>の<strong>DeviceUsageTypePaging</strong>)、ドライバー呼び出し<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicestate" data-raw-source="[&lt;strong&gt;IoInvalidateDeviceState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicestate)"> <strong>IoInvalidateDeviceState</strong> </a> 、最終的なこのフラグを設定および<strong>IRP_MN_QUERY_PNP_DEVICE_STATE</strong>要求。</p>
<p>このビットが設定されて、デバイスの場合、PnP マネージャーには、親デバイス、その親の親のデバイスなどを行うには、この設定が反映されます。</p>
<p>このビットがルートで列挙されるデバイスに設定されている場合、デバイスを無効またはアンインストールできません。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_REMOVED</td>
<td><p>デバイスが物理的に削除されました。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_RESOURCE_REQUIREMENTS_CHANGED</td>
<td><p>デバイスのリソース要件が変更されました。</p>
<p>通常、バス ドライバーは、新しい子デバイスを列挙するためのリソース要件を展開する必要がありますと判断したときに、このフラグを設定します。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_DISCONNECTED</td>
<td><p>デバイス ドライバーが読み込まれますが、このドライバーは、デバイスが不要になったコンピューターに接続されていることを検出しました。 通常、このフラグは、ワイヤレス デバイスと通信する関数のドライバーに対して使用されます。 たとえば、フラグは、デバイスが範囲外へ移動しすると、デバイスの範囲に移動し、再度接続をオフに設定されます。</p>
<p>バス ドライバーでは、このフラグは通常は設定されません。 代わりに、デバイスが不要になった接続されている場合は、子デバイスを列挙するバス ドライバーを停止します。 このフラグは、関数のドライバーが接続を管理する場合にのみ使用されます。</p>
<p>このフラグの唯一の目的では、クライアントが、デバイスが接続されているかどうかを把握できるようにします。 フラグを設定するには影響しません、ドライバーが読み込まれるかどうか。</p></td>
</tr>
</tbody>
</table>

 

PnP マネージャー クエリ、デバイスの PNP\_デバイス\_状態を送信してデバイスの開始直後に、 **IRP\_MN\_クエリ\_PNP\_デバイス\_状態**デバイス スタックを要求します。 この IRP に応答してでデバイスのドライバーは PNP で適切なフラグを設定\_デバイス\_状態。

最初のクエリの後に状態の特性のいずれかを変更する場合、ドライバー マネージャーに通知します PnP 呼び出して[ **IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicestate)します。 呼び出しに応答**IoInvalidateDeviceState**、PnP マネージャー クエリ、デバイスの PNP\_デバイス\_もう一度状態します。

デバイスは PNP マークされている場合\_デバイス\_いない\_DISABLEABLE、デバッガーを表示する、DNUF\_いない\_devnode DISABLEABLE ユーザー フラグ。 デバッガーを表示することも、 **DisableableDepends**上の理由から、デバイスを無効にできない理由の数をカウントする値。 この値は、X は 1 つのデバイスを無効にすることはできません、Y は無効にすることはできません、デバイスの子のデバイスの数の場合、X + Y の合計です。




