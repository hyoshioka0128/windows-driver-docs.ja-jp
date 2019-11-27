---
title: IRP_MN_SURPRISE_REMOVAL 要求の処理
description: IRP_MN_SURPRISE_REMOVAL 要求の処理
ms.assetid: 39a90617-40ad-4c10-95d3-2b618d66d70e
keywords:
- 不用意の削除 WDK PnP
- IRP_MN_SURPRISE_REMOVAL
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eeaa38dbcbf7f354a1b0f5ab0eb1084739b4a0e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836597"
---
# <a name="handling-an-irp_mn_surprise_removal-request"></a>IRP\_処理\_突然\_の削除要求





Windows 2000 以降の PnP マネージャーは、この IRP を送信して、デバイスが i/o 操作で使用できなくなったため、予期せずコンピューターから削除された ("突然の削除") ことをドライバーに通知します。

PnP マネージャーは、次の理由により、 [**IRP\_削除要求\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)を送信します。

-   バスにホットプラグ通知がある場合は、デバイスが消失したことをデバイスの親バスドライバーに通知します。 バスドライバーは[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)を呼び出します。 応答として、PnP マネージャーは、その子のバスドライバーを照会します ([**IRP\_\_クエリ\_デバイス\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations) **busrelations**の関係)。 PnP マネージャーは、デバイスが新しい子リストに含まれていないと判断し、そのデバイスに対する突然の削除操作を開始します。

-   バスは別の理由で列挙され、突然削除されたデバイスは子の一覧に含まれません。 PnP マネージャーは、突然の削除操作を開始します。

-   デバイスの関数ドライバーは、デバイスが存在しないことを判断します (たとえば、要求が繰り返しタイムアウトするなど)。 バスは列挙可能ですが、ホットプラグ通知を持っていない可能性があります。 この場合、関数ドライバーは[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)を呼び出します。 応答として、PnP マネージャーは、 [**pnp\_デバイス\_状態要求\_、IRP\_\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state)をデバイススタックに送信します。 関数ドライバーは、デバイスに障害が発生したことを示す[**pnp\_デバイスの\_状態**](#about-pnp_device_state)のビットマスクで、PNP\_デバイス\_失敗フラグを設定します。

-   ドライバースタックは正常に Irp\_を完了し、デバイスの要求[ **\_を停止\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)ますが、その後の[**irp\_完了\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求の開始\_失敗します。 このような場合は、デバイスがまだ接続されている可能性があります。

すべての PnP ドライバーはこの IRP を処理する必要があり、 **irp&gt;IoStatus. status**を STATUS\_SUCCESS に設定する必要があります。 PnP デバイス用のドライバーは、ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが呼び出された後、いつでも**IRP\_\_\_** 処理するように準備する必要があります。 IRP を適切に処理することで、ドライバーと PnP マネージャーは次のことができるようになります。

1.  デバイスがまだ接続されている場合は、デバイスを無効にします。

    ドライバースタックが Irp\_が正常に完了した場合は、デバイス要求の[ **\_を停止\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)ますが、何らかの理由により後続の irp\_失敗して[ **\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)の要求を開始すると、デバイスを無効にする必要があります。\_

2.  デバイスに割り当てられているハードウェアリソースを解放し、別のデバイスで使用できるようにします。

    デバイスが使用できなくなるとすぐに、ハードウェアリソースが解放されます。 PnP マネージャーは、同じデバイスを含む別のデバイスにリソースを再割り当てできます。この場合、ユーザーはコンピューターにホットプラグバックする可能性があります。

3.  データ損失とシステム中断のリスクを最小限に抑えます。

    ホットプラグとそのドライバーをサポートするデバイスは、突然の削除を処理するように設計する必要があります。 ユーザーは、ホットプラグをサポートするデバイスをいつでも削除できることを期待しています。

PnP マネージャーは、システムスレッドのコンテキストで、IRQL = パッシブ\_レベルでの**IRP\_削除\_を\_** して、IRP を送信します。

PnP マネージャーは、ユーザーモードアプリケーションやその他のカーネルモードコンポーネントに通知する前に、この IRP をドライバーに送信します。 IRP が完了すると、PnP マネージャーは、\_デバイスの GUID\_ターゲットと共に**Eventcomponents Targetdevicechange** notification を送信\_\_ます。この通知に登録されているカーネルモードコンポーネントには、ドライブ.

**Irp\_\_驚く\_削除**irp は、まずデバイススタックの上位ドライバーによって処理され、次に下位のドライバーごとに処理されます。

**IRP\_が\_驚く\_削除**されると、ドライバーは次の処理を順番に実行する必要があります。

1.  デバイスが削除されているかどうかを確認します。

    ドライバーは、デバイスがまだ接続されているかどうかを常に判断する必要があります。 有効である場合、ドライバーはデバイスを停止して無効にする必要があります。

2.  デバイスのハードウェアリソース (割り込み、i/o ポート、メモリレジスタ、および DMA チャネル) を解放します。

3.  親バスドライバーで、ドライバーが対応できる場合はバススロットの電源を入れます。 [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して、電源マネージャーに通知します。 詳細については、「[電源管理](implementing-power-management.md)」を参照してください。

4.  デバイスで新しい i/o 操作を実行しないようにします。

    ドライバーは、後続の[**irp\_MJ\_CLEANUP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)、 [**irp\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)、 [**irp\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)、および[**irp\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)要求を処理する必要がありますが、ドライバーは新しい i/o 操作。 ドライバーは、終了、クリーンアップ、および PnP Irp 以外に、デバイスが存在する場合にドライバーによって処理された後続の Irp をすべて失敗させる必要があります。

    ドライバーは、デバイスが突然削除されたことを示すために、デバイス拡張機能のビットを設定できます。 ドライバーのディスパッチルーチンは、このビットを確認する必要があります。

5.  デバイス上の未処理の i/o 要求を失敗させます。

6.  ドライバーがデバイス用に処理しない Irp を引き続き渡します。

7.  [**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を使用してデバイスインターフェイスを無効にします。

8.  デバイス固有の割り当て、メモリ、イベント、またはその他のシステムリソースをクリーンアップします。

    ドライバーは、後続の IRP\_を受け取るまで、このようなクリーンアップを延期して[ **\_デバイス要求を削除\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)ます。ただし、レガシコンポーネントに閉じられないハンドルが開いている場合は、remove IRP は送信されません。

9.  デバイスオブジェクトはデバイススタックにアタッチしたままにしておきます。

    その後の**IRP\_完了\_\_デバイス**の要求を削除するまで、デバイスオブジェクトをデタッチして削除しないでください。

10. IRP を終了します。

    関数またはフィルタードライバーの場合:

    -   **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

    -   [**IoskipIoCallDriver Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を使用して次のスタックの場所を設定し、IRP を次の下位[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)のドライバーに渡します。

    -   **IoCallDriver**の状態を[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンからの戻りステータスとして伝達します。

    -   IRP を完了しないでください。

    バスドライバー (子 PDO に対してこの IRP を処理する) では、次の操作を行います。

    -   **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

    -   IO\_\_を増やさずに、IRP ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了します。

    -   *DispatchPnP*ルーチンからを返します。

この IRP が成功し、デバイスに対して開いているハンドルがすべて閉じられると、PnP マネージャーは、デバイススタックに\_デバイスの要求を[**削除\_、IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)を送信します。 Remove IRP に応答して、ドライバーはデバイスオブジェクトをスタックからデタッチし、削除します。 レガシコンポーネントにデバイスが開かれているハンドルがあり、i/o エラーが発生してもハンドルが開いたままになっている場合、PnP マネージャーは削除 IRP を送信しません。

すべてのドライバーがこの IRP を処理する必要があり、デバイスがコンピューターから物理的に削除されていることに注意してください。 ただし、一部のドライバーでは、IRP を処理しないと、悪影響を及ぼすことはありません。 たとえば、システムハードウェアリソースを消費せず、プロトコルベースのバス上に存在するデバイス (USB や1394など) は、を消費しないため、ハードウェアリソースを割り当てることができません。 ドライバーが削除された後に、ドライバーがデバイスにアクセスしようとするリスクはありません。これは、機能とフィルタードライバーが親バスドライバーを使用してのみデバイスにアクセスするためです。 バスは削除通知をサポートしているため、デバイスが非表示になったときに親バスドライバーに通知され、その後デバイスへのすべてのアクセス試行がバスドライバーによって失敗します。

Windows 98/Me では、PnP マネージャーはこの IRP を送信しません。 ユーザーが適切なユーザーインターフェイスを使用せずにデバイスを削除した場合、PnP マネージャーは、デバイスのドライバーに\_デバイスの要求を**削除\_、IRP\_** を送信します。 すべての WDM ドライバーは、 **irp\_\_** を処理する必要があります。突然\_削除し、 **IRP\_\_デバイスを削除\_** ます。 **Irp\_\_削除\_デバイス**のコードでは、ドライバーが前の予期しない IRP を受信し、両方のケースを処理する必要があるかどうかを確認する必要があります。

 ## <a name="using-guid_reenumerate_self_interface_standard"></a>GUID_REENUMERATE_SELF_INTERFACE_STANDARD の使用

GUID_REENUMERATE_SELF_INTERFACE_STANDARD インターフェイスを使用すると、ドライバーはデバイスを再列挙するように要求できます。

このインターフェイスを使用するには、InterfaceType = GUID_REENUMERATE_SELF_INTERFACE_STANDARD を使用して IRP_MN_QUERY_INTERFACE IRP をバスドライバーに送信します。 バスドライバーは、インターフェイスの個々のルーチンへのポインターを含む REENUMERATE_SELF_INTERFACE_STANDARD 構造体へのポインターを提供します。 [ReenumerateSelf ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-preenumerate_self)は、バスドライバーが子デバイスを reenumerate することを要求します。


## <a name="about-pnp_device_state"></a>PNP_DEVICE_STATE について

PNP\_デバイスの\_状態の種類は、デバイスの PnP 状態を示すビットマスクです。 ドライバーは、 **IRP\_の\_クエリ\_PNP\_デバイス\_状態**要求に応答して、この型の値を返します。

``` syntax
typedef ULONG PNP_DEVICE_STATE, *PPNP_DEVICE_STATE;
```

PNP\_デバイス\_状態値のフラグビットは、次のように定義されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>フラグビット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PNP_DEVICE_DISABLED</td>
<td><p>デバイスは物理的に存在していますが、ハードウェアで無効になっています。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_DONT_DISPLAY_IN_UI</td>
<td><p>デバイスをユーザーインターフェイスに表示しません。 物理的に存在するが、現在の構成では使用できないデバイスに対して設定します。たとえば、ラップトップのドッキングが解除されたときには使用できない、ラップトップのゲームポートなどです。 ( <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities" data-raw-source="[&lt;strong&gt;DEVICE_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)"><strong>DEVICE_CAPABILITIES</strong></a>構造体の<strong>Nodisplayinui</strong>フラグも参照してください)。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_FAILED</td>
<td><p>デバイスは存在しますが、正常に機能していません。</p>
<p>このフラグと PNP_DEVICE_RESOURCE_REQUIREMENTS_CHANGED の両方を設定した場合、PnP マネージャが新しいハードウェアリソースを割り当てる前にデバイスを停止する必要があります (デバイスでは、無着陸再調整はサポートされていません)。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_NOT_DISABLEABLE</td>
<td><p>デバイスは、コンピューターを起動するときに必要になります。 このようなデバイスは無効にしないでください。</p>
<p>ドライバーは、適切なシステム操作に必要なデバイスにこのビットを設定します。 たとえば、デバイスがページングパス ( <strong>DeviceIoInvalidateDeviceState Typepaging</strong>の場合は<a href="irp-mn-device-usage-notification.md" data-raw-source="[&lt;strong&gt;IRP_MN_DEVICE_USAGE_NOTIFICATION&lt;/strong&gt;](irp-mn-device-usage-notification.md)"><strong>IRP_MN_DEVICE_USAGE_NOTIFICATION</strong></a> ) にあるという通知をドライバーが受信すると、ドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate" data-raw-source="[&lt;strong&gt;IoInvalidateDeviceState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)"></a>を呼び出し、結果の<strong>IRP_MN_QUERY_PNP_DEVICE_STATE</strong>要求にこのフラグを設定します。</p>
<p>このビットがデバイスに対して設定されている場合、PnP マネージャーは、デバイスの親デバイス (親デバイス) にこの設定を反映します。</p>
<p>このビットがルートで列挙されたデバイスに対して設定されている場合、デバイスを無効にしたり、アンインストールしたりすることはできません。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_REMOVED</td>
<td><p>デバイスは物理的に削除されています。</p></td>
</tr>
<tr class="even">
<td>PNP_DEVICE_RESOURCE_REQUIREMENTS_CHANGED</td>
<td><p>デバイスのリソース要件が変更されました。</p>
<p>通常、バスドライバーは、新しい子デバイスを列挙するためにリソース要件を拡張する必要があると判断したときに、このフラグを設定します。</p></td>
</tr>
<tr class="odd">
<td>PNP_DEVICE_DISCONNECTED</td>
<td><p>デバイスドライバーが読み込まれていますが、このドライバーは、デバイスがコンピューターに接続されていないことを検出しました。 通常、このフラグは、ワイヤレスデバイスと通信する関数ドライバーに使用されます。 たとえば、デバイスが範囲外に移動したときにフラグが設定され、デバイスが範囲内に戻り、再接続された後にクリアされます。</p>
<p>通常、バスドライバーはこのフラグを設定しません。 デバイスが接続されていない場合は、代わりに、バスドライバーが子デバイスの列挙を停止する必要があります。 このフラグは、関数ドライバーが接続を管理する場合にのみ使用されます。</p>
<p>このフラグの唯一の目的は、デバイスが接続されているかどうかをクライアントに通知することです。 フラグを設定しても、ドライバーが読み込まれるかどうかには影響しません。</p></td>
</tr>
</tbody>
</table>

 

PnP マネージャーは、デバイスを起動した直後にデバイスの PNP\_デバイス\_状態を照会します。これには、IRP\_完了した **\_クエリ\_pnp\_デバイス\_状態**要求をデバイススタックに送信します。 この IRP に応答して、デバイスのドライバーによって、PNP\_デバイス\_状態の適切なフラグが設定されます。

最初のクエリの後に状態の特性が変化した場合、ドライバーは[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)を呼び出すことによって PnP マネージャーに通知します。 PnP マネージャーは、 **IoInvalidateDeviceState**への呼び出しに応答して、デバイスの PNP\_デバイス\_状態を再度照会します。

デバイスが PNP\_とマークされている場合\_\_DISABLEABLE が許可されていないと、デバッガーによって、devnode の DNUF\_\_DISABLEABLE ユーザーフラグが表示されます。 デバッガーでは、デバイスを無効にできない理由の数をカウントする**Disableabledepends**値も表示されます。 この値は X + Y の合計です。 X は、デバイスを無効にできない場合は1、Y は無効にできないデバイスの子デバイスの数を示します。




