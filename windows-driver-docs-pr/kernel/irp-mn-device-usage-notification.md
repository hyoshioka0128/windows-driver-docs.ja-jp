---
title: IRP_MN_DEVICE_USAGE_NOTIFICATION
description: システムのコンポーネントは、デバイスが特別なファイルをサポートできるかどうかのデバイス ドライバーを確認するには、この IRP を送信します。
ms.date: 08/12/2017
ms.assetid: d8287ba2-ac0a-4407-b587-a5aa5b3617a2
keywords:
- IRP_MN_DEVICE_USAGE_NOTIFICATION Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 2ce83261421bbddb47b3653a6ddff1e0707256c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368392"
---
# <a name="irpmndeviceusagenotification"></a>IRP\_MN\_デバイス\_使用状況\_通知


システム コンポーネント、デバイスがサポートできるかどうかのデバイス ドライバーを確認するには、この IRP の送信、*特殊なファイル*します。 特殊なファイルには、ページング ファイルには、ダンプ ファイル、休止状態ファイルが含まれます。 デバイスのすべてのドライバーが IRP を成功した場合は、特殊なファイルが作成されます。 システムには、この IRP が特別なファイルをデバイスから削除されたことをドライバーに通知するためにも送信します。

関数のドライバーは、自分のデバイスは、ページング ファイル、ダンプ ファイル、または休止状態ファイルに含めることができる場合、この IRP を処理する必要があります。 フィルター ドライバーは、フィルタ リングされている関数のドライバーが IRP を処理する場合、この IRP を処理する必要があります。 バス ドライバーには、この IRP のアダプターまたはコント ローラー (バス FDO) と、その子デバイス (子 Pdo) を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

システムは、作成またはページング ファイル、ダンプ ファイル、または休止状態ファイルを削除すると、この IRP を送信します。 デバイスが従来の親子リレーションシップの外側まで広がる電源管理の関係にある場合、ドライバーは別のデバイス スタックにデバイスの使用状況情報を伝達するには、この IRP を送信できます。 詳細については、の説明を参照して、 **PowerRelations**で要求[ **IRP\_MN\_クエリ\_デバイス\_リレーション**](irp-mn-query-device-relations.md).

システムのコンポーネントとドライバーは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.UsageNotification.InPath**のメンバー、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造は、ブール値。 このパラメーターが場合**TRUE**ページング、クラッシュ ダンプ、システムを作成または休止状態が、デバイスのファイルします。 ときに**InPath**は**FALSE**、このようなファイルがデバイスから削除されました。

**Parameters.UsageNotification.Type**はファイルの種類を示す列挙型。 このパラメーターは、次の値のいずれか。**DeviceUsageTypePaging**、 **DeviceUsageTypeDumpFile**、または**DeviceUsageTypeHibernation**します。

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバー セット**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。

ドライバーは変更しないでください、 **Irp -&gt;IoStatus.Information**フィールド; IRP を送信するコンポーネントによって設定された、0 のままです。

<a name="operation"></a>操作
---------

ドライバーは、デバイス スタック IRP の方法では、stack のバックアップの IRP の方法では、この IRP を処理します。

ドライバーは、次のようにプロシージャを使用したこの IRP に応答します。

-   場合**Parameters.UsageNotification.InPath**は**TRUE**デバイスが、特別なファイルをサポートするかどうかを確認します。

    特定のドライバーをテストする必要があります**Parameters.UsageNotification.Type**(s) ドライバーをサポートできます。 追加の通知の種類は、今後追加される可能性があります。

    各通知の種類をサポートするために必要なアクションについて説明した次の詳細を参照してください。

    場合**Parameters.UsageNotification.InPath**は**TRUE**と、ドライバーは、デバイス上の特別なファイルをサポートできない、ドライバーは IRP がエラー状態を完了する必要があります。

-   場合は、デバイスには、特殊なファイルがサポートされています。

    1.  デバイスが含まれているようになりましたか、特殊なファイルに含まれないことを反映するように適切なアクションを実行します。

        通常、ドライバーをインクリメントまたはカウンターをデクリメントします。 たとえば場合、 **Parameters.UsageNotification.Type**は**DeviceUsageTypePaging**と**Parameters.UsageNotification.InPath**は**TRUE**、デバイス上のページング ファイルの数のカウントをインクリメントします。 特定ドライバーのディスパッチ ルーチンは、カウンターを確認する必要があります。

        特殊なファイルを保持するデバイスを無効にしない必要があります。 ドライバーを呼び出すことができます[ **IoInvalidateDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff549361)、PnP マネージャーに再びクエリをデバイスの PnP デバイスの状態情報を要求します。 結果の応答で[ **IRP\_MN\_クエリ\_PNP\_デバイス\_状態**](irp-mn-query-pnp-device-state.md) IRP、ドライバーは PNPを設定する必要があります\_デバイス\_いない\_DISABLEABLE フラグ。

        場合**InPath**は**FALSE**、ドライバーの設定、DO\_POWER\_PAGABLE デバイスの場合は、そのデバイス オブジェクトのビットします。

    2.  関連するデバイス情報を必要とするデバイスの使用状況情報を伝達します。

        その処理の一環として、 **IRP\_MN\_デバイス\_使用状況\_通知**IRP、ドライバーが 1 つまたは複数の他のデバイス スタックに、情報を渡す必要あります。 このようなドライバーが新たに作成**IRP\_MN\_デバイス\_使用状況\_通知**IRP (または Irp) スタックの適切なデバイス (またはスタック) に送信します。 ドライバーは、ドライバーが受け取ったデバイス使用状況の IRP の処理を完了する前に送信する任意のデバイスの使用状況の通知 IRP(s) の完了を待つ必要があります。

        関連するデバイスを識別する方法は、デバイスとドライバーに固有です。 通常、ドライバーは IRP をファイルの I/O 要求を送信するには、他のドライバーに送信します。 バス ドライバーでは、子デバイスは、この要求を処理する場合は、デバイスの親のデバイス スタックを IRP の使用状況の通知を送信する必要があります。

        たとえば、ftdisk 5 のディスクのストライプ セットの実行中は、伝達各これら 5 つのディスクにページング通知ページング ファイルの操作を処理するために必要なこれらのデバイスの各できるためします。

    3.  関数またはフィルター ドライバー、設定、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン。

    4.  関数またはフィルター ドライバーでは、次のように設定します**Irp -&gt;IoStatus.Status**ステータス\_成功すると、次の設定の場所スタックが作成され、で [次へ] の下位のドライバーに IRP を渡す[  **。保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。 IRP を実行しないでください。

        子 PDO の IRP を処理している、バス ドライバー: 設定**Irp -&gt;IoStatus.Status** IRP を完了して ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343))。

    5.  IRP の完了処理。

        場合、 *IoCompletion*ルーチンが検出されると、下位のドライバーが IRP を失敗した関数またはフィルター ドライバーが IRP への応答で、実行されたすべての操作を元に戻すし、エラーを伝達する必要があります。 関数またはフィルター ドライバーには、その他の任意のデバイス スタックを使用状況情報が反映される、ドライバーはエラーを通知するためにこれらのスタックに別使用率の IRP を送信する必要があります。

        状態が状態の場合\_成功と**InPath**は**TRUE**、オフにします\_POWER\_ページング可能なビット。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**ページング、クラッシュ ダンプ、およびデバイス上に休止状態ファイルをサポートしています。**

ドライバーの特殊なファイルの数が 0 以外の場合、ドライバーは、そのデバイス (または子孫のデバイス) 上の特別なファイルの存在をサポートする必要があります。

**DeviceUsageTypePaging**ドライバー、デバイス上で作成されたファイルは、次を実行する必要があります。

-   用のメモリ内のコードのロックの[ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、 [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、 [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、および[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

-   オフにします\_POWER\_PAGABLE (デバイス スタックを IRP の方向) にデバイスの場合は、そのデバイス オブジェクトのビットします。

-   失敗**IRP\_MN\_クエリ\_停止\_デバイス**と**IRP\_MN\_クエリ\_削除\_デバイス**デバイスの要求。

**DeviceUsageTypeDumpFile**ドライバー、そのデバイス上のファイルは、次を実行する必要があります。

-   用のメモリ内のコードのロックの*DispatchRead*、 *DispatchWrite*、 *DispatchDeviceControl*、および*DispatchPower*ルーチン。

-   D0 状態から、デバイスはなりません。

    アイドル状態の検出については、デバイスを登録しないでください ([**PoRegisterDeviceForIdleDetection**](https://msdn.microsoft.com/library/windows/hardware/ff559721))。 デバイスが既に登録されている場合、登録をキャンセルします。 ドライバーは、デバイスのアイドル状態の検出を実行する場合は、このような検出を中断します。

-   オフにします\_POWER\_PAGABLE (デバイス スタックを IRP の方向) にデバイスの場合は、そのデバイス オブジェクトのビットします。

-   失敗[ **IRP\_MN\_クエリ\_停止\_デバイス**](irp-mn-query-stop-device.md)と[ **IRP\_MN\_クエリ\_削除\_デバイス**](irp-mn-query-remove-device.md)デバイスの要求。

**DeviceUsageTypeHibernation**ドライバー、そのデバイス上のファイルは、次を実行する必要があります。

-   用のメモリ内のコードのロックの*DispatchRead*、 *DispatchWrite*、 *DispatchDeviceControl*、および*DispatchPower*ルーチン。

-   ドライバーの受信、S4 システム電源 IRP を示すシステムが休止状態にしようとしているときに、デバイスが D0 の状態が確認します。

-   休止状態 D3 セット電力への応答でデバイスを電源 IRP S4 の一部であるアクション。 参照してください[システム電源操作](https://msdn.microsoft.com/library/windows/hardware/ff564553)詳細についてはします。

    D3 セット power IRP を受信すると、デバイスの電源を切ると電源マネージャーに通知を除く D3 状態で、デバイスを配置するために必要なすべてのタスクを実行します ([**PoSetPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff559765))。 デバイスは、休止状態ファイルが書き込まれるまでに電源を保持する必要があります。

-   オフにします\_POWER\_PAGABLE (デバイス スタックを IRP の方向) にデバイスの場合は、そのデバイス オブジェクトのビットします。

-   失敗[ **IRP\_MN\_クエリ\_停止\_デバイス**](irp-mn-query-stop-device.md)と[ **IRP\_MN\_クエリ\_削除\_デバイス**](irp-mn-query-remove-device.md)デバイスの要求。

参照してください[電源管理](https://msdn.microsoft.com/library/windows/hardware/ff547131)デバイスの電源状態の詳細については、Irp の電源をドライバーで電源管理をサポートします。

**この IRP を送信します。**

ドライバーを送信する、 **IRP\_MN\_デバイス\_使用状況\_情報**IRP、のみを別のデバイス スタックにデバイスの使用状況情報を伝達することができます。 ドライバーは、デバイスの使用状況情報の最初のソースではありません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IoAdjustPagingPathCount**](https://msdn.microsoft.com/library/windows/hardware/ff548209)

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MN\_クエリ\_デバイス\_リレーション**](irp-mn-query-device-relations.md)

[**IRP\_MN\_クエリ\_PNP\_デバイス\_状態**](irp-mn-query-pnp-device-state.md)

[**IRP\_MN\_クエリ\_削除\_デバイス**](irp-mn-query-remove-device.md)

[**IRP\_MN\_クエリ\_停止\_デバイス**](irp-mn-query-stop-device.md)

[**PoRegisterDeviceForIdleDetection**](https://msdn.microsoft.com/library/windows/hardware/ff559721)

[**PoSetPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff559765)

 

 




