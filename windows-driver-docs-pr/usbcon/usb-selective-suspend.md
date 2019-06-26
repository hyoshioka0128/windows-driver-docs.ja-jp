---
Description: このセクションでは、セレクティブ サスペンド機能の適切なメカニズムの選択についての情報を提供します。
title: USB セレクティブ サスペンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33f661b9d2b4d406103a330c4dadf85478b7ce59
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356585"
---
# <a name="usb-selective-suspend"></a>USB セレクティブ サスペンド


このセクションでは、セレクティブ サスペンド機能の適切なメカニズムの選択についての情報を提供します。

Microsoft Windows XP およびそれ以降のオペレーティング システムでは、USB core スタックは、の修正バージョンをサポートしています、"選択的な中断"機能。 ユニバーサル シリアル バス仕様のバージョン 2.0 で説明します。

USB のセレクティブ サスペンド機能は、ハブ上の他のポートの操作の影響を与えずに、個々 のポートを中断するハブのドライバーを使用できます。 USB デバイスの選択的に中断は、により、バッテリ電源を節約するためにポータブル コンピューターで特に便利です。 指紋リーダー、生体認証スキャナーの他の種類など、多数のデバイスのみ、電源を断続的に必要です。 全体的な電力を削減する、デバイスが、使用されていないときに、このようなデバイスを中断する消費します。 さらに、選択的に中断されていない任意のデバイスでは、システム メモリ内で上に存在する、転送スケジュールを無効にする USB ホスト コント ローラーをできない可能性があります。 ホスト コント ローラーで、スケジューラへの DMA 転送すると、システムのプロセッサが C3 などのより深いスリープ状態を入力するようにできます。 Windows 選択的な中断動作は Windows XP および Windows Vista 以降のバージョンの Windows で動作しているデバイスに異なります。

2 つの異なるメカニズムの USB デバイスを選択的に中断がある: アイドル状態の要求の Irp ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) power Irp を設定し、([**IRP\_MN\_設定\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power))。 使用するためのメカニズムは、オペレーティング システムとデバイスの種類によって異なります。 複合または複合ではないです。

##  <a name="selecting-a-selective-suspend-mechanism"></a>選択的な選択メカニズムを中断


待機とリモート ウェイク アップするためのインターフェイスを有効にする複合デバイスでは、上のインターフェイス用のクライアント ドライバーは IRP をスリープ解除 (IRP\_MN\_待機\_WAKE)、IRP のアイドル状態の要求を使用する必要があります ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification))、デバイスをセレクティブ サスペンドするためのメカニズムです。

リモート ウェイク アップの詳細についてを参照してください。

[USB デバイスのリモート ウェイク アップ](https://docs.microsoft.com/windows-hardware/drivers/usbcon/remote-wakeup-of-usb-devices)

[待機またはスリープ解除操作の概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-wait-wake-operation)

オペレーティング システムでは、非複合デバイス方法ドライバーにより、選択的かを判断します。 Windows のバージョンを中断します。

-   Windows XP:Windows XP ですべてのクライアント ドライバーは Irp のアイドル状態の要求を使用する必要があります ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 自分のデバイスの電源をします。 クライアント ドライバーでは、自分のデバイスをセレクティブ サスペンドを WDM power Irp を使用する必要があります。 これにより、その他のデバイスは、選択的に中断できなくなります。 詳細については、「USB グローバル中断」を参照してください。
-   Windows Vista と Windows の以降のバージョン:ドライバー作成者には、Windows Vista 以降のバージョンの Windows でのデバイスの電源の複数の選択肢があります。 Windows Vista には、Windows のアイドル状態要求 IRP のメカニズムがサポートされていますが、ドライバーを使用する必要はありません。

次の表に、IRP のアイドル状態の要求の使用を必要とするシナリオと、USB デバイスを中断する WDM power IRP が使用できるものを示します。

| Windows のバージョン     | 複合デバイスでウェイク アップの武装関数 | 複合デバイスでのウェイク アップしない武装関数 | 1 つのインターフェイスの USB デバイス |
|---------------------|----------------------------------------------|--------------------------------------------------|-----------------------------|
| Windows 7           | IRP アイドル状態の要求を使用する必要があります。                    | WDM Power IRP を使用できます。                            | WDM Power IRP を使用できます。       |
| Windows Server 2008 | IRP アイドル状態の要求を使用する必要があります。                    | WDM Power IRP を使用できます。                            | WDM Power IRP を使用できます。       |
| Windows Vista       | IRP アイドル状態の要求を使用する必要があります。                    | WDM Power IRP を使用できます。                            | WDM Power IRP を使用できます。       |
| Windows Server 2003 | IRP アイドル状態の要求を使用する必要があります。                    | IRP アイドル状態の要求を使用する必要があります。                        | IRP アイドル状態の要求を使用する必要があります。   |
| Windows XP          | IRP アイドル状態の要求を使用する必要があります。                    | IRP アイドル状態の要求を使用する必要があります。                        | IRP アイドル状態の要求を使用する必要があります。   |



このセクションには、Windows 選択的な機構を中断して、次のトピックが含まれていますがについて説明します。

# <a name="sending-a-usb-idle-request-irp"></a>IRP USB アイドル状態要求を送信します。


クライアント ドライバーが IRP アイドル状態要求を送信して、バス ドライバーを通知するとき、デバイスがアイドル ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)). 低電力状態にし、デバイスも安全であると判断した場合、バス ドライバーは、クライアントのデバイス ドライバーが IRP のアイドル状態の要求でスタックに渡されたコールバック ルーチンを呼び出します。

コールバック ルーチンでクライアント ドライバーは保留中のすべての I/O 操作をキャンセルし、すべての USB I/O Irp を完了するまで待機する必要があります。 発行できます、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)に WDM デバイスの電源状態を変更する要求**D2**します。 コールバック ルーチンを待つ必要があります、 **D2**を返す前に完了する要求。 アイドル状態の通知のコールバック ルーチンの詳細については、「USB アイドル状態の通知コールバック ルーチン」を参照してください。

バス ドライバーでは、アイドル状態の通知のコールバック ルーチンを呼び出した後 IRP のアイドル状態の要求は完了しません。 代わりに、バス ドライバーを保持、アイドル状態、次の条件のいずれかが true になるまで、保留中の IRP を要求します。

-   **IRP\_MN\_SUPRISE\_削除**または**IRP\_MN\_削除\_デバイス IRP**を受信します。 これらの Irp のいずれかが受信されたとき IRP の完了状態でアイドル状態の要求\_キャンセルします。
-   バス ドライバーがデバイスを動作の電源状態にする要求を受信 (**D0**)。 この要求を受け取ったバス ドライバーは保留中のアイドル状態の要求状態 IRP が完了した\_成功します。

アイドル状態の要求の Irp の使用には次の制限が適用されます。

-   ドライバーは、デバイスの電源状態である必要があります**D0** IRP アイドル状態要求を送信するときにします。
-   ドライバーは、デバイス スタックごとに 1 つだけアイドル状態要求 IRP を送信する必要があります。

次のコードの WDM 例では、デバイス ドライバーが IRP USB アイドル状態要求の送信を取る手順を示します。 エラー チェックは、次のコード例で省略されています。

1.  割り当てし、初期化、 [ **IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification) IRP
    ```cpp
    irp = IoAllocateIrp (DeviceContext->TopOfStackDeviceObject->StackSize, FALSE);
    nextStack = IoGetNextIrpStackLocation (irp);
    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_IDLE_NOTIFICATION;
    nextStack->Parameters.DeviceIoControl.InputBufferLength =
    sizeof(struct _USB_IDLE_CALLBACK_INFO);
    ```

2.  割り当てるし、アイドル状態の要求情報構造体の初期化 (USB\_IDLE\_コールバック\_情報)。
    ```cpp
    idleCallbackInfo = ExAllocatePool (NonPagedPool,
    sizeof(struct _USB_IDLE_CALLBACK_INFO));
    idleCallbackInfo->IdleCallback = IdleNotificationCallback;
    // Put a pointer to the device extension in member IdleContext
    idleCallbackInfo->IdleContext = (PVOID) DeviceExtension;  
    nextStack->Parameters.DeviceIoControl.Type3InputBuffer =
    idleCallbackInfo;
    ```

3.  完了ルーチンを設定します。

    クライアント ドライバーは IRP のアイドル状態の要求完了ルーチンを関連付ける必要があります。 アイドル状態の通知の完了ルーチンと例のコードの詳細については、「USB アイドル要求 IRP 完了ルーチン」を参照してください。

    ```cpp
    IoSetCompletionRoutine (irp,
     IdleNotificationRequestComplete,
       DeviceContext,
       TRUE,
       TRUE,
       TRUE);

    ```

4.  デバイスの拡張機能には、アイドル状態の要求を格納します。
    ```cpp
    deviceExtension->PendingIdleIrp = irp;

    ```

5.  親のドライバーにアイドル状態の要求を送信します。
    ```cpp
    ntStatus = IoCallDriver (DeviceContext->TopOfStackDeviceObject, irp);
    ```

## <a name="canceling-a-usb-idle-request"></a>USB のアイドル状態の要求を取り消しています


特定の状況では、デバイス ドライバーがアイドル状態の要求が、バス ドライバーに送信されました IRP をキャンセルする必要があります。 これが発生する場合、デバイスを削除すると、アクティブになりますアイドル状態になると、アイドル状態の要求を送信した後、またはシステム全体が低いシステム電源の状態に遷移する場合。

クライアント ドライバーでは、アイドル状態の IRP をキャンセルを呼び出して[ **IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp)します。 次の表では、アイドル状態の IRP をキャンセルする 3 つのシナリオについて説明し、ドライバーのアクションが実行する必要がありますを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>シナリオ</th>
<th>アイドル状態の要求の取り消し機構</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>クライアント ドライバーが IRP がアイドル状態をキャンセルし、USB ドライバー スタックは、「USB アイドル状態の通知コールバック ルーチン」呼び出されていません。</td>
<td><p>USB ドライバー スタックは、アイドル状態の IRP を完了します。 デバイスは決してため、 <strong>D0</strong>ドライバーでは、デバイスの状態は変更されません。</p></td>
</tr>
<tr class="even">
<td>クライアント ドライバーは IRP がアイドル状態に取り消さ、USB ドライバー スタックが USB アイドル状態の通知のコールバック ルーチンを呼び出しましたが、まだ返ってが。</td>
<td><p>クライアント ドライバーが IRP のキャンセルを呼び出された場合でも、USB のアイドル状態の通知コールバック ルーチンが呼び出されることができます。 この場合、クライアント ドライバーのコールバック ルーチンは、低電力状態にデバイスを同期的に送信してデバイスを電源もする必要があります。</p>
<p>クライアント ドライバーに送信できますし、デバイスが低電力状態にある場合、 <strong>D0</strong>要求。</p>
<p>または、ドライバーは IRP がアイドル状態を完了し、送信する USB ドライバー スタックの待機できる、 <strong>D0</strong> IRP します。</p>
<p>コールバック ルーチンは、デバイスを電源 IRP を割り当てるメモリの不足が原因の低電力状態にできない場合はアイドル状態の IRP をキャンセルする必要があり、即座に終了します。 コールバック ルーチンが返されます。 までアイドル状態の IRP は完了しませんそのため、コールバック ルーチンを完了するキャンセルされたアイドル IRP の待機をブロックしないでください。</p></td>
</tr>
<tr class="odd">
<td>デバイスは、既に低電力状態にされています。</td>
<td><p>クライアント ドライバーが送信するデバイスが省電力状態で既に場合、 <strong>D0</strong> IRP します。 USB ドライバー スタックは、アイドル状態の要求に STATUS_SUCCESS IRP を完了します。</p>
<p>または、ドライバーをアイドル状態の IRP をキャンセル、USB ドライバー スタックがアイドル状態の IRP の完了するを待機し、送信、 <strong>D0</strong> IRP します。</p></td>
</tr>
</tbody>
</table>

## <a name="usb-idle-request-irp-completion-routine"></a>USB アイドル状態の要求の IRP の完了ルーチン


多くの場合、バス ドライバーはドライバーのアイドル状態要求 IRP の完了ルーチンを呼び出すことができます。 この場合、クライアント ドライバー、バス ドライバーは IRP を完了した理由を検出する必要があります。 返されるステータス コードは、この情報を提供できます。 状態コードの状態でない場合\_POWER\_状態\_無効な場合、ドライバーそのデバイスを配置する必要があります**D0** 、デバイスがでない場合**D0**します。 デバイスがアイドル状態のままの場合、ドライバーは IRP に別のアイドル状態の要求を送信できます。

**注**IRP の完了ルーチンのアイドル状態の要求を待機しているブロックされないようにする必要があります、 **D0** power 要求が完了します。 完了ルーチンは、ハブのドライバーで電源 IRP のコンテキストで呼び出されることができ、デッドロックが発生する別能力 IRP の完了ルーチンでブロックされている可能性があります。

次の一覧は、アイドル状態の要求の完了ルーチンがいくつかの一般的なステータス コードを解釈する方法を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_SUCCESS</p></td>
<td><p>デバイスを中断不要になったことを示します。 ただし、ドライバーことを確認自分のデバイス電源に<strong>D0</strong>にされていない場合<strong>D0</strong>します。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_CANCELLED</p></td>
<td><p>バス ドライバーでは、アイドル状態の要求で、次の状況のいずれかで STATUS_CANCELLED IRP を実行します。</p>
<ul>
<li>デバイス ドライバーは IRP が取り消されました。</li>
<li>システム電源の状態の変更が必要です。</li>
<li>Windows xp で接続された USB デバイスのいずれかのデバイス ドライバーはそのデバイスにできませんでした。 <strong>D2</strong> 、アイドル状態の要求のコールバック ルーチンの実行中にします。 その結果、バス ドライバーには、すべての保留中のアイドル状態要求 Irp が完了しました。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>STATUS_POWER_STATE_INVALID</p></td>
<td><p>デバイス ドライバーが要求したことを示します、 <strong>D3</strong>電源のデバイスの状態。 このような場合は、バス ドライバーは STATUS_POWER_STATE_INVALID ですべての保留中のアイドル状態 Irp を完了します。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_DEVICE_BUSY</p></td>
<td><p>バス ドライバーがデバイスのアイドル状態要求の保留中の IRP を既に保持していることを示します。 1 つだけアイドル状態の IRP が保留されている特定のデバイスの時刻にします。 複数のアイドル状態の要求の Irp を送信して、電源ポリシーの所有者の側でエラーが発生、ドライバーのライターでアドレス指定する必要があります。</p></td>
</tr>
</tbody>
</table>



次のコード例では、アイドル状態の要求の完了ルーチンの実装例を示します。

```ManagedCPlusPlus
/*Routine Description:

  Completion routine for idle notification IRP

Arguments:

    DeviceObject - pointer to device object
    Irp - I/O request packet
    DeviceExtension - pointer to device extension

Return Value:

    NT status value

--*/

NTSTATUS
IdleNotificationRequestComplete(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp,
    IN PDEVICE_EXTENSION DeviceExtension
    )
{
    NTSTATUS                ntStatus;
    POWER_STATE             powerState;
    PUSB_IDLE_CALLBACK_INFO idleCallbackInfo;

    ntStatus = Irp->IoStatus.Status;

    if(!NT_SUCCESS(ntStatus) && ntStatus != STATUS_NOT_SUPPORTED) 
    {

        //Idle IRP completes with error.

        switch(ntStatus) 
        {

        case STATUS_INVALID_DEVICE_REQUEST:

            //Invalid request.

            break;

        case STATUS_CANCELLED:

            //1. The device driver canceled the IRP. 
            //2. A system power state change is required. 

            break;

        case STATUS_POWER_STATE_INVALID:

            // Device driver requested a D3 power state for its device
            // Release the allocated resources.

            goto IdleNotificationRequestComplete_Exit;

        case STATUS_DEVICE_BUSY:

            //The bus driver already holds an idle IRP pending for the device.

            break;

        default:
            break;

        }


        // If IRP completes with error, issue a SetD0

        //Increment the I/O count because
        //a new IRP is dispatched for the driver.
        //This call is not shown.

        powerState.DeviceState = PowerDeviceD0;

        // Issue a new IRP
        PoRequestPowerIrp (
            DeviceExtension->PhysicalDeviceObject, 
            IRP_MN_SET_POWER, 
            powerState, 
            (PREQUEST_POWER_COMPLETE) PoIrpCompletionFunc, 
            DeviceExtension, 
            NULL);
    }

IdleNotificationRequestComplete_Exit:

    idleCallbackInfo = DeviceExtension->IdleCallbackInfo;

    DeviceExtension->IdleCallbackInfo = NULL;

    DeviceExtension->PendingIdleIrp = NULL;

    InterlockedExchange(&DeviceExtension->IdleReqPend, 0);

    if(idleCallbackInfo)
    {
        ExFreePool(idleCallbackInfo);
    }

    DeviceExtension->IdleState = IdleComplete;

    // Because the IRP was created using IoAllocateIrp,
    // the IRP needs to be released by calling IoFreeIrp.
    // Also return STATUS_MORE_PROCESSING_REQUIRED so that
    // the kernel does not reference this.

    IoFreeIrp(Irp);

    KeSetEvent(&DeviceExtension->IdleIrpCompleteEvent, IO_NO_INCREMENT, FALSE);

    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

## <a name="usb-idle-notification-callback-routine"></a>USB のアイドル状態の通知コールバック ルーチン


デバイスの子を中断しても安全な場合、バス ドライバー (ハブ ドライバーのインスタンス) または一般的な親ドライバーのいずれかを決定します。 場合は、それぞれの子のクライアント ドライバーによって提供されるアイドル通知コールバック ルーチンを呼び出します。

USB の関数のプロトタイプ\_IDLE\_コールバックを次に示します。

``` syntax
typedef VOID (*USB_IDLE_CALLBACK)(__in PVOID Context);
```

デバイス ドライバーは、アイドル状態の通知コールバック ルーチンで次の操作を実行する必要があります。

-   要求、 [ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)デバイスは、リモート ウェイク アップ装備する必要がある場合、デバイスの IRP します。
-   すべての I/O をキャンセルし、低電力状態に移動するデバイスを準備します。
-   WDM スリープ状態に呼び出すことによって、デバイスを配置[ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)で、 *PowerState* PowerDeviceD2 (wdm.h; で定義されている列挙子の値に設定するパラメーターntddk.h)。 Windows xp の場合、ドライバーする必要がありますいないにそのデバイス PowerDeviceD3、場合でも、デバイスがリモート ウェイクの有効活用されません。

Windows xp の場合、ドライバーは、アイドル状態の通知のコールバック ルーチンが、デバイスをセレクティブ サスペンドを依存する必要があります。 Windows XP で実行されているドライバーは、低電力状態で、デバイスをアイドル状態の通知のコールバック ルーチンを使用せずに直接 puts、中断してから、USB デバイス ツリー内の他のデバイスこのできない場合があります。 詳細については、「USB グローバル中断」を参照してください。

ハブ ドライバーと[USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md) IRQL でアイドル状態の通知のコールバック ルーチンを呼び出す = パッシブ\_レベル。 これにより、電源状態の変更要求が完了するまで待機する間にブロックするコールバック ルーチン。

システムが中にのみ、コールバック ルーチンが呼び出される**S0**であり、デバイス**D0**します。

アイドル状態の要求の通知コールバック ルーチンに次の制限が適用されます。

-   デバイス ドライバーがからデバイスの電源状態遷移を開始できる**D0**に**D2**アイドル状態の通知コールバック ルーチンが他の電源の状態遷移が許可されています。 具体的には、ドライバーを読み取ろうとしないでにそのデバイスを変更する**D0**コールバック ルーチンの実行中にします。
-   デバイス ドライバーは、アイドル状態の通知のコールバック ルーチン内では、複数の電源から IRP を要求する必要があります。

### <a name="arming-devices-for-wakeup-in-the-idle-notification-callback-routine"></a>デバイスをアイドル状態の通知コールバック ルーチンでウェイク アップ取り組ま


アイドル状態の通知のコールバック ルーチンがそのデバイスがあるかどうかを決定する必要があります、 [ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)保留中の要求。 場合ありません IRP\_MN\_待機\_スリープ解除要求が保留中、コールバック ルーチンは IRP を送信する必要があります\_MN\_待機\_デバイスを中断する前にスリープ解除要求。 待機のスリープ解除メカニズムの詳細については、次を参照してください。[をサポートしているデバイスをあるウェイク アップ機能](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)します。


## <a name="usb-global-suspend"></a>USB のグローバルの一時停止します。


USB 2.0 仕様グローバルの一時停止として定義バス USB ホスト コント ローラーの背後にある全体の中断開始-フレームのパケットをなど、バス上のすべての USB トラフィックを停止しています。 既に中断されていないダウン ストリーム デバイスは、アップ ストリームのポートでアイドル状態を検出し、自身で中断状態を入力します。 Windows を実装しませんグローバル中断この方法で。 Windows では、バス上のすべての USB トラフィックが停止します。 前に、USB ホスト コント ローラーの背後にある各 USB デバイスが常に選択的に中断します。

-   [条件のグローバルな Windows 7 での中断](#conditions-for-global-suspend-in-windows-7)
-   [条件のグローバルな Windows Vista での中断](#conditions-for-global-suspend-in-windows-vista)
-   [条件のグローバルな Windows XP での中断](#conditions-for-global-suspend-in-windows-xp)
-   [関連トピック](#related-topics)

### <a name="conditions-for-global-suspend-in-windows-7"></a>条件のグローバルな Windows 7 での中断


Windows 7 より積極的に Windows Vista よりも USB ハブを選択的に中断します。 Windows 7 の USB ハブのドライバーは、すべての接続されているデバイスのいずれかのハブをセレクティブ サスペンド**D1**、 **D2**、または**D3**デバイスの電源状態。 すべての USB ハブは、オプションを選択すると、バス全体をグローバル中断入ります中断します。 デバイスが WDM デバイス状態のときにアイドル状態として扱われます、デバイスを Windows 7 の USB ドライバー スタック**D1**、 **D2**、または**D3**します。

### <a name="conditions-for-global-suspend-in-windows-vista"></a>条件のグローバルな Windows Vista での中断


グローバルの一時停止を行うための要件は、Windows xp よりも Windows Vista をより柔軟です。

デバイスが WDM デバイス状態のときに、USB スタックでデバイスを Windows Vista でのアイドル状態として処理する具体的には、 **D1**、 **D2**、または**D3**します。

次の図は、Windows Vista で行われるシナリオを示しています。

![windows vista では、グローバルなを示すダイアグラムを中断します。](images/global-suspendlh.png)

この図は、"条件のグローバルな中断で Windows XP"セクションに示すように 1 つに似た状況を示しています。 ただし、ここでデバイスの 3 と見なされるアイドル状態のデバイス。 すべてのデバイスはアイドル状態であるため、バス ドライバーは Irp の保留中のアイドル状態要求に関連付けられているコールバック ルーチンのアイドル状態の通知を呼び出すことができません。 各ドライバーは、そのデバイスを中断し、バス ドライバーは、これを行うには安全ではすぐに、USB ホスト コント ローラーを中断します。

Windows Vista ではハブ以外のすべての USB デバイスである必要があります**D1**、 **D2**、または**D3**グローバル中断を開始する、前にどの時点で、ルート ハブを含む、すべての USB ハブになります中断されています。 選択的にサポートしない任意の USB クライアント ドライバーを中断することを意味すると、バスがグローバルの一時停止を入力できなくなります。

### <a name="conditions-for-global-suspend-in-windows-xp"></a>条件のグローバルな Windows XP での中断


Windows XP で電力の削減を最大化するためには、すべてのデバイス ドライバーが Irp のアイドル状態の要求を使用して、そのデバイスを中断することが重要です。 1 つのドライバーでは、そのデバイスを中断する場合は、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)要求代わりに、アイドル状態の IRP には、その他のデバイスが中断するように可能性があります。

次の図は、Windows XP で行われるシナリオを示しています。

![windows xp では、グローバルなを示すダイアグラムを中断します。](images/global-suspendxp.png)

この図では、デバイス 3 D3 の電源状態し、アイドル状態が保留中の IRP を要求します。 デバイス 3 を満たさず、グローバルの目的でアイドル状態のデバイスが Windows xp の場合、suspend、親のアイドル状態の要求の保留中の IRP があるないためです。 これは、ため、バス ドライバーがアイドル状態の要求ツリーで、その他のデバイスのドライバーに関連付けられているコールバック ルーチンを呼び出すことはできません。

## <a name="enabling-selective-suspend"></a>選択的に有効化を中断


セレクティブ サスペンドのアップグレードのバージョンの Microsoft Windows XP は無効です。 Windows XP、Windows Vista、および以降のバージョンの Windows のクリーン インストールする場合は有効です。

選択的に有効にする特定のルート ハブとその子デバイスのサポートを中断、チェック ボックスをオンにする、**電源管理** タブで、USB ルート ハブの**デバイス マネージャー**します。

または、有効にできますかの値を設定して無効にする選択的なが中断**HcDisableSelectiveSuspend**の USB ポート ドライバー ソフトウェア キーの下。 選択的に 1 つの無効化の値を中断します。 選択的な 0 の有効値を中断します。

たとえば、Hydra OHCI コント ローラーの Usbport.inf 無効にする選択的には、次の行が中断します。

```cpp
[OHCI_NOSS.AddReg.NT]
HKR,,"HcDisableSelectiveSuspend",0x00010001,1
```

クライアント ドライバーは選択的かどうかを判断しようとはしないでください中断がアイドル状態の要求を送信する前に有効になっています。 デバイスのアイドル時間がアイドル状態の要求を送信する必要があります。 アイドル状態の要求が失敗すると、クライアント ドライバーがアイドル タイマーをリセットする必要があります、再試行しています。

## <a name="related-topics"></a>関連トピック
[USB 電源管理](usb-power-management.md)  



