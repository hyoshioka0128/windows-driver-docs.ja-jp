---
title: IRP_MN_DEVICE_USAGE_NOTIFICATION
description: システムコンポーネントは、この IRP を送信して、デバイスが特別なファイルをサポートできるかどうかをデバイスのドライバーに要求します。
ms.date: 08/12/2017
ms.assetid: d8287ba2-ac0a-4407-b587-a5aa5b3617a2
keywords:
- IRP_MN_DEVICE_USAGE_NOTIFICATION カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 0d0622b992e69fcf7fb5e112e49ed1e666125c82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838590"
---
# <a name="irp_mn_device_usage_notification"></a>IRP\_\_デバイス\_使用状況\_通知


システムコンポーネントは、この IRP を送信して、デバイスが*特別なファイル*をサポートできるかどうかをデバイスのドライバーに要求します。 特別なファイルとしては、ページングファイル、ダンプファイル、休止状態ファイルなどがあります。 デバイスのすべてのドライバーが IRP に成功した場合、システムは特殊なファイルを作成します。 また、この IRP は、デバイスから特別なファイルが削除されたことをドライバーに通知するためにも送信します。

関数ドライバーは、デバイスにページングファイル、ダンプファイル、または休止状態ファイルを含めることができる場合に、この IRP を処理する必要があります。 フィルタードライバーがフィルター処理を行う関数ドライバーが IRP を処理する場合、フィルタードライバーはこの IRP を処理する必要があります。 バスドライバーは、アダプターまたはコントローラー (bus FDO) とその子デバイス (子 PDOs) に対して、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

システムは、ページングファイル、ダンプファイル、または休止状態ファイルを作成または削除するときに、この IRP を送信します。 デバイスの電源管理の関係が従来の親子関係の外部にある場合、ドライバーはこの IRP を送信して、デバイスの使用状況情報を別のデバイススタックに伝達することができます。 詳細については、IRP\_の**Powerrelations**要求の説明を参照してください[ **\_クエリ\_デバイス\_関係**](irp-mn-query-device-relations.md)です。

システムコンポーネントとドライバーは、任意のスレッドコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_STACK\_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**UsageNotification**メンバーはブール値です。 このパラメーターが**TRUE**の場合、システムはデバイス上にページング、クラッシュダンプ、または休止状態ファイルを作成します。 **Inpath**が**FALSE**の場合、このようなファイルはデバイスから削除されています。

**UsageNotification**は、ファイルの種類を示す列挙型です。 このパラメーターには、 **DeviceDeviceUsageTypeDumpFile Typepaging**、、または**device typeハイバネーション**のいずれかの値が含まれます。

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは **、Irp&gt;iostatus. status**を STATUS\_SUCCESS または適切なエラー状態に設定します。

ドライバーは、 **Irp&gt;IoStatus. 情報**フィールドを変更しません。IRP を送信するコンポーネントによって設定された0のままです。

<a name="operation"></a>操作
---------

ドライバーは、IRP がデバイススタックをダウンする前にこの IRP を処理し、IRP の方法でスタックをバックアップします。

ドライバーは、次のようなプロシージャを使用して、この IRP に応答します。

-   **UsageNotification**が**TRUE**の場合は、デバイスが特別なファイルをサポートしているかどうかを確認します。

    ドライバーは、ドライバーがサポートできる特定の**UsageNotification**(s) をテストする必要があります。 その他の通知の種類は、今後追加される可能性があります。

    各通知の種類をサポートするために必要なアクションについては、以下の詳細情報を参照してください。

    **UsageNotification**が**TRUE**で、ドライバーがデバイス上の特殊ファイルをサポートできない場合、ドライバーはエラー状態の IRP を完了する必要があります。

-   デバイスが特別なファイルをサポートしている場合は、次のようになります。

    1.  適切な操作を行って、デバイスに特別なファイルが含まれているか、それが含まれていないことを反映します。

        ドライバーは、通常、カウンターを増減します。 たとえば、 **UsageNotification**が**Device Typepaging**および**UsageNotification**である場合は、デバイス上のページングファイルの数をインクリメントしています。この値は**TRUE**です。 特定のドライバーディスパッチルーチンでは、カウンターを確認する必要があります。

        特別なファイルを含むデバイスは無効にしないでください。 ドライバーは[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)を呼び出すことができ、pnp マネージャーはデバイスの pnp デバイスの状態情報を再照会するように要求します。 生成された[**IRP\_\_クエリ\_pnp\_デバイス\_状態**](irp-mn-query-pnp-device-state.md)IRP に応答して、ドライバーは PNP\_デバイス\_\_disableable フラグを設定する必要があります。

        **Inpath**が**FALSE**の場合、ドライバーはデバイスのデバイスオブジェクトに [DO\_POWER\_pagable] ビットを設定します。

    2.  デバイスの使用状況情報を、情報を必要とする関連デバイスに伝達します。

        **Irp\_\_デバイス\_使用状況\_通知**irp の処理の一環として、1つまたは複数の他のデバイススタックに情報を渡すためにドライバーが必要になる場合があります。 このようなドライバーは、NOTIFICATION irp (または Irp)\_通知 irp (または Irp) の\_使用して、新しい**IRP\_\_** 作成し、適切なデバイススタック (またはスタック) に送信します。 ドライバーは、受信したデバイス使用状況の IRP の処理がドライバーによって完了される前に、送信されたデバイス使用状況通知 IRP の完了を待機する必要があります。

        関連するデバイスを識別する方法は、デバイスとドライバーによって異なります。 通常、ドライバーは、そのファイルに対して i/o 要求を送信する他のドライバーに IRP を送信します。 バスドライバーが子デバイスに対してこの要求を処理するときは、デバイスの親のデバイススタックに使用状況通知 IRP を送信する必要があります。

        たとえば、ftdisk で5台のディスクストライプセットが実行されている場合、ページング通知はこれらの5つの各ディスクに反映されます。これは、これらの各デバイスがページングファイル操作を処理する必要があるためです。

    3.  関数またはフィルタードライバーで、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定します。

    4.  関数またはフィルタードライバーで、 **irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定し、次のスタックの場所を設定して、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して irp を次の下位のドライバーに渡します。 IRP を完了しないでください。

        子 PDO の IRP を処理しているバスドライバーでは、 **irp-&gt;iostatus. Status**を設定して、Irp ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了します。

    5.  IRP 完了処理中:

        *Iocompletion*ルーチンが、下位のドライバーが irp に障害を検出したことを検出した場合、関数またはフィルタードライバーは、irp に応答して実行されたすべての操作を元に戻し、エラーを伝達する必要があります。 関数またはフィルタードライバーが使用状況の情報を他のデバイススタックに伝達した場合、ドライバーは、そのスタックに別の使用状況の IRP を送信して、エラーが発生したことを通知する必要があります。

        Status が STATUS\_SUCCESS および**Inpath**が**TRUE**の場合は、[DO\_パワー\_pagable] ビットをオフにします。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**デバイスでのページング、クラッシュダンプ、および休止状態ファイルのサポート**

ドライバーの特別なファイルカウントが0以外の場合、ドライバーはデバイス (または派生デバイス) に特殊なファイルが存在することをサポートする必要があります。

デバイス上に作成された**device使用 Typepaging**ファイルの場合、ドライバーは次の操作を行う必要があります。

-   [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)の各ルーチンのメモリ内のコードをロックします。

-   デバイスのデバイスオブジェクト (IRP がデバイススタックの上にある状態) で、[DO\_POWER\_PAGABLE] ビットをオフにします。

-   **\_クエリ\_** 失敗した場合は、デバイスと**IRP\_** \_停止し、デバイスに対する\_デバイス要求を削除\_クエリを実行\_ます。

デバイス上の**DeviceUsageTypeDumpFile**ファイルの場合、ドライバーは次の操作を行う必要があります。

-   *DispatchRead*、 *DispatchWrite*、 *DispatchDeviceControl*、 *DispatchPower*の各ルーチンのメモリ内のコードをロックします。

-   デバイスを D0 状態から除外しないでください。

    アイドル状態の検出用にデバイスを登録しないでください ([**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection))。 デバイスが既に登録されている場合は、登録を取り消します。 ドライバーがデバイスに対して独自のアイドル検出を実行する場合は、そのような検出を中断します。

-   デバイスのデバイスオブジェクト (IRP がデバイススタックの上にある状態) で、[DO\_POWER\_PAGABLE] ビットをオフにします。

-   [ **\_クエリ\_** ](irp-mn-query-stop-device.md)失敗した場合は、デバイスと[**IRP\_** ](irp-mn-query-remove-device.md)\_停止し、デバイスに対する\_デバイス要求を削除\_クエリを実行\_ます。

デバイス上の**device使用 Typeハイバネーション**ファイルの場合、ドライバーは次の操作を行う必要があります。

-   *DispatchRead*、 *DispatchWrite*、 *DispatchDeviceControl*、 *DispatchPower*の各ルーチンのメモリ内のコードをロックします。

-   システムが休止状態になることを示す S4 システム電源 IRP をドライバーが受信したときに、デバイスが D0 状態になっていることを確認します。

-   S4 の休止状態アクションの一部である D3 set-電源 IRP に応答して、デバイスの電源を切ることは避けてください。 詳細については、「[システム電源アクション](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-actions)」を参照してください。

    このような D3 パワー IRP の受信時に、デバイスの電源をオフにして、電源マネージャーに通知する ([**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)) ことを除いて、デバイスを D3 状態にするために必要なすべてのタスクを実行します。 デバイスは、休止状態ファイルが書き込まれるまで電源を保持する必要があります。

-   デバイスのデバイスオブジェクト (IRP がデバイススタックの上にある状態) で、[DO\_POWER\_PAGABLE] ビットをオフにします。

-   [ **\_クエリ\_** ](irp-mn-query-stop-device.md)失敗した場合は、デバイスと[**IRP\_** ](irp-mn-query-remove-device.md)\_停止し、デバイスに対する\_デバイス要求を削除\_クエリを実行\_ます。

デバイスの電源状態、電源 Irp、およびドライバーでの電源管理のサポートの詳細については、「[電源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-power-management)」を参照してください。

**この IRP を送信しています**

ドライバーは、 **irp\_\_デバイス\_使用状況\_情報**irp に送信できますが、デバイス使用状況情報を別のデバイススタックに伝達するだけです。 ドライバーは、デバイスの使用状況情報の最初のソースではありません。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoAdjustPagingPathCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioadjustpagingpathcount)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_\_クエリ\_デバイス\_関係**](irp-mn-query-device-relations.md)

[**IRP\_\_クエリ\_PNP\_デバイス\_状態**](irp-mn-query-pnp-device-state.md)

[**IRP\_\_クエリ\_\_デバイスの削除**](irp-mn-query-remove-device.md)

[**IRP\_\_クエリ\_\_デバイスの停止**](irp-mn-query-stop-device.md)

[**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)

[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)

 

 




