---
Description: このトピックでは、関数の概要が中断し、関数リモート ウェイク アップ機能ユニバーサル シリアル バス (USB) の 3.0 の多機能デバイス (複合デバイス) を提供します。
title: 複合のドライバーで中断する関数を実装する方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41de7e83354c04c4ad8cacb874f5a83edf5a4595
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349118"
---
# <a name="how-to-implement-function-suspend-in-a-composite-driver"></a>複合のドライバーで中断する関数を実装する方法


このトピックでは、関数の概要が中断し、関数リモート ウェイク アップ機能ユニバーサル シリアル バス (USB) の 3.0 の多機能デバイス (複合デバイス) を提供します。 このトピックでは、ドライバーでは複合デバイスを制御するこれらの機能を実装する方法について説明します。 置換で、Usbccgp.sys 複合のドライバーをトピックが適用されます。

ユニバーサル シリアル バス (USB) 3.0 の仕様と呼ばれる新しい機能を定義する*関数中断*します。 機能は、その他の関数とは無関係に、低電力状態に複合デバイスの個々 の関数を使用できます。 関数のキーボードとマウスの別の関数を定義する複合デバイスを検討してください。 ユーザーが作業の状態でキーボードの機能のままで一定期間、マウスを移動しません。 マウスのクライアント ドライバーは、関数のアイドル状態を検出し、キーボードの機能が稼働状態のままの状態を中断する関数を送信できます。

複合デバイス全体の遷移には、個々 の関数はすべて中断状態と状態を中断します。 ただし、デバイス全体が中断デバイス内の任意の関数の電源の状態に関係なく状態に移行できます。 特定の関数およびデバイス全体には、中断状態が入力と、デバイスが中断状態では、デバイスの保留の開始と終了のプロセス全体を通じて、関数の中断状態が保持されます。

USB 2.0 デバイスをリモート ウェイク アップ機能に似ています (を参照してください[USB デバイスのリモート ウェイク アップ](remote-wakeup-of-usb-devices.md))、USB 3.0 複合デバイスで個々 の関数をウェイク アップできる低電力状態から他の関数の電源の状態に影響を与えずにします。 この機能は呼*リモート ウェイク アップ機能*します。 機能は、デバイスのファームウェアのリモート ウェイク アップのビットを設定するプロトコル要求を送信することによって、ホストによって明示的に有効です。 このプロセスが呼び出されます*リモート ウェイク アップの関数を取り組ま*します。 リモート ウェイクのビットについては、公式の USB 仕様の図 9-6 を参照してください。

リモート ウェイク アップ、関数の関数をされている場合 (ときに中断状態) はウェイク アップを生成するための十分な電力が保持されます*信号を再開*ユーザー イベントが物理デバイスで発生します。 終了が関連付けられている関数の状態を中断し、その再開シグナルの結果として、クライアント ドライバーことができます。 マウス関数複合デバイスの例では、ユーザーはアイドル状態でマウスの形跡ときにマウス関数再開にシグナルを送りますホスト。 ホストでは、USB ドライバー スタックは、関数が復帰を対応する関数のクライアント ドライバーに通知を反映させるを検出します。 クライアント ドライバーでは、ウェイク アップ関数、および、作業の状態を入力できます。

クライアント ドライバーの場合は、状態とウェイク アップする関数は、中断する関数を送信するための手順は、中断状態にデバイス全体を送信する単一関数のデバイス ドライバーに似ています。 次の手順では、これらの手順をまとめたものです。

1.  アイドル状態にある、関連付けられた関数を検出します。
2.  アイドル状態の I/O 要求パケット (IRP) を送信します。
3.  待機ウェイク I/O 要求パケット (IRP) を送信することによってその関数のリモート ウェイク アップを arm に要求を送信します。
4.  省電力状態に関数を送信することによって移行**Dx** Irp の電源 (**D2**または**D3**)。

上記の手順の詳細についてを参照してください"の送信、USB アイドル要求 IRP" [USB セレクティブ サスペンド](usb-selective-suspend.md)します。
複合のドライバーでは、クライアント ドライバー (関数デバイス スタックの FDO) によって送信された複合のデバイスとハンドル power の要求で、物理デバイス オブジェクト (PDO) の各関数を作成します。 クライアント ドライバーを正常に入力し、終了するために、その関数の状態を中断、複合ドライバーは、関数をサポートする必要がありますを中断し、リモートのウェイク アップ機能、およびプロセス受信の電源を要求します。

Windows 8 では、USB 3.0 デバイスの USB ドライバー スタックは、これらの機能をサポートします。 さらに、関数を中断し、Microsoft が提供する関数のリモート ウェイク アップの実装が追加された[一般的な親の USB ドライバー](usb-common-class-generic-parent-driver.md) (Usbccgp.sys)、これは、Windows の既定の複合ドライバー。 カスタム複合ドライバーを作成する場合、ドライバーが関数に関連する要求を処理する必要がありますを中断し、次の手順に従って、リモート ウェイク アップを要求します。

<a name="instructions"></a>手順
------------

### <a href="" id="determine-whether-the-usb-driver-stack-supports-function-suspend"></a>手順 1:USB ドライバー スタックのサポート関数が中断するかどうかを判断します。

デバイスの起動のルーチンで ([**IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749))、複合のドライバーの次の手順を実行します。

1.  呼び出す、 [ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)基になる USB ドライバー スタックは、関数をサポートするかどうかを判断するルーチンが機能を中断します。 呼び出しは、以前の呼び出しで取得した有効な USBD の処理が必要です、 [ **USBD\_CreateHandle** ](https://msdn.microsoft.com/library/windows/hardware/hh406241)ルーチン。

    呼び出しは成功[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)基になる USB ドライバー スタックのサポート関数が中断するかどうかを決定します。 USB ドライバー スタックでは、関数はサポートされていないことを示すエラー コードが中断または接続しているデバイスが USB 3.0 多機能デバイスではない、呼び出しを返すことができます。

2.  場合、 [ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)呼び出し関数が中断することは、基になる USB ドライバー スタックに複合デバイスを登録します。 複合デバイスを登録するには送信する必要があります、 [ **IOCTL\_内部\_USB\_登録\_複合\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/hh450854) I/Oコントロールの要求。 この要求の詳細については、次を参照してください。[複合デバイスを登録する方法](register-a-composite-driver.md)します。

    登録要求を使用して、 [**登録\_複合\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/hh450898)複合ドライバーに関する情報を指定する構造体。 設定することを確認**CapabilityFunctionSuspend**複合ドライバーが関数をサポートしていることを示すためには 1 を中断します。

USB ドライバー スタックが関数をサポートするかどうかを確認する方法を示すコード例については、中断を参照してください[ **USBD\_QueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh406230)します。

### <a href="" id="handle-the-idle-irp"></a>手順 2:アイドル状態の IRP を処理します。

クライアント ドライバーがアイドル状態の IRP を送信できます (を参照してください[ **IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270))。 クライアント ドライバーが関数のアイドル状態を検出した後、要求が送信されます。 IRP にはコールバックの完了のルーチンへのポインターが含まれています (と呼ばれる*アイドル コールバック*) クライアント ドライバーによって実装されます。 アイドル状態のコールバックでは、クライアントは、状態を中断する関数を送信する前に保留中の I/O 転送では、キャンセルなどのタスクを実行します。

**注**  アイドル状態の IRP メカニズムは USB 3.0 デバイスのクライアント ドライバーの省略可能です。 ただし、ほとんどのクライアント ドライバーは、USB 2.0 と USB 3.0 の両方のデバイスをサポートするために書き込まれます。 USB 2.0 デバイスをサポートするには、複合ドライバーは、各関数の電源の状態を追跡するためにその IRP に依存するため、ドライバーがアイドル状態の IRP を送信する必要があります。 すべての関数がアイドル状態の場合は、複合、ドライバーは中断状態にデバイス全体を送信します。

 

クライアント ドライバーからアイドル状態の IRP を受信すると、複合ドライバーはすぐにクライアント ドライバーが中断状態に関数を送信することがあります、クライアント ドライバーに通知するアイドル状態のコールバックを呼び出す必要があります。

### <a href="" id="send-a-request-for-remote-wake-up-notification"></a>手順 3:リモート ウェイク アップの通知の要求を送信します。

クライアント ドライバーは、関数をリモート ウェイク アップを送信することで arm に要求を送信できる、 [ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)マイナー関数コードで IRP に設定[**IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766) (待機ウェイク IRP)。 クライアント ドライバーは、ドライバーがユーザー イベントの結果として動作する状態を入力する場合にのみ、この要求を送信します。

待機ウェイク IRP を受信すると、複合のドライバーを送信する必要があります、 [ **IOCTL\_内部\_USB\_要求\_リモート\_WAKE\_通知** ](https://msdn.microsoft.com/library/windows/hardware/hh450856) USB ドライバー スタックに I/O 制御要求。 要求には、スタックが再開信号に関する通知を受信すると、複合ドライバーに通知する USB ドライバー スタックができます。 **IOCTL\_内部\_USB\_要求\_リモート\_WAKE\_通知**を使用して、 [**要求\_リモート\_WAKE\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh406227)要求パラメーターを指定する構造体。 複合のドライバーを指定する必要がある値の 1 つは、リモート ウェイク アップされている関数の関数のハンドルです。 複合のドライバーでは、USB ドライバー スタックに複合デバイスを登録する前の要求では、そのハンドルを取得します。 複合のドライバーの登録要求の詳細については、次を参照してください。[複合デバイスを登録する方法](register-a-composite-driver.md)します。

複合のドライバーが、(リモート ウェイク アップ) へのポインターを提供する要求の IRP、完了のルーチンは、複合、ドライバーによって実装されます。

次のコード例では、リモート ウェイク アップ要求を送信する方法を示します。

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

[ **IOCTL\_内部\_USB\_要求\_リモート\_WAKE\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh450856)によって要求が完了しました再開の信号に関する通知を受信すると、ウェイク アップ プロセス中に USB ドライバー スタック。 この期間中、USB ドライバー スタックは、リモートのウェイク アップ完了ルーチンを呼び出します。

複合ドライバーは、保留中の待機ウェイク IRP を保持し、後の処理キューにする必要があります。 複合のドライバーは、ドライバーのリモートのウェイク アップ完了ルーチンを取得、USB ドライバー スタックによって呼び出されたときにその IRP を完了する必要があります。

### <a href="" id="send-a-request-to-arm-the-function-for-remote-wake-up"></a>手順 4:リモート ウェイク アップの関数を Arm に要求を送信します。

クライアント ドライバーを送信する関数を低電力状態を送信する、 [ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744) IRP を Windows Driver Model (を変更する要求WDM) デバイスの電源状態を**D2**または**D3**します。 通常、クライアント ドライバーの送信**D2** IRP がドライバーにリモート ウェイク アップを要求するには、前の待機ウェイク IRP が送信される場合。 それ以外の場合、クライアント ドライバーの送信**D3** IRP します。

受信すると、 **D2** IRP、複合ドライバーする必要がありますまず決定待機ウェイク IRP が保留中かどうか、クライアント ドライバーによって送信される前の要求から。 その IRP が保留中の場合は、複合、ドライバーは、リモート ウェイク アップの関数を arm する必要があります。 これを行うには、複合のドライバーがセットを送信する必要がある\_関数の最初のインターフェイスに再開信号を送信するデバイスを有効にする機能の制御を要求します。 コントロールの要求を送信するには、割り当て、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造を呼び出すことによって、 [ **USBD\_UrbAllocate** ](https://msdn.microsoft.com/library/windows/hardware/hh406250)ルーチンを呼び出します[ **UsbBuildFeatureRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538932)マクロを書式設定、 **URB**一連の\_機能要求。 呼び出しで指定 URB\_関数\_設定\_機能\_TO\_操作コードと、USB インターフェイス\_機能\_関数\_として中断、機能のセレクター。 *インデックス*パラメーター設定**ビット 1**の最上位バイト。 値をコピーすること、 **wIndex**フィールドに、転送のパケットをセットアップします。

次の例は、セットを送信する方法を示しています。\_機能コントロール要求。

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

複合のドライバーを送信し、 **D2** IRP USB ドライバー スタックにします。 その他のすべての関数がある場合は、中断状態、USB ドライバー スタックは、コント ローラー上の特定のポート レジスタを操作することで、ポートを中断します。

<a name="remarks"></a>コメント
-------

マウス関数の例で、リモートのウェイク アップ機能が有効になっているため、(手順 4 を参照)、マウス関数が、ユーザーがマウスを形跡ときに、ホスト コント ローラーにアップ ストリーム ネットワーク上で再開シグナルを生成します。 コント ローラーを関数に関する情報を含む通知パケットを送信することによって、USB ドライバー スタックを通知します。 関数のスリープ解除通知については、USB 3.0 仕様で図 8-17 を参照してください。

USB ドライバー スタックの完了通知パケットを受信すると、保留中[ **IOCTL\_内部\_USB\_要求\_リモート\_WAKE\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh450856)要求 (手順 3 を参照してください)、(リモート ウェイク アップ) を呼び出すと、要求で指定され、複合ドライバによって実装された完了コールバック ルーチン。 通知には、複合ドライバーに達するに通知クライアントに対応するドライバー関数がクライアント ドライバーが既に送信した待機ウェイク IRP の完了を稼働状態になったことです。

(リモート ウェイク アップ) が完了するまで、日常的な複合ドライバーは IRP が保留中の待機スリープ解除を完了する作業項目をキューする必要があります。 USB 3.0 デバイスの場合は、複合ドライバー スリープ状態の解除を再開信号を送信し、他の関数のまま関数のみは、状態を中断します。 USB 2.0 デバイスのドライバーの関数の既存の実装との互換性を確保する作業項目のキューします。 作業項目のキューについては、次を参照してください。 [ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)します。

ワーカー スレッドは待機ウェイク IRP が完了し、クライアント ドライバーの完了ルーチンを呼び出します。 完了ルーチンを送信し、 **D0** IRP を動作中の関数を入力します。 待機ウェイク IRP を完了する前に、複合のドライバーを呼び出す必要があります[ **PoSetSystemWake** ](https://msdn.microsoft.com/library/windows/hardware/ff559770)からシステムをスリープ解除に使用されたものとして IRP が状態を中断する待機ウェイクをマークします。 電源マネージャーは、システムをデバイスに関する情報が含まれる Event Tracing for Windows (ETW) イベント (グローバル システム チャネルで表示できる) を記録します。

## <a name="related-topics"></a>関連トピック
[USB 電源管理](usb-power-management.md)  
[USB のセレクティブ サスペンドします。](usb-selective-suspend.md)  



