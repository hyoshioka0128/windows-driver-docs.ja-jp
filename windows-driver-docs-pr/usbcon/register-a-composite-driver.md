---
Description: 方法、複合のドライバーと呼ばれる USB 多機能デバイスを登録し、基になる USB ドライバー スタックと複合デバイスの登録を解除します。
title: 複合デバイスを登録する方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0351a0869e3cb6d9ecc2b869f69929b735df4339
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368800"
---
# <a name="how-to-register-a-composite-device"></a>複合デバイスを登録する方法


このトピックでは、複合のドライバーと呼ばれる、USB 多機能デバイスのドライバーを登録および基になる USB ドライバー スタックと複合デバイスの登録を解除する方法について説明します。 Microsoft 提供のドライバーで、Usbccgp.sys は、Windows によって読み込まれる既定の複合ドライバーです。 このトピックの手順では、カスタム Windows Driver Model WDM ベース複合ドライバーで、Usbccgp.sys を置換するには適用されます。

ユニバーサル シリアル バス (USB) デバイスでは、同時にアクティブになっている複数の関数を提供できます。 このような多機能デバイスとも呼ばれます*複合デバイス*します。 たとえば、キーボード機能のための関数とマウスの別の関数複合デバイスを定義します。 デバイスの機能は、複合、ドライバーによって列挙されます。 複合のドライバーでは、モノリシック モデル自体これらの機能を管理したり、各関数の物理デバイス オブジェクト (Pdo) を作成することができます。 これらの個々 の Pdo は、それぞれのそれぞれの USB 機能ドライバー、キーボード ドライバーおよびマウス ドライバーによって管理されます。

USB 3.0 の仕様の定義、*関数の中断とリモート ウェイク アップ機能*個々 の関数を入力し、その他の関数または全体のデバイスの電源状態の影響を与えずに低電力状態を終了できるようにします。 機能の詳細については、次を参照してください。[複合ドライバーでは実装関数を中断する方法](how-to--implement-remote-and-function-wake-support.md)します。

機能を使用するには、複合ドライバーは、基になる USB ドライバー スタックと、デバイスを登録する必要があります。 複合のドライバーを基になるスタック USBD のバージョンをサポートしていることを確認して行う必要があります機能は、USB 3.0 デバイスに適用される、ため\_インターフェイス\_バージョン\_602 します。 登録要求は、複合ドライバー: から

-   基になる USB ドライバー スタックにドライバーがリモート ウェイク アップの関数を arm に要求を送信する役割があることを通知します。 リモートのウェイク アップ要求は、デバイスに必要なプロトコルの要求を送信する USB ドライバー スタックによって処理されます。
-   USB ドライバー スタックによって割り当てられた関数ハンドル (関数ごとに 1 つ) の一覧を取得します。 複合ドライバーを使用できますドライバーの機能ハンドル要求ハンドルに関連付けられている関数のリモート ウェイク アップ。

複合のドライバーがドライバーの AddDevice またはデバイスの起動のルーチン処理するために登録要求を送信する通常[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device). 複合のドライバーがデバイスの停止など、ドライバーのアンロードのルーチンで登録に割り当てられているリソースを解放するそのため、([**IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)) または装置を削除するルーチン ([**IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device))。

### <a name="prerequisites"></a>前提条件

登録要求を送信する前にことを確認します。

-   関数の数が、デバイスであります。 数ができる、構成の取得要求によって取得された記述子を派生します。
-   以前の呼び出しで USBD ハンドルを取得した[ **USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_createhandle)します。
-   基になる USB ドライバー スタックは、USB 3.0 デバイスをサポートします。 これを行うには、呼び出す[ **USBD\_IsInterfaceVersionSupported** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_isinterfaceversionsupported) USBD を渡すと\_インターフェイス\_バージョン\_602 バージョンを確認するとします。

コード例では、次を参照してください。[複合ドライバーでは実装関数を中断する方法](how-to--implement-remote-and-function-wake-support.md)します。
手順
------------

### <a name="register-a-composite-device"></a>複合デバイスを登録します。

次の手順では、複合のドライバーを USB ドライバー スタックに関連付けるための登録要求を送信およびビルドを行う方法について説明します。

1.  割り当て、 [**複合\_デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/ns-usbdlib-_composite_device_capabilities)構造体を呼び出すことによって初期化、 [**複合\_デバイス\_機能\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-composite_device_capabilities_init)マクロ。
2.  設定、 **CapabilityFunctionSuspend**のメンバー [**複合\_デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/ns-usbdlib-_composite_device_capabilities)を 1 にします。
3.  割り当て、 [**登録\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/ns-usbdlib-_register_composite_device)構造体し、構造体を呼び出すことによって初期化、 [ **USBD\_BuildRegisterCompositeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_buildregistercompositedevice)ルーチン。 呼び出しで指定、初期化された USBD ハンドル[**複合\_デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/ns-usbdlib-_composite_device_capabilities)構造、および関数の数。
4.  I/O 要求パケット (IRP) を呼び出すことによって割り当てる[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp) IRP の最初のスタックの場所へのポインターを取得し、([**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)) を呼び出して[ **IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)します。
5.  関数のハンドルの配列を保持するために十分な大きさであるバッファーのメモリを割り当てる (USBD\_関数\_処理)。 配列内の要素の数は、Pdo の数である必要があります。
6.  次のメンバーを設定して、要求を構築、 [ **IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location):
    -   要求の種類を設定して指定**Parameters.DeviceIoControl.IoControlCode**に[ **IOCTL\_内部\_USB\_登録\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_register_composite_device)します。
    -   入力パラメーターを設定して指定**Parameters.Others.Argument1** 、初期化済みのアドレスに[**登録\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/ns-usbdlib-_register_composite_device)構造体。
    -   出力パラメーターを設定して指定**AssociatedIrp.SystemBuffer**手順 5. で割り当てられたバッファーにします。

7.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRP をスタックの次の場所に渡すことによって、要求を送信します。

完了したら、USB ドライバー スタックによって返される関数のハンドルの配列を検査します。 将来使用するため、ドライバーのデバイス コンテキストで配列を格納することができます。

次のコード例では、ビルドし、登録要求を送信する方法を示します。 例には、複合のドライバーは、以前に取得した関数の数を格納します。 ドライバーのデバイス コンテキストでは、USBD の処理を前提としています。

```ManagedCPlusPlus
VOID  RegisterCompositeDriver(PPARENT_FDO_EXT parentFdoExt)  
{  
    PIRP                            irp;  
    REGISTER_COMPOSITE_DRIVER       registerInfo;  
    COMPOSITE_DRIVER_CAPABILITIES   capabilities;  
    NTSTATUS                        status;  
    PVOID                           buffer;  
    ULONG                           bufSize;  
    PIO_STACK_LOCATION              nextSp;  

    buffer = NULL;  

    COMPOSITE_DRIVER_CAPABILITIES_INIT(&capabilities);  
    capabilities.CapabilityFunctionSuspend = 1;  

    USBD_BuildRegisterCompositeDriver(parentFdoExt->usbdHandle,  
        capabilities,  
        parentFdoExt->numFunctions,  
        &registerInfo);  

    irp = IoAllocateIrp(parentFdoExt->topDevObj->StackSize, FALSE);  

    if (irp == NULL) 
    {  
        //IoAllocateIrp failed.
        status = STATUS_INSUFFICIENT_RESOURCES;  
        goto ExitRegisterCompositeDriver;    
    }  

    nextSp = IoGetNextIrpStackLocation(irp);  

    bufSize = parentFdoExt->numFunctions * sizeof(USBD_FUNCTION_HANDLE);  

    buffer = ExAllocatePoolWithTag (NonPagedPool, bufSize, POOL_TAG);  

    if (buffer == NULL) 
    {  
        // Memory alloc for function-handles failed.
        status = STATUS_INSUFFICIENT_RESOURCES;  
        goto ExitRegisterCompositeDriver;    
    }  

    nextSp->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;     
    nextSp->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_REGISTER_COMPOSITE_DRIVER;  

    //Set the input buffer in Argument1      
    nextSp->Parameters.Others.Argument1 = &registerInfo;  

    //Set the output buffer in SystemBuffer field for USBD_FUNCTION_HANDLE.      
    irp->AssociatedIrp.SystemBuffer = buffer;  

    // Pass the IRP down to the next device object in the stack. Not shown.
    status = CallNextDriverSync(parentFdoExt, irp, FALSE);  

    if (!NT_SUCCESS(status))
    {  
        //Failed to register the composite driver.
        goto ExitRegisterCompositeDriver;    
    }  

    parentFdoExt->compositeDriverRegistered = TRUE;  

    parentFdoExt->functionHandleArray = (PUSBD_FUNCTION_HANDLE) buffer;  

End:  
    if (!NT_SUCCESS(status)) 
    {  
        if (buffer != NULL) 
        {  
            ExFreePoolWithTag (buffer, POOL_TAG);  
            buffer = NULL;  
        }  
    }  

    if (irp != NULL) 
    {  
        IoFreeIrp(irp);  
        irp = NULL;  
    }  

    return;  
}
```

### <a name="unregister-the-composite-device"></a>複合デバイスの登録を解除します。

1.  呼び出すことによって、IRP を割り当てる[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp) IRP の最初のスタックの場所へのポインターを取得し、([**IO\_スタック\_場所** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)) を呼び出して[ **IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)します。
2.  設定して、要求を構築、 **Parameters.DeviceIoControl.IoControlCode**のメンバー [ **IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location) に[ **IOCTL\_内部\_USB\_登録解除\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_unregister_composite_device)します。
3.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRP をスタックの次の場所に渡すことによって、要求を送信します。

[ **IOCTL\_内部\_USB\_登録解除\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_unregister_composite_device)で複合ドライバーによって要求が 1 回送信します装置を削除するルーチンのコンテキスト。 要求では、USB ドライバー スタックと複合ドライバーとその列挙型の関数間の関連付けを削除します。 要求は、その関連付けを維持するために作成されたすべてのリソースと前回の登録要求で返されたすべての機能ハンドルによってクリーンアップされます。

次のコード例では、ビルドして、複合デバイスの登録を解除する要求を送信する方法を示します。 例では、複合ドライバーが以前登録されている登録要求をこのトピックで前述したよう想定しています。

```ManagedCPlusPlus
VOID  UnregisterCompositeDriver(  
    PPARENT_FDO_EXT parentFdoExt )  
{  
    PIRP                irp;  
    PIO_STACK_LOCATION  nextSp;  
    NTSTATUS            status;  

    PAGED_CODE();  

    irp = IoAllocateIrp(parentFdoExt->topDevObj->StackSize, FALSE);  

    if (irp == NULL) 
    {  
        //IoAllocateIrp failed.
        status = STATUS_INSUFFICIENT_RESOURCES;  
        return;  
    }  

    nextSp = IoGetNextIrpStackLocation(irp);  

    nextSp->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;     
    nextSp->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_UNREGISTER_COMPOSITE_DRIVER;  

    // Pass the IRP down to the next device object in the stack. Not shown.
    status = CallNextDriverSync(parentFdoExt, irp, FALSE);  

    if (NT_SUCCESS(status)) 
    {  
        parentFdoExt->compositeDriverRegistered = FALSE;      
    }  

    IoFreeIrp(irp);  

    return;  
}
```

## <a name="related-topics"></a>関連トピック
[**IOCTL\_内部\_USB\_登録\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_register_composite_device)  
[**IOCTL\_内部\_USB\_登録解除\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_unregister_composite_device)  



