---
Description: このトピックでは、ユニバーサルシリアルバス (USB) 3.0 マルチ機能デバイス (複合デバイス) の関数の中断と関数のリモートウェイクアップ機能の概要について説明します。
title: 複合ドライバーで関数の中断を実装する方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 757dcece9f37d26d2d18cb9bbf6df540987684c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844993"
---
# <a name="how-to-implement-function-suspend-in-a-composite-driver"></a>複合ドライバーで関数の中断を実装する方法


このトピックでは、ユニバーサルシリアルバス (USB) 3.0 マルチ機能デバイス (複合デバイス) の関数の中断と関数のリモートウェイクアップ機能の概要について説明します。 このトピックでは、複合デバイスを制御するドライバーでこれらの機能を実装する方法について説明します。 このトピックは、Usbccgp を置き換える複合ドライバーに適用されます。

Universal Serial Bus (USB) 3.0 仕様では、*関数の中断*と呼ばれる新しい機能が定義されています。 この機能を使用すると、複合デバイスの個々の機能が、他の機能とは別に低電力状態に入ることができます。 キーボードの関数とマウスの別の機能を定義する複合デバイスを考えてみましょう。 ユーザーはキーボードの機能を動作状態のままにしますが、一定の時間、マウスを移動しません。 マウスのクライアントドライバーは、関数のアイドル状態を検出し、キーボード関数が動作状態のままであれば、その関数を中断状態に送信できます。

すべての個別の関数が中断状態になると、複合デバイス全体が中断状態に移行します。 ただし、デバイス内のすべての機能の電源状態に関係なく、デバイス全体が中断状態に移行する可能性があります。 特定の関数とデバイス全体が中断状態になった場合、デバイスが中断状態になっている間、およびデバイスの中断エントリと終了プロセスを通じて、関数の中断状態が保持されます。

Usb 2.0 デバイスのリモートウェイクアップ機能 (「 [Usb デバイスのリモートウェイクアップ](remote-wakeup-of-usb-devices.md)」を参照) と同様に、usb 3.0 複合デバイスの個々の機能は、他の機能の電源状態に影響を与えることなく、低電力状態からウェイクアップできます。 この機能は *、関数のリモートウェイクアップ*と呼ばれます。 この機能は、デバイスのファームウェアのリモートウェイクアップビットを設定するプロトコル要求を送信することによって、ホストによって明示的に有効化されます。 このプロセスは *、リモートウェイクアップ用の関数の取り組ま*と呼ばれます。 リモートウェイク関連のビットの詳細については、公式の USB 仕様の図9-6 を参照してください。

関数がリモートウェイクアップ用に設定されている場合、(中断状態のときに) 関数は、物理デバイスでユーザーイベントが発生したときにウェイクアップ*再開通知*を生成するのに十分な電力を保持します。 この再開信号の結果として、クライアントドライバーは、関連付けられている関数の中断状態を終了できます。 複合デバイスのマウス機能の例では、ユーザーがアイドル状態にあるマウスをウィグリングすると、マウス機能によってホストに再開信号が送信されます。 ホストでは、USB ドライバースタックは、ウェイクアップされた機能を検出し、対応する関数のクライアントドライバーに通知を伝達します。 その後、クライアントドライバーは関数をウェイクアップして、動作状態に入ることができます。

クライアントドライバーの場合は、状態を中断するために関数を送信し、関数をウェイクアップする手順は、デバイス全体を中断状態に送信する単一関数のデバイスドライバーに似ています。 これらの手順の概要を次に示します。

1.  関連付けられている関数がアイドル状態であることを検出します。
2.  アイドル状態の i/o 要求パケット (IRP) を送信します。
3.  待機ウェイクアップ i/o 要求パケット (IRP) を送信して、リモートウェイクアップのためにその機能を arm に渡す要求を送信します。
4.  **Dx**の電源 Irp (**D2**または**D3**) を送信して、関数を低電力状態に移行します。

上記の手順の詳細については、「 [Usb 選択的中断](usb-selective-suspend.md)」の「Usb アイドル要求の IRP を送信する」を参照してください。
複合ドライバーは、複合デバイスの各関数用に物理デバイスオブジェクト (PDO) を作成し、クライアントドライバー (関数のデバイススタックの FDO) によって送信された電力要求を処理します。 クライアントドライバーが機能の中断状態を正常に開始して終了するには、複合ドライバーが機能の中断およびリモートウェイクアップ機能をサポートし、受信した電源要求を処理する必要があります。

Windows 8 では、USB 3.0 デバイスの USB ドライバースタックがこれらの機能をサポートしています。 さらに、関数の中断および関数のリモートウェイクアップの実装は、Windows の既定の複合ドライバーである Microsoft 提供の[USB 汎用親ドライバー](usb-common-class-generic-parent-driver.md) (Usbccgp) に追加されています。 カスタム複合ドライバーを作成する場合は、次の手順に従って、関数の中断およびリモートウェイクアップ要求に関連する要求をドライバーで処理する必要があります。

<a name="instructions"></a>手順
------------

### <a href="" id="determine-whether-the-usb-driver-stack-supports-function-suspend"></a>手順 1: USB ドライバースタックが関数の中断をサポートしているかどうかを判断する

複合ドライバーの開始デバイスルーチン ([**IRP\_\_によって起動\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)) で、次の手順を実行します。

1.  [**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))ルーチンを呼び出して、基になる USB ドライバースタックが関数の中断機能をサポートしているかどうかを確認します。 この呼び出しには、前の[**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)ルーチンの呼び出しで取得した有効な USBD ハンドルが必要です。

    [**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))への呼び出しが成功すると、基になる USB ドライバースタックが関数の中断をサポートしているかどうかが判断されます。 この呼び出しは、USB ドライバースタックが関数の中断をサポートしていないか、接続されているデバイスが USB 3.0 マルチ機能デバイスではないことを示すエラーコードを返すことができます。

2.  [**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))の呼び出しで、関数の中断がサポートされていることが示された場合は、基になる USB ドライバースタックに複合デバイスを登録します。 複合デバイスを登録するには、 [ **\_内部\_USB\_登録し、複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_register_composite_device)i/o 制御要求\_登録する必要があります。 この要求の詳細については、「[複合デバイスを登録する方法](register-a-composite-driver.md)」を参照してください。

    登録要求では、[**登録\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_register_composite_device)構造を使用して、複合ドライバーに関する情報を指定します。 **CapabilityFunctionSuspend**が1に設定されていることを確認してください。これは、複合ドライバーが関数の中断をサポートしていることを示します。

USB ドライバースタックが関数の中断をサポートしているかどうかを確認する方法を示すコード例については、「 [**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))」を参照してください。

### <a href="" id="handle-the-idle-irp"></a>手順 2: アイドル状態の IRP を処理する

クライアントドライバーは、アイドル状態の IRP を送信できます (「 [**IOCTL\_内部\_USB\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification))」を参照してください。 要求は、クライアントドライバーが関数のアイドル状態を検出した後に送信されます。 IRP には、クライアントドライバーによって実装されるコールバック完了ルーチン (*アイドルコールバック*と呼ばれます) へのポインターが含まれています。 アイドルコールバック内では、クライアントは、中断状態の関数を送信する直前に、保留中の i/o 転送のキャンセルなどのタスクを実行します。

USB 3.0 デバイスのクライアントドライバーでは、アイドル状態の IRP メカニズムがオプションで  **ことに注意**してください。 ただし、ほとんどのクライアントドライバーは、USB 2.0 と USB 3.0 の両方のデバイスをサポートするように記述されています。 USB 2.0 デバイスをサポートするには、ドライバーがアイドル状態の IRP を送信する必要があります。これは、複合ドライバーが各関数の電源状態を追跡するためにその IRP に依存しているためです。 すべての関数がアイドル状態の場合、複合ドライバーはデバイス全体を中断状態に送信します。

 

クライアントドライバーからアイドル状態の IRP を受け取ると、複合ドライバーはすぐにアイドルコールバックを呼び出して、クライアントドライバーが中断状態になることがクライアントドライバーに通知されるようにクライアントドライバーに通知する必要があります。

### <a href="" id="send-a-request-for-remote-wake-up-notification"></a>手順 3: リモートウェイクアップ通知の要求を送信する

クライアントドライバーは、 [**irp\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) IRP を送信することによって、その機能を arm に渡す要求を送信します。これにより、マイナー機能コードが irp\_\_に設定され、[**待機\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)(待機-ウェイクアップ IRP) になります。 クライアントドライバーは、ユーザーイベントの結果として動作状態を入力する必要がある場合にのみ、この要求を送信します。

複合ドライバーは、待機ウェイク IRP を受信したときに、リモート\_ウェイクアップ\_通知 I/o 制御要求\_、USB ドライバースタックに[ **\_内部\_usb\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_request_remote_wake_notification)を送信する必要があります。 この要求により、スタックが再開シグナルに関する通知を受信したときに、USB ドライバースタックから複合ドライバーに通知されるようになります。 **内部\_USB\_要求\_リモート\_ウェイク\_通知**では、要求[ **\_リモート\_ウェイク\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_request_remote_wake_notification)構造を使用して要求パラメーターを指定します。\_。 複合ドライバーによって指定される必要がある値の1つは、リモートウェイクアップ用に設定されている関数の関数ハンドルです。 前の要求でを処理して、複合デバイスを USB ドライバースタックに登録するために取得した複合ドライバー。 複合ドライバーの登録要求の詳細については、「[複合デバイスを登録する方法](register-a-composite-driver.md)」を参照してください。

要求の IRP では、複合ドライバーは、複合ドライバーによって実装される (リモートウェイクアップ) 完了ルーチンへのポインターを提供します。

次のコード例は、リモートウェイクアップ要求を送信する方法を示しています。

```ManagedCPlusPlus
/*++

Description: 
    This routine sends a IOCTL_INTERNAL_USB_REQUEST_REMOTE_WAKE_NOTIFICATION request
    to the USB driver stack. The IOCTL is completed by the USB driver stack 
    when the function wakes up from sleep.

    Parameters:
    parentFdoExt: The device context associated with the FDO for the
    composite driver.

    functionPdoExt: The device context associated with the PDO (created by 
    the composite driver) for the client driver.
--*/

VOID
SendRequestForRemoteWakeNotification(
    __inout PPARENT_FDO_EXT parentFdoExt,
    __inout PFUNCTION_PDO_EXT functionPdoExt
)

{
    PIRP                                irp;
    REQUEST_REMOTE_WAKE_NOTIFICATION    remoteWake;
    PIO_STACK_LOCATION                  nextStack;
    NTSTATUS                            status;

    // Allocate an IRP
    irp =  IoAllocateIrp(parentFdoExt->topDevObj->StackSize, FALSE); 

    if (irp)
    {
 
        //Initialize the USBDEVICE_REMOTE_WAKE_NOTIFICATION structure
        remoteWake.Version = 0;
        remoteWake.Size = sizeof(REQUEST_REMOTE_WAKE_NOTIFICATION);
        remoteWake.UsbdFunctionHandle = functionPdoExt->functionHandle;
        remoteWake.Interface = functionPdoExt->baseInterfaceNumber;

        nextStack = IoGetNextIrpStackLocation(irp);

        nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;   
        nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_REQUEST_REMOTE_WAKE_NOTIFICATION;

        nextStack->Parameters.Others.Argument1 = &remoteWake;
        
        // Caller's completion routine will free the IRP when it completes.
 
        SetCompletionRoutine(functionPdoExt->debugLog,
                             parentFdoExt->fdo,
                             irp, 
                             CompletionRemoteWakeNotication, 
                             (PVOID)functionPdoExt, 
                             TRUE, TRUE, TRUE);

        // Pass the IRP
        IoCallDriver(parentFdoExt->topDevObj, irp);

    }

    return;
}
```

[**内部\_usb\_要求\_リモート\_wake\_通知要求の IOCTL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_request_remote_wake_notification)は、再開シグナルに関する通知を受信したときに、ウェイクアッププロセス中に usb ドライバースタックによって完了します。 その間、USB ドライバースタックによって、リモートウェイクアップの完了ルーチンも呼び出されます。

複合ドライバーは、待機-ウェイク IRP を保留したままにして、後で処理するためにキューに置く必要があります。 複合ドライバーは、ドライバーのリモートウェイクアップ完了ルーチンが USB ドライバースタックによって起動されたときに、その IRP を完了する必要があります。

### <a href="" id="send-a-request-to-arm-the-function-for-remote-wake-up"></a>手順 4: リモートウェイクアップ用に関数を Arm に渡す要求を送信する

関数を低電力状態に送信するために、クライアントドライバーは、Windows Driver Model (WDM) デバイスの電源状態を**D2**または**D3**に変更する要求を使用して\_電源 irp を\_設定して、 [**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)を送信します。 通常、リモートウェイクアップを要求するためにドライバーが前に待機ウェイク IRP を送信した場合、クライアントドライバーは**D2** irp を送信します。 それ以外の場合、クライアントドライバーは**D3** IRP を送信します。

**D2** irp を受信すると、複合ドライバーは、最初にクライアントドライバーによって送信された前の要求から待機ウェイク IRP が保留されているかどうかを判断する必要があります。 その IRP が保留中の場合は、複合ドライバーがリモートウェイクアップ用に関数を arm にする必要があります。 これを行うには、複合ドライバーは、デバイスが再開信号を送信できるようにするために、関数の最初のインターフェイスに\_機能コントロール要求を送信する必要があります。 コントロール要求を送信するには、 [**USBD\_Urを検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)ルーチンを呼び出し、 [**UsbBuildFeatureRequest**](https://docs.microsoft.com/previous-versions/ff538932(v=vs.85))マクロを呼び出して、SET\_機能要求の**urb**をフォーマットすることによって、 [**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体を割り当てます。 この呼び出しでは、URB\_関数を指定し\_\_機能\_を操作コードとして\_インターフェイスに設定します。また、USB\_機能\_機能セレクターとして中断\_ます。 *Index*パラメーターで、最上位バイトの**ビット 1**を設定します。 この値は、転送のセットアップパケットの**wIndex**フィールドにコピーされます。

次の例は、SET\_機能コントロール要求を送信する方法を示しています。

```ManagedCPlusPlus
/*++

Routine Description:

Sends a SET_FEATURE for REMOTE_WAKEUP to the device using a standard control request.

Parameters:
parentFdoExt: The device context associated with the FDO for the
composite driver.

functionPdoExt: The device context associated with the PDO (created by 
the composite driver) for the client driver.

Returns:

NTSTATUS code.

--*/
VOID
    NTSTATUS SendSetFeatureControlRequestToSuspend(
    __inout PPARENT_FDO_EXT parentFdoExt,
    __inout PFUNCTION_PDO_EXT functionPdoExt,
    )

{
    PURB                            urb
    PIRP                            irp;
    PIO_STACK_LOCATION              nextStack;
    NTSTATUS                        status;

    status = USBD_UrbAllocate(parentFdoExt->usbdHandle, &urb);

    if (!NT_SUCCESS(status))
    {    
        //USBD_UrbAllocate failed.
        goto Exit;
    }

    //Format the URB structure.
    UsbBuildFeatureRequest (
        urb,
        URB_FUNCTION_SET_FEATURE_TO_INTERFACE, // Operation code
        USB_FEATURE_FUNCTION_SUSPEND,          // feature selector
        functionPdoExt->firstInterface,           // first interface of the function
        NULL);

    irp =  IoAllocateIrp(parentFdoExt->topDevObj->StackSize, FALSE); 

    if (!irp)
    {
        // IoAllocateIrp failed.
        status = STATUS_INSUFFICIENT_RESOURCES;

        goto Exit;
    }

    nextStack = IoGetNextIrpStackLocation(irp);

    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;  

    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_URB;  

    //  Attach the URB to the IRP.
    USBD_AssignUrbToIoStackLocation(nextStack, (PURB)urb);

    // Caller's completion routine will free the IRP when it completes.
    SetCompletionRoutine(functionPdoExt->debugLog,
        parentFdoExt->fdo,
        irp, 
        CompletionForSuspendControlRequest, 
        (PVOID)functionPdoExt, 
        TRUE, TRUE, TRUE);


    // Pass the IRP
    IoCallDriver(parentFdoExt->topDevObj, irp);


Exit:
    if (urb)
    {
        USBD_UrbFree( parentFdoExt->usbdHandle, urb); 
    }

    return status;

}
```

その後、複合ドライバーは**D2** IRP を USB ドライバースタックに送信します。 他のすべての関数が中断状態にある場合、USB ドライバースタックはコントローラー上の特定のポートレジスタを操作してポートを中断します。

<a name="remarks"></a>注釈
-------

マウスの機能の例では、リモートウェイクアップ機能が有効になっているため (手順4を参照)、マウスの機能により、ユーザーがマウスを操作したときに、ネットワーク上でホストコントローラーへの再開信号が生成されます。 次に、コントローラーは、ウェイクアップした関数に関する情報を含む通知パケットを送信することによって、USB ドライバースタックに通知します。 関数のウェイクアップ通知の詳細については、「USB 3.0 仕様」の図8-17 を参照してください。

USB ドライバースタックは、通知パケットを受信すると、保留中の[**IOCTL\_内部\_usb\_要求\_リモート\_ウェイク\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_request_remote_wake_notification)要求 (手順3を参照) を完了し、(リモートウェイクアップ) を呼び出します。要求で指定され、複合ドライバーによって実装された完了コールバックルーチン。 通知が複合ドライバーに到達すると、クライアントドライバーが以前に送信した待機ウェイク IRP を完了することによって、関数が動作状態に入ったことを、対応するクライアントドライバーに通知します。

(リモートウェイクアップ) 完了ルーチンでは、保留中の待機ウェイク IRP を完了するために、複合ドライバーが作業項目をキューに入れます。 USB 3.0 デバイスの場合、複合ドライバーは再開信号を送信し、他の機能を中断状態のままにする関数だけを起動します。 作業項目をキューに置いて、USB 2.0 デバイスの関数ドライバーの既存の実装との互換性を確保します。 作業項目のキューの詳細については、「 [**Ioqueueworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)」を参照してください。

ワーカースレッドは、待機ウェイク IRP を完了し、クライアントドライバーの完了ルーチンを呼び出します。 次に、完了ルーチンは**D0** IRP を送信して、関数を動作状態にします。 待機ウェイク IRP を完了する前に、複合ドライバーは[**Posetsystemwake**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemwake)を呼び出して、待機ウェイク irp を、中断状態からシステムをウェイクアップするためのものとしてマークする必要があります。 電源マネージャーは、システムを起動したデバイスに関する情報を含む Windows イベントトレーシング (ETW) イベント (グローバルシステムチャネルに表示される) をログに記録します。

## <a name="related-topics"></a>関連トピック
[USB 電源管理](usb-power-management.md)  
[USB セレクティブサスペンド](usb-selective-suspend.md)  



