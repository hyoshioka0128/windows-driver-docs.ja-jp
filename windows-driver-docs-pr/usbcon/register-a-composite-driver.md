---
Description: 複合ドライバーと呼ばれる USB マルチ機能デバイスが、基になる USB ドライバースタックで複合デバイスを登録および登録解除する方法を説明します。
title: 複合デバイスを登録する方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9394af1e736b767d9cacb9ac16be5ee3588eb03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824198"
---
# <a name="how-to-register-a-composite-device"></a>複合デバイスを登録する方法


このトピックでは、複合ドライバーと呼ばれる USB マルチ機能デバイスのドライバーが、基になる USB ドライバースタックを使用して複合デバイスを登録および登録解除する方法について説明します。 Microsoft 提供のドライバーである Usbccgp は、Windows によって読み込まれる既定の複合ドライバーです。 このトピックの手順は、Usbccgp を置き換えるカスタム Windows Driver Model (WDM) ベースの複合ドライバーに適用されます。

ユニバーサルシリアルバス (USB) デバイスは、同時にアクティブになっている複数の機能を提供できます。 このようなマルチ関数デバイスは、*複合デバイス*とも呼ばれます。 たとえば、複合デバイスでは、キーボード機能用の関数と、マウスの別の機能を定義できます。 デバイスの機能は、複合ドライバーによって列挙されます。 複合ドライバーは、これらの関数自体をモノリシックモデルで管理したり、各関数に対して物理デバイスオブジェクト (PDOs) を作成したりすることができます。 これらの個々の PDOs は、それぞれの USB 機能ドライバー、キーボードドライバー、およびマウスドライバーによって管理されます。

USB 3.0 仕様では、*関数の中断機能とリモートウェイクアップ機能*を定義しています。この機能を使用すると、他の機能やデバイス全体の電源状態に影響を与えずに、個々の機能で低電力状態を入力および終了できます。 この機能の詳細については、「[複合ドライバーで関数の中断を実装する方法](how-to--implement-remote-and-function-wake-support.md)」を参照してください。

この機能を使用するには、複合ドライバーが、基になる USB ドライバースタックにデバイスを登録する必要があります。 この機能は USB 3.0 デバイスに適用されるため、複合ドライバーは、基になるスタックがバージョン USBD\_インターフェイス\_バージョン\_602 をサポートしていることを確認する必要があります。 登録要求では、複合ドライバーは次のようになります。

-   基になる USB ドライバースタックに、ドライバーがリモートウェイクアップ用の機能を arm に送信するように要求していることを通知します。 リモートウェイクアップ要求は、USB ドライバースタックによって処理されます。このスタックは、必要なプロトコル要求をデバイスに送信します。
-   USB ドライバースタックによって割り当てられた関数ハンドルのリスト (関数ごとに1つ) を取得します。 その後、複合ドライバーは、そのハンドルに関連付けられている関数のリモートウェイクアップを要求するドライバーの関数ハンドルを使用できます。

通常、複合ドライバーは、ドライバーの AddDevice または開始デバイスルーチンに登録要求を送信して、 [ **\_デバイスの起動\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を処理します。 その結果、複合ドライバーは、ドライバーのアンロードルーチンで登録に割り当てられているリソースを解放します。たとえば、停止デバイス ([**irp\_、\_デバイスの停止\_停止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device))、またはデバイスを削除するルーチン (irp\_になります。[ **\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)) を削除します。

### <a name="prerequisites"></a>前提条件

登録要求を送信する前に、次のことを確認してください。

-   デバイス内の関数の数がわかっています。 この数値は、get 構成要求によって取得された記述子を派生させることができます。
-   前の[**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)の呼び出しで USBD ハンドルを取得しました。
-   基になる USB ドライバースタックは、USB 3.0 デバイスをサポートしています。 これを行うには、 [**USBD\_IsInterfaceVersionSupported**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isinterfaceversionsupported)を呼び出し、USBD\_INTERFACE\_version\_602 を、確認するバージョンとして渡します。

コード例については、「[複合ドライバーで関数の中断を実装する方法](how-to--implement-remote-and-function-wake-support.md)」を参照してください。
手順
------------

### <a name="register-a-composite-device"></a>複合デバイスを登録する

次の手順では、複合ドライバーを USB ドライバースタックと関連付けるための登録要求を作成して送信する方法について説明します。

1.  [**複合\_デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_composite_device_capabilities)の構造体を割り当て、[**複合\_デバイス\_\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-composite_device_capabilities_init)を呼び出すことによって初期化マクロを初期化します。
2.  [**複合\_デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_composite_device_capabilities)の**CapabilityFunctionSuspend**メンバーを1に設定します。
3.  [**USBD\_BuildRegisterCompositeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_buildregistercompositedevice)ルーチンを呼び出して、[**登録\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_register_composite_device)構造体に割り当て、構造体を初期化します。 呼び出しで、USBD ハンドル、初期化された[**複合\_デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_composite_device_capabilities)の構造体、および関数の数を指定します。
4.  [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)を呼び出して i/o 要求パケット (irp) を割り当て、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)ドの場所を呼び出して、irp の最初のスタック位置 ([**IO\_スタックの\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)) へのポインターを取得します。
5.  関数ハンドルの配列を保持するのに十分な大きさのバッファー (USBD\_関数\_ハンドル) にメモリを割り当てます。 配列内の要素の数は、PDOs の数である必要があります。
6.  [**IO\_STACK\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の次のメンバーを設定して、要求を作成します。
    -   要求の種類を指定するには、 [ **\_内部\_USB\_\_複合\_デバイスを登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_register_composite_device)し**ます。**
    -   入力パラメーターを指定するには、**引数 1**を、初期化されたレジスタのアドレスに設定します。[**複合\_デバイス構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_register_composite_device)ます。
    -   **AssociatedIrp**を、手順 5. で割り当てたバッファーに設定して、出力パラメーターを指定します。

7.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、IRP を次のスタック位置に渡して要求を送信します。

完了したら、USB ドライバースタックによって返される関数ハンドルの配列を調べます。 将来使用するために、ドライバーのデバイスコンテキストに配列を格納できます。

次のコード例は、登録要求をビルドして送信する方法を示しています。 この例では、複合ドライバーが、以前に取得した関数の数と USBD ハンドルをドライバーのデバイスコンテキストに格納していることを前提としています。

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

### <a name="unregister-the-composite-device"></a>複合デバイスの登録解除

1.  [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)を呼び出して irp を割り当て、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)ドの場所を呼び出して、irp の最初のスタック位置 ([**IO\_stack\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)) へのポインターを取得します。
2.  [**IO\_STACK\_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の**Parameters. DeviceIoControl**メンバーを[**IOCTL\_内部\_USB\_登録解除\_複合\_デバイスの登録を解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_unregister_composite_device)して、要求をビルドします.
3.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、IRP を次のスタック位置に渡して要求を送信します。

[ **\_内部\_USB\_登録解除\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_unregister_composite_device)の要求は、デバイスの削除ルーチンのコンテキストで複合ドライバーによって1回送信されます。 要求の目的は、USB ドライバースタックと複合ドライバーとその列挙関数との関連付けを削除することです。 また、要求は、その関連付けと、前の登録要求で返されたすべての関数ハンドルを維持するために作成されたすべてのリソースをクリーンアップします。

次のコード例は、複合デバイスの登録を解除する要求を作成して送信する方法を示しています。 この例では、このトピックで既に説明したように、複合ドライバーが登録要求によって既に登録されていることを前提としています。

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
[**IOCTL\_内部\_USB\_登録\_複合\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_register_composite_device)  
[**IOCTL\_内蔵\_USB\_\_複合\_デバイスの登録解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_unregister_composite_device)  



