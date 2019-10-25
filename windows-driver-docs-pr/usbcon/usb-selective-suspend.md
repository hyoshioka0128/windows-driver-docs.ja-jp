---
Description: ここでは、セレクティブサスペンド機能に適したメカニズムを選択する方法について説明します。
title: USB セレクティブ サスペンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e28084d10d9f201a5be66fac8da746d16c7f2db2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841686"
---
# <a name="usb-selective-suspend"></a>USB セレクティブ サスペンド

ここでは、セレクティブサスペンド機能に適したメカニズムを選択する方法について説明します。

Microsoft Windows XP 以降のオペレーティングシステムでは、USB コアスタックは、ユニバーサルシリアルバス仕様のリビジョン2.0 で説明されている "セレクティブサスペンド" 機能の変更されたバージョンをサポートしています。

USB のセレクティブサスペンド機能を使用すると、ハブドライバーはハブ上の他のポートの操作に影響を与えずに個々のポートを中断できます。 USB デバイスの選択的な中断は、バッテリ電源を節約するためにポータブルコンピューターで特に役立ちます。 指紋リーダーやその他の種類の生体認証スキャナーなど、多くのデバイスでは、断続的に電力を消費する必要があります。 このようなデバイスを中断すると、デバイスが使用されていないときに、全体的な電力消費量が削減されます。 さらに重要なこととして、選択的に中断されていないデバイスは、USB ホストコントローラーがシステムメモリ内に存在する転送スケジュールを無効にできない場合があります。 ホストコントローラーによるスケジューラへの DMA 転送によって、システムのプロセッサが C3 などのより詳細なスリープ状態を入力できなくなることがあります。 Windows のセレクティブサスペンドの動作は、windows XP および Windows Vista 以降のバージョンの Windows で動作するデバイスでは異なります。

USB デバイスを選択的に一時停止するには、アイドル要求の Irp ([**内部\_usb\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) の2つの異なるメカニズムを使用して、電源 irp を設定します ([**irp\_\_\_設定\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power))。 使用するメカニズムは、オペレーティングシステムとデバイスの種類 (複合または非複合) によって異なります。

## <a name="selecting-a-selective-suspend-mechanism"></a>選択的中断メカニズムの選択

クライアントドライバーは、複合デバイス上のインターフェイスに対して、待機ウェイク IRP (IRP\_\_WAIT\_WAKE) を使用したリモートウェイクアップのインターフェイスを有効にするために、アイドル状態の要求 IRP ([**IOCTL\_内部\_USB\_SUBMIT) を使用する必要があり\_IDLE\_NOTIFICATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) メカニズム。デバイスを選択的に中断します。

リモートウェイクアップの詳細については、以下を参照してください。

[USB デバイスのリモートウェイクアップ](https://docs.microsoft.com/windows-hardware/drivers/usbcon/remote-wakeup-of-usb-devices)

[待機/ウェイク操作の概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-wait-wake-operation)

Windows オペレーティングシステムのバージョンによって、非複合デバイスのドライバーで選択的中断が有効になる方法が決まります。

- Windows XP: Windows XP では、すべてのクライアントドライバーはアイドル状態の要求 Irp ([**IOCTL\_内部\_USB\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) を使用してデバイスの電源を切る必要があります。 クライアントドライバーは、WDM 電源 Irp を使用してデバイスを選択的に中断することはできません。 そうすることで、他のデバイスが選択的に中断されるのを防ぐことができます。 詳細については、「USB グローバル中断」を参照してください。
- Windows Vista 以降のバージョンの Windows: ドライバーライターには、Windows Vista およびそれ以降のバージョンの Windows でのデバイスの電源をオンにするための選択肢があります。 Windows Vista では Windows idle request IRP メカニズムがサポートされていますが、ドライバーで使用する必要はありません。

次の表は、アイドル要求の IRP を使用する必要があるシナリオと、WDM 電源 IRP を使用して USB デバイスを中断するシナリオを示しています。

| Windows のバージョン     | 複合デバイスで機能し、ウェイクに使用する | 複合デバイスで機能します。 Wake では使用できません | シングルインターフェイス USB デバイス |
|---------------------|----------------------------------------------|--------------------------------------------------|-----------------------------|
| Windows 7           | アイドル要求の IRP を使用する必要があります                    | WDM 電源 IRP を使用できる                            | WDM 電源 IRP を使用できる       |
| Windows Server 2008 | アイドル要求の IRP を使用する必要があります                    | WDM 電源 IRP を使用できる                            | WDM 電源 IRP を使用できる       |
| Windows Vista       | アイドル要求の IRP を使用する必要があります                    | WDM 電源 IRP を使用できる                            | WDM 電源 IRP を使用できる       |
| Windows Server 2003 | アイドル要求の IRP を使用する必要があります                    | アイドル要求の IRP を使用する必要があります                        | アイドル要求の IRP を使用する必要があります   |
| Windows XP          | アイドル要求の IRP を使用する必要があります                    | アイドル要求の IRP を使用する必要があります                        | アイドル要求の IRP を使用する必要があります   |

ここでは、Windows の選択的中断メカニズムについて説明し、次のトピックについて説明します。

## <a name="sending-a-usb-idle-request-irp"></a>USB アイドル要求 IRP を送信しています

デバイスがアイドル状態になると、クライアントドライバーはアイドル状態の要求を送信することによってバスドライバーに通知します。これは、アイドル状態の要求 IRP ([**IOCTL\_内部\_USB\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) です。 バスドライバーは、デバイスを低電力状態にするのが安全であると判断した後、クライアントデバイスドライバーがアイドル要求の IRP でスタックに渡したコールバックルーチンを呼び出します。

コールバックルーチンでは、クライアントドライバーはすべての保留中の i/o 操作をキャンセルし、すべての USB i/o Irp が完了するまで待機する必要があります。 次に、IRP デバイスの電源状態を**D2**に変更するために、 [ **\_電源要求\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された IRP\_を発行できます。 コールバックルーチンは、 **D2**要求が完了するのを待ってから制御を戻す必要があります。 アイドル状態の通知コールバックルーチンの詳細については、「USB アイドル通知コールバックルーチン」を参照してください。

バスドライバーは、アイドル状態の通知コールバックルーチンを呼び出した後、アイドル状態の要求 IRP を完了しません。 代わりに、バスドライバーは、次のいずれかの条件が満たされるまで保留中のアイドル要求 IRP を保持します。

- **Irp\_\_suprise**削除または**IRP\_\_削除\_デバイスの irp**を受信しました。 これらの Irp のいずれかを受信すると、アイドル状態の要求 IRP が完了し、状態\_取り消されます。
- バスドライバーは、デバイスを動作中の電源状態 (**D0**) にする要求を受信します。 この要求を受信すると、バスドライバーは状態\_SUCCESS で保留中のアイドル要求の IRP を完了します。

アイドル状態の要求 Irp の使用には、次の制限が適用されます。

- アイドル状態の要求の IRP を送信するときに、ドライバーはデバイスの電源状態の**D0**にある必要があります。
- ドライバーは、デバイススタックごとにアイドル状態の要求 IRP を1つだけ送信する必要があります。

次の WDM コード例は、デバイスドライバーが USB アイドル要求の IRP を送信するために実行する手順を示しています。 次のコード例では、エラーチェックは省略されています。

1. [**IOCTL\_内部\_USB\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)IRP の割り当てと初期化を行います。

    ```cpp
    irp = IoAllocateIrp (DeviceContext->TopOfStackDeviceObject->StackSize, FALSE);
    nextStack = IoGetNextIrpStackLocation (irp);
    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_IDLE_NOTIFICATION;
    nextStack->Parameters.DeviceIoControl.InputBufferLength =
    sizeof(struct _USB_IDLE_CALLBACK_INFO);
    ```

2. アイドル状態の要求情報の構造 (USB\_IDLE\_CALLBACK\_INFO) を割り当て、初期化します。

    ```cpp
    idleCallbackInfo = ExAllocatePool (NonPagedPool,
    sizeof(struct _USB_IDLE_CALLBACK_INFO));
    idleCallbackInfo->IdleCallback = IdleNotificationCallback;
    // Put a pointer to the device extension in member IdleContext
    idleCallbackInfo->IdleContext = (PVOID) DeviceExtension;  
    nextStack->Parameters.DeviceIoControl.Type3InputBuffer =
    idleCallbackInfo;
    ```

3. 完了ルーチンを設定します。

    クライアントドライバーは、完了ルーチンとアイドル要求の IRP を関連付ける必要があります。 アイドル状態の通知完了ルーチンとコード例の詳細については、「USB アイドル要求の IRP 完了ルーチン」を参照してください。

    ```cpp
    IoSetCompletionRoutine (irp,
        IdleNotificationRequestComplete,
        DeviceContext,
        TRUE,
        TRUE,
        TRUE);
    ```

4. デバイス拡張機能にアイドル状態の要求を格納します。

    ```cpp
    deviceExtension->PendingIdleIrp = irp;

    ```

5. アイドル状態の要求を親ドライバーに送信します。

    ```cpp
    ntStatus = IoCallDriver (DeviceContext->TopOfStackDeviceObject, irp);
    ```

## <a name="canceling-a-usb-idle-request"></a>USB アイドル要求をキャンセルしています

特定の状況下では、デバイスドライバーがバスドライバーに送信されたアイドル状態の要求 IRP をキャンセルする必要がある場合があります。 これは、デバイスが削除された場合、アイドル状態になった後にアクティブになり、アイドル状態の要求を送信した場合、またはシステム全体がより低いシステム電源状態に移行している場合に発生する可能性があります。

クライアントドライバーは、 [**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出して、アイドル状態の IRP をキャンセルします。 次の表では、アイドル状態の IRP をキャンセルし、ドライバーが実行する必要のあるアクションを指定する3つのシナリオについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>シナリオ</th>
<th>アイドル要求のキャンセルメカニズム</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>クライアントドライバーがアイドル状態の IRP をキャンセルし、USB ドライバースタックが "USB アイドル通知のコールバックルーチン" を呼び出していません。</td>
<td><p>USB ドライバースタックは、アイドル状態の IRP を完了します。 デバイスは<strong>D0</strong>のままではないため、ドライバーはデバイスの状態を変更しません。</p></td>
</tr>
<tr class="even">
<td>クライアントドライバーがアイドル状態の IRP をキャンセルしました。 USB ドライバースタックは、USB アイドル通知コールバックルーチンを呼び出しましたが、まだ返されていません。</td>
<td><p>クライアントドライバーが IRP で取り消しを呼び出した場合でも、USB アイドル通知コールバックルーチンが呼び出される可能性があります。 この場合、クライアントドライバーのコールバックルーチンは、デバイスを低電力状態に同期的に送信することによってデバイスの電源を切断する必要があります。</p>
<p>デバイスの電源がより低い状態になると、クライアントドライバーは<strong>D0</strong>要求を送信できるようになります。</p>
<p>また、ドライバーは、USB ドライバースタックがアイドル状態の IRP を完了するのを待ってから、 <strong>D0</strong> irp を送信することもできます。</p>
<p>パワー IRP を割り当てるためのメモリが不足しているため、コールバックルーチンがデバイスを低電力状態にすることができない場合は、アイドル状態の IRP をキャンセルしてすぐに終了する必要があります。 アイドル状態の IRP は、コールバックルーチンが返されるまで完了しません。したがって、コールバックルーチンは、取り消されたアイドル状態の IRP が完了するのを待機するのをブロックすることはできません。</p></td>
</tr>
<tr class="odd">
<td>デバイスは既に低電力状態になっています。</td>
<td><p>デバイスが既に低電力状態になっている場合、クライアントドライバーは<strong>D0</strong> IRP を送信できます。 USB ドライバースタックは、STATUS_SUCCESS を使用したアイドル状態の要求 IRP を完了します。</p>
<p>また、ドライバーはアイドル状態の IRP をキャンセルし、USB ドライバースタックがアイドル状態の IRP を完了するのを待ってから、 <strong>D0</strong> irp を送信することもできます。</p></td>
</tr>
</tbody>
</table>

## <a name="usb-idle-request-irp-completion-routine"></a>USB アイドル要求の IRP 完了ルーチン

多くの場合、バスドライバーはドライバーのアイドル要求の IRP 完了ルーチンを呼び出す可能性があります。 これが発生した場合、クライアントドライバーは、バスドライバーが IRP を完了した理由を検出する必要があります。 返されたステータスコードは、この情報を提供できます。 状態コードが状態でない場合\_電源\_状態\_無効である場合、デバイスがまだ**d0**にない場合は、ドライバーによってデバイスが**d0**に挿入されます。 デバイスがアイドル状態のままである場合、ドライバーは別のアイドル要求の IRP を送信できます。

**メモ** アイドル要求の IRP 完了ルーチンは、 **D0**の電源要求の完了の待機をブロックすることはできません。 完了ルーチンは、ハブドライバーによって電源 IRP のコンテキストで呼び出すことができます。また、完了ルーチンの別の電源 IRP でブロックすると、デッドロックが発生する可能性があります。

次の一覧は、アイドル状態の要求の完了ルーチンが、一般的なステータスコードを解釈する方法を示しています。

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
<td><p>デバイスが中断されないことを示します。 ただし、ドライバーは、デバイスの電源が入っていることを確認し<strong>、d0 に</strong>登録されていない場合はそれらを<strong>d0</strong>に配置する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_CANCELLED</p></td>
<td><p>バスドライバーは、次のいずれかの状況で、STATUS_CANCELLED を使用してアイドル状態の要求 IRP を完了します。</p>
<ul>
<li>デバイスドライバーが IRP を取り消しました。</li>
<li>システムの電源状態の変更が必要です。</li>
<li>Windows XP では、接続されているいずれかの USB デバイスのデバイスドライバーが、アイドル状態の要求コールバックルーチンの実行中に、そのデバイスを<strong>D2</strong>に配置できませんでした。 その結果、バスドライバーは保留中のアイドル状態の要求 Irp をすべて完了しました。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>STATUS_POWER_STATE_INVALID</p></td>
<td><p>デバイスドライバがデバイスの<strong>D3</strong>電源状態を要求したことを示します。 このエラーが発生すると、バスドライバーは、STATUS_POWER_STATE_INVALID を使用して保留中のすべてのアイドル状態の Irp を完了します。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_DEVICE_BUSY</p></td>
<td><p>バスドライバーが、デバイスに対して保留中のアイドル要求 IRP を既に保持していることを示します。 特定のデバイスに対して一度に保留できるアイドル状態の IRP は1つだけです。 複数のアイドル状態の要求 Irp を送信することは、電源ポリシーの所有者の一部でエラーとなり、ドライバーの作成者が対処する必要があります。</p></td>
</tr>
</tbody>
</table>

次のコード例は、アイドル状態の要求完了ルーチンの実装例を示しています。

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

## <a name="usb-idle-notification-callback-routine"></a>USB アイドル通知コールバックルーチン

バスドライバー (ハブドライバーのインスタンスまたは汎用の親ドライバー) によって、デバイスの子をいつ安全に中断できるかが決まります。 存在する場合は、各子のクライアントドライバーによって提供されるアイドル状態の通知コールバックルーチンを呼び出します。

USB\_アイドル\_コールバックの関数プロトタイプは次のとおりです。

``` syntax
typedef VOID (*USB_IDLE_CALLBACK)(__in PVOID Context);
```

デバイスドライバーは、アイドル通知コールバックルーチンで次の操作を行う必要があります。

- デバイスでリモートウェイクアップを行う必要がある場合は、デバイスに対して[**irp\_完了\_\_待機**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)するように要求します。
- すべての i/o をキャンセルし、デバイスをより低電力状態にする準備をします。
- *PowerState*パラメーターを Enumerator 値 PowerDeviceD2 (WDM; ntddk で定義) に設定して、 [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して、デバイスを WDM スリープ状態にします。 Windows XP では、デバイスにリモートスリープが設定されていない場合でも、ドライバーはデバイスを PowerDeviceD3 に配置しないでください。

Windows XP では、ドライバーは、デバイスを選択的に中断するために、アイドル通知コールバックルーチンに依存している必要があります。 Windows XP で実行されているドライバーが、アイドル状態の通知コールバックルーチンを使用せずにデバイスをより低電力状態にする場合、これにより、USB デバイスツリー内の他のデバイスが中断されるのを防ぐことができます。 詳細については、「USB グローバル中断」を参照してください。

ハブドライバーと[USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)はどちらも、IRQL = パッシブ\_レベルでアイドル通知コールバックルーチンを呼び出します。 これにより、コールバックルーチンは、電源状態変更要求の完了を待機している間、ブロックすることができます。

コールバックルーチンは、システムが**S0**で、デバイスが**D0**にある間だけ呼び出されます。

アイドル状態の要求通知コールバックルーチンには、次の制限が適用されます。

- デバイスドライバーは、アイドル状態の通知コールバックルーチンで、デバイスの電源状態の通知を**D0**から**D2**に開始できますが、その他の電源状態の移行は許可されません。 特に、ドライバーは、コールバックルーチンの実行中に、デバイスを**D0**に変更することはできません。
- デバイスドライバーは、アイドル通知コールバックルーチン内から複数の電源 IRP を要求することはできません。

### <a name="arming-devices-for-wakeup-in-the-idle-notification-callback-routine"></a>アイドル状態の通知コールバックルーチンでウェイクアップ用にデバイスを取り組まする

アイドル状態の通知のコールバックルーチンは、デバイスが IRP を\_しているかどうかを判断し[ **\_待機\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)要求が保留中であるかどうかを確認します。 \_待機\_ウェイク要求が保留中であることを待機している IRP\_がない場合、コールバックルーチンは、デバイスを中断する前に待機\_待機\_待機を\_送信する必要があります。 待機ウェイクメカニズムの詳細については、「[ウェイクアップ機能を持つデバイスのサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)」を参照してください。

## <a name="usb-global-suspend"></a>USB グローバル中断

USB 2.0 仕様では、バス上のすべての USB トラフィック (フレームの開始パケットを含む) を停止することによって、USB ホストコントローラーの背後にあるバス全体の中断としてグローバル中断が定義されています。 まだ中断されていないダウンストリームデバイスは、アップストリームポートでアイドル状態を検出し、それ自体に中断状態を入力します。 Windows は、この方法ではグローバル中断を実装しません。 Windows は、バス上のすべての USB トラフィックを停止する前に、USB ホストコントローラーの背後にある各 USB デバイスを選択的に中断します。

- [Windows 7 でのグローバル中断の条件](#conditions-for-global-suspend-in-windows-7)
- [Windows Vista でのグローバル中断の条件](#conditions-for-global-suspend-in-windows-vista)
- [Windows XP でのグローバル中断の条件](#conditions-for-global-suspend-in-windows-xp)
- [関連トピック](#related-topics)

### <a name="conditions-for-global-suspend-in-windows-7"></a>Windows 7 でのグローバル中断の条件

Windows 7 では、Windows Vista よりも USB ハブを選択的に一時停止することがより積極的になります。 Windows 7 の USB ハブドライバーは、接続されているすべてのデバイスが**D1**、 **D2**、または**D3**デバイスの電源状態にあるすべてのハブを選択的に中断します。 すべての USB ハブが選択的に中断されると、バス全体がグローバル中断に入ります。 Windows 7 の USB ドライバースタックは、デバイスが**D1**、 **D2**、または**D3**の WDM デバイス状態にあるときに、デバイスをアイドル状態として扱います。

### <a name="conditions-for-global-suspend-in-windows-vista"></a>Windows Vista でのグローバル中断の条件

Windows Vista では、Windows XP よりもグローバルな中断を行うための要件はより柔軟です。

特に、デバイスが**D1**、 **D2**、または**D3**の WDM デバイス状態にある場合、USB スタックはデバイスを Windows Vista ではアイドル状態として扱います。

次の図は、Windows Vista で発生する可能性のあるシナリオを示しています。

![windows vista でのグローバル中断を示す図](images/global-suspendlh.png)

この図は、「Windows XP でのグローバル中断の条件」に示されているような状況を示しています。 ただし、この場合、デバイス3はアイドル状態のデバイスとして修飾されます。 すべてのデバイスがアイドル状態であるため、バスドライバーは、保留中のアイドル状態の要求の Irp に関連付けられているアイドル通知コールバックルーチンを呼び出すことができます。 各ドライバーがデバイスを中断すると、バスドライバーは、その処理を安全にすると同時に、USB ホストコントローラーを中断します。

Windows Vista では、グローバル中断が開始される前に、すべての非ハブ USB デバイスが**D1**、 **D2**、または**D3**に存在する必要があります。その時点で、ルートハブを含むすべての usb ハブが中断されます。 これは、セレクティブサスペンドをサポートしていないすべての USB クライアントドライバーが、バスがグローバル中断を開始できないことを意味します。

### <a name="conditions-for-global-suspend-in-windows-xp"></a>Windows XP でのグローバル中断の条件

Windows XP で電力を節約するためには、すべてのデバイスドライバーがアイドル状態の要求 Irp を使用してデバイスを中断することが重要です。 1つのドライバーが Irp\_によってデバイスを中断した場合\_アイドル状態の要求 IRP ではなく、[**電源要求\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)すると、他のデバイスが中断されるのを防ぐことができます。

次の図は、Windows XP で発生する可能性のあるシナリオを示しています。

![windows xp でのグローバル中断を示す図](images/global-suspendxp.png)

この図では、デバイス3は電力状態 D3 であり、アイドル状態の要求 IRP が保留になっていません。 デバイス3は、Windows XP でのグローバル中断を目的として、アイドル状態のデバイスとしては使用できません。これは、その親で保留されているアイドル要求の IRP が存在しないためです。 これにより、バスドライバーは、ツリー内の他のデバイスのドライバーに関連付けられているアイドル要求コールバックルーチンを呼び出すことができなくなります。

## <a name="enabling-selective-suspend"></a>セレクティブサスペンドを有効にする

Microsoft Windows XP のアップグレードバージョンでは、選択的中断は無効になっています。 Windows XP、Windows Vista、およびそれ以降のバージョンの Windows のクリーンインストールに対応しています。

特定のルートハブとその子デバイスに対してセレクティブサスペンドのサポートを有効にするには、**デバイスマネージャー**で、USB ルートハブの **[電源管理]** タブのチェックボックスをオンにします。

また、USB ポートドライバーのソフトウェアキーの下にある**HcDisableSelectiveSuspend**の値を設定して、セレクティブサスペンドを有効または無効にすることもできます。 値1は、選択的中断を無効にします。 値を0にすると、選択的中断が有効になります。

たとえば、Usbport の次の行では、Hydra OHCI コントローラーのセレクティブサスペンドを無効にしています。

```cpp
[OHCI_NOSS.AddReg.NT]
HKR,,"HcDisableSelectiveSuspend",0x00010001,1
```

クライアントドライバーは、アイドル状態の要求を送信する前に、セレクティブサスペンドが有効になっているかどうかを判断することはできません。 デバイスがアイドル状態のときは常にアイドル要求を送信する必要があります。 アイドル状態の要求が失敗した場合、クライアントドライバーはアイドルタイマーをリセットして再試行します。

## <a name="related-topics"></a>関連トピック

[USB 電源管理](usb-power-management.md)  
