---
Description: In this topic, you will learn about how to select a configuration in a universal serial bus (USB) device.
title: USB デバイスの構成を選択する方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d3f0877c8f73c5a464ea76f21fd5c747faefe85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550987"
---
# <a name="how-to-select-a-configuration-for-a-usb-device"></a>USB デバイスの構成を選択する方法


このトピックでは、ユニバーサル シリアル バス (USB) デバイスで、構成を選択する方法について説明します。

USB デバイスの構成を選択するには、デバイスのクライアント ドライバーはでサポートされる構成の少なくとも 1 つを選択し、使用する各インターフェイスの設定を指定する必要があります。、 クライアント ドライバー パッケージには、*選択構成要求*具体的には、USB バス ドライバー (USB ハブ PDO)、Microsoft 提供の USB ドライバー スタックに要求を送信します。 USB バス ドライバーが、指定した構成との通信チャネルを設定の各インターフェイスを選択または*パイプ*インターフェイス内で各エンドポイントにします。 要求が完了すると、クライアント ドライバーが選択された構成のハンドルを受け取るし、インターフェイスごとに別のアクティブな設定で定義されているエンドポイントをパイプ処理します。 クライアント ドライバーは、構成設定を変更して、送信 I/O の読み取り/書き込み要求、特定のエンドポイントを受信したハンドルを使用できます。

クライアント ドライバー選択構成要求を送信する、 [USB 要求ブロック (URB)](communicating-with-a-usb-device.md) URB 型の\_関数\_選択\_構成します。 このトピックの手順を使用する方法を説明する、 [ **USBD\_SelectConfigUrbAllocateAndBuild** ](https://msdn.microsoft.com/library/windows/hardware/hh406243)ルーチンをその URB をビルドします。 ルーチンは、メモリを割り当て、URB、選択構成要求が、URB を書式設定し、クライアント ドライバーに URB のアドレスを返します。

代わりに、割り当てることができます、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体であり、URB を手動でまたは呼び出すことによって、その書式を設定、 [ **UsbBuildSelectConfigurationRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538968)マクロ。

### <a name="prerequisites"></a>前提条件

-   Windows 8 で[ **USBD\_SelectConfigUrbAllocateAndBuild** ](https://msdn.microsoft.com/library/windows/hardware/hh406243)置き換えます[ **USBD\_CreateConfigurationRequestEx**](https://msdn.microsoft.com/library/windows/hardware/ff539029).
-   選択構成要求を送信する前に、クライアント ドライバーの登録は USB ドライバー スタックと USBD ハンドルが必要です。 USBD ハンドルの呼び出しを作成する[ **USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)します。
-   構成記述子を取得したかどうかを確認 ([**USB\_構成\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539241)構造) の構成を選択します。 通常、URB 型の URB を送信する\_関数\_取得\_記述子\_FROM\_デバイス (を参照してください[  **\_URB\_コントロール\_記述子\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff540357)) デバイスの構成に関する情報を取得します。 詳細については、次を参照してください。 [USB 構成記述子](usb-configuration-descriptors.md)します。

<a name="instructions"></a>手順
------------

### <a href="" id="create-an-array-of-usbd-interface-list-entry-structures-"></a>手順 1:USBD の配列を作成する\_インターフェイス\_一覧\_エントリの構造体。

1.  構成でインターフェイスの数を取得します。 この情報は、 **bNumInterfaces**のメンバー、 [ **USB\_構成\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539241)構造体。
2.  配列を作成する[ **USBD\_インターフェイス\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff539076)構造体。 配列内の要素の数は、いずれかを指定する必要がありますよりもインターフェイスの数。 呼び出すことによって、配列の初期化[ **RtlZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff563610)します。

    クライアント ドライバーでは、代替の設定を指定の配列で、有効にするには、各インターフェイスで[ **USBD\_インターフェイス\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff539076)構造体。

    -   **InterfaceDescriptor**各構造体のメンバーが別の設定を含むインターフェイス記述子をポイントします。
    -   **インターフェイス**各構造体のメンバーを指す、 [ **USBD\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539068)パイプ情報を含む構造体その**パイプ**メンバー。 **パイプ**別の設定で定義されている各エンドポイントに関する情報を格納します。

3.  構成内の各インターフェイス (または、代替の設定) のインターフェイス記述子を取得します。 これらのインターフェイスの記述子を取得するには呼び出すことによって[ **USBD\_ParseConfigurationDescriptorEx**](https://msdn.microsoft.com/library/windows/hardware/ff539102)します。

    **複合 USB デバイスのドライバーを関数: について  **

    Microsoft 製で、構成が選択されている USB デバイスが複合デバイスの場合は、[汎用的な親の USB ドライバー](usb-common-class-generic-parent-driver.md) (Usbccgp.sys)。 複合デバイスの機能のドライバーのいずれかには、クライアント ドライバーは、構成を変更できませんが、ドライバーはで、Usbccgp.sys を介して選択構成要求を送信できます。

    その要求を送信する前に、クライアント ドライバーが、URB を送信する必要があります\_関数\_取得\_記述子\_FROM\_デバイス要求。 応答で、Usbccgp.sys 取得、*部分構成記述子*インターフェイス記述子と対象のクライアント ドライバーが読み込まれる特定の機能に関連するその他の記述子のみを格納します。 報告されたインターフェイスの数、 **bNumInterfaces**部分構成記述子のフィールドが USB 複合デバイス全体に対して定義されているインターフェイスの合計数より小さい。 さらに、部分構成記述子に、インターフェイス、記述子の**bInterfaceNumber**デバイス全体の基準とした実際のインターフェイスの数を示します。 Usbccgp.sys 可能性がありますの部分構成記述子を報告するなど、 **bNumInterfaces** 2 の値と**bInterfaceNumber**値を 4 に、最初のインターフェイス。 インターフェイスの数が報告されたインターフェイスの数より大きいことに注意してください。

    部分的な構成でインターフェイスを列挙中に、インターフェイスの数に基づくインターフェイスの数を計算することでインターフェイスを検索しないようにします。 前の例では場合、 [ **USBD\_ParseConfigurationDescriptorEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539102) 0 から始まり、終わりをループで呼び出される`(bNumInterfaces - 1)`、(指定したインターフェイス インデックスをインクリメントして*InterfaceNumber*パラメーター) ルーチンを各反復処理では、適切なインターフェイスを取得するが失敗しました。 代わりに-1 を渡すことによって構成記述子ですべてのインターフェイスを検索することを必ず*InterfaceNumber*します。 実装の詳細については、このセクションのコード例を参照してください。

    Usbccgp.sys クライアント ドライバーによって送信される選択構成要求を処理する方法については、次を参照してください。[既定以外の USB の構成を選択する構成で、Usbccgp.sys](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)します。

4.  各配列の要素 (最後の要素) を除く、設定、 **InterfaceDescriptor**インターフェイス、記述子のアドレスへのメンバー。 配列の最初の要素、設定、 **InterfaceDescriptor**構成では、最初のインターフェイスを表すインターフェイス記述子のアドレスへのメンバー。 同様に、 *n*番目の要素の配列内の設定、 **InterfaceDescriptor**メンバーを表すインターフェイス記述子のアドレスを*n*番目のインターフェイスで、構成します。
5.  **InterfaceDescriptor**の最後の要素のメンバーを NULL に設定する必要があります。

### <a href="" id="get-a-pointer-to-an-urb-allocated-by-the-usb-driver-stack-"></a>手順 2:USB ドライバー スタックによって割り当てられた、URB へのポインターを取得します。

次に、呼び出す[ **USBD\_SelectConfigUrbAllocateAndBuild** ](https://msdn.microsoft.com/library/windows/hardware/hh406243)を選択する構成とのデータが設定された配列を指定することによって[ **USBD\_インターフェイス\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff539076)構造体。 ルーチンは、次のタスクを実行します。

-   URB を作成および指定した構成、そのインターフェイスおよびエンドポイントに関する情報が格納され、URB に要求の種類を設定\_関数\_選択\_構成します。
-   その URB、内で割り当て、 [ **USBD\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539068)クライアント ドライバーを指定する各インターフェイスの記述子の構造体。
-   セット、**インターフェイス**のメンバー、 *n*番目の要素の呼び出し元の[ **USBD\_インターフェイス\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff539076)配列の対応するアドレスに[ **USBD\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539068) URB で構造体。
-   初期化します、 **InterfaceNumber**、 **AlternateSetting**、 **NumberOfPipes**、**パイプ\[は\]します。MaximumTransferSize**、および**パイプ\[は\]します。PipeFlags**メンバー。

    **注**  Windows 7 および前のでは、クライアント ドライバーは呼び出すことによって、URB 選択構成要求を作成[ **USBD\_CreateConfigurationRequestEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539029). Windows 2000 で**USBD\_CreateConfigurationRequestEx**初期化**パイプ\[は\]します。MaximumTransferSize** URB の読み取り/書き込み要求を 1 つの既定の最大転送サイズ。 クライアント ドライバーで別の最大転送サイズを指定できます、**パイプ\[は\]します。MaximumTransferSize**します。 USB スタックでは、Windows XP、Windows Server 2003、およびそれ以降のバージョンのオペレーティング システムでは、この値は無視されます。 詳細については**MaximumTransferSize**、「設定 USB 転送し、パケット サイズ」を参照してください[USB の帯域幅割り当て](usb-bandwidth-allocation.md)します。

### <a href="" id="submit-the-urb-to-the-usb-driver-stack-"></a>手順 3:USB ドライバー スタックに URB を送信します。

USB ドライバー スタックに URB を送信するクライアント ドライバーを送信する必要があります、 [ **IOCTL\_内部\_USB\_送信\_URB** ](https://msdn.microsoft.com/library/windows/hardware/ff537271) I/O 制御要求。 URB を送信する方法の詳細については、次を参照してください。 [、URB を送信する方法](send-requests-to-the-usb-driver-stack.md)します。

USB ドライバー スタックを URB を受信した後に、残りの部分の各メンバーの[ **USBD\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539068)構造体。 具体的には、**パイプ**配列メンバーは、インターフェイスのエンドポイントに関連付けられているパイプに関する情報を入力します。

### <a href="" id="on-request-completion--inspect-the-usbd-interface-information-structures-and-the-urb-"></a>手順 4:要求完了時に検査、USBD\_インターフェイス\_情報構造体と URB します。

スタックが代替の設定との関連するインターフェイスの一覧を返します、USB ドライバー スタックには、要求の IRP が完了すると、 [ **USBD\_インターフェイス\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff539076)配列。

1.  **パイプ**のそれぞれに所属[ **USBD\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539068)の配列へのポインターを構造体[ **USBD\_パイプ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539114)その特定のインターフェイスの各エンドポイントに関連付けられているパイプに関する情報を含む構造体。 クライアント ドライバーからパイプ ハンドルを取得できます**パイプ\[は\]します。PipeHandle**使用と、特定のパイプに I/O 要求を送信します。 **パイプ\[は\]します。PipeType**メンバーは、エンドポイントとそのパイプでサポートされている転送の種類を指定します。

2.  内で、 **UrbSelectConfiguration** URB のメンバーは、USB ドライバー スタックは、型 URB の URB を送信して別のインターフェイスの設定を選択するために使用できるハンドルを返します\_関数\_選択\_インターフェイス (*選択インターフェイス要求*)。 割り当てをその要求について、URB 構造の作成は、呼び出す[ **USBD\_SelectInterfaceUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406245)します。

    アイソクロナスのコントロールをサポートし、有効になっているインターフェイス内でエンドポイントを中断する十分な帯域幅がある場合、選択構成要求と インターフェイスの要求が失敗します。 その場合は、USB バス ドライバーの設定、**状態**USBD URB ヘッダーのメンバー\_状態\_いいえ\_帯域幅。

次のコード例は、の配列を作成する方法を示しています[ **USBD\_インターフェイス\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff539076)構造と呼び出し[  **。USBD\_SelectConfigUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406243)します。 この例は、SubmitUrbSync を呼び出すことによって同期的に、要求を送信します。 SubmitUrbSync のコード例を参照してくださいを参照してください。 [、URB を送信する方法](send-requests-to-the-usb-driver-stack.md)します。

```ManagedCPlusPlus
/*++

Routine Description:
This helper routine selects the specified configuration.

Arguments:
USBDHandle - USBD handle that is retrieved by the 
client driver in a previous call to the USBD_CreateHandle routine.

ConfigurationDescriptor - Pointer to the configuration
descriptor for the device. The caller receives this pointer
from the URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE request.

Return Value: NT status value
--*/

NTSTATUS SelectConfiguration (PDEVICE_OBJECT DeviceObject,
                              PUSB_CONFIGURATION_DESCRIPTOR ConfigurationDescriptor)
{
    PDEVICE_EXTENSION deviceExtension;
    PIO_STACK_LOCATION nextStack;
    PIRP irp;
    PURB urb = NULL;

    KEVENT    kEvent;
    NTSTATUS ntStatus;    

    PUSBD_INTERFACE_LIST_ENTRY   interfaceList = NULL; 
    PUSB_INTERFACE_DESCRIPTOR    interfaceDescriptor = NULL;
    PUSBD_INTERFACE_INFORMATION  Interface = NULL;
    USBD_PIPE_HANDLE             pipeHandle;

    ULONG                        interfaceIndex;

    PUCHAR StartPosition = (PUCHAR)ConfigurationDescriptor;

    deviceExtension = (PDEVICE_EXTENSION)DeviceObject->DeviceExtension;

    // Allocate an array for the list of interfaces
    // The number of elements must be one more than number of interfaces.
    interfaceList = (PUSBD_INTERFACE_LIST_ENTRY)ExAllocatePool (
        NonPagedPool, 
        sizeof(USBD_INTERFACE_LIST_ENTRY) *
        (deviceExtension->NumInterfaces + 1));

    if(!interfaceList)
    {
        //Failed to allocate memory
        ntStatus = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    // Initialize the array by setting all members to NULL.
    RtlZeroMemory (interfaceList, sizeof (
        USBD_INTERFACE_LIST_ENTRY) *
        (deviceExtension->NumInterfaces + 1));

    // Enumerate interfaces in the configuration.
    for ( interfaceIndex = 0; 
        interfaceIndex < deviceExtension->NumInterfaces; 
        interfaceIndex++) 
    {
        interfaceDescriptor = USBD_ParseConfigurationDescriptorEx(
            ConfigurationDescriptor, 
            StartPosition, // StartPosition 
            -1,            // InterfaceNumber
            0,             // AlternateSetting
            -1,            // InterfaceClass
            -1,            // InterfaceSubClass
            -1);           // InterfaceProtocol

        if (!interfaceDescriptor) 
        {
            ntStatus = STATUS_INSUFFICIENT_RESOURCES;
            goto Exit;
        }

        // Set the interface entry
        interfaceList[interfaceIndex].InterfaceDescriptor = interfaceDescriptor;
        interfaceList[interfaceIndex].Interface = NULL;

        // Move the position to the next interface descriptor
        StartPosition = (PUCHAR)interfaceDescriptor + interfaceDescriptor->bLength;

    }

    // Make sure that the InterfaceDescriptor member of the last element to NULL.
    interfaceList[deviceExtension->NumInterfaces].InterfaceDescriptor = NULL;

    // Allocate and build an URB for the select-configuration request.
    ntStatus = USBD_SelectConfigUrbAllocateAndBuild(
        deviceExtension->UsbdHandle, 
        ConfigurationDescriptor, 
        interfaceList,
        &urb);

    if(!NT_SUCCESS(ntStatus)) 
    {
        goto Exit;
    }

    // Allocate the IRP to send the buffer down the USB stack.
    // The IRP will be freed by IO manager.
    irp = IoAllocateIrp((deviceExtension->NextDeviceObject->StackSize)+1, TRUE);  

    if (!irp)
    {
        //Irp could not be allocated.
        ntStatus = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    ntStatus = SubmitUrbSync( 
        deviceExtension->NextDeviceObject, 
        irp, 
        urb, 
        CompletionRoutine);

    // Enumerate the pipes in the interface information array, which is now filled with pipe
    // information.

    for ( interfaceIndex = 0; 
        interfaceIndex < deviceExtension->NumInterfaces; 
        interfaceIndex++) 
    {
        ULONG i;

        Interface = interfaceList[interfaceIndex].Interface;

        for(i=0; i < Interface->NumberOfPipes; i++) 
        {
            pipeHandle = Interface->Pipes[i].PipeHandle;

            if (Interface->Pipes[i].PipeType == UsbdPipeTypeInterrupt)
            {
                deviceExtension->InterruptPipe = pipeHandle;
            }
            if (Interface->Pipes[i].PipeType == UsbdPipeTypeBulk && USB_ENDPOINT_DIRECTION_IN (Interface->Pipes[i].EndpointAddress))
            {
                deviceExtension->BulkInPipe = pipeHandle;
            }
            if (Interface->Pipes[i].PipeType == UsbdPipeTypeBulk && USB_ENDPOINT_DIRECTION_OUT (Interface->Pipes[i].EndpointAddress))
            {
                deviceExtension->BulkOutPipe = pipeHandle;
            }
        }
    }

Exit:

    if(interfaceList) 
    {
        ExFreePool(interfaceList);
        interfaceList = NULL;
    }

    if (urb)
    {
        USBD_UrbFree( deviceExtension->UsbdHandle, urb); 
    }


    return ntStatus;

}

NTSTATUS CompletionRoutine ( PDEVICE_OBJECT DeviceObject,
                            PIRP           Irp,
                            PVOID          Context)
{
    PKEVENT kevent;

    kevent = (PKEVENT) Context;

    if (Irp->PendingReturned == TRUE)
    {
        KeSetEvent(kevent, IO_NO_INCREMENT, FALSE);
    }

    KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "Select-configuration request completed. \n" ));


    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

<a name="remarks"></a>注釈
-------

**USB デバイスの構成を無効になります。  **

USB デバイスを無効にするには、作成し、NULL 構成記述子を使用して、選択構成要求を送信します。 要求の種類、デバイスの構成が選択されている要求用に作成した URB を再利用できます。 代わりに、呼び出すことによって新しい URB を割り当てることができます[ **USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)します。 使用して、URB の書式を設定する必要があります、要求を送信する前に、 [ **UsbBuildSelectConfigurationRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538968)マクロでは、次のコード例に示すようにします。

```ManagedCPlusPlus
URB Urb;
UsbBuildSelectConfigurationRequest(
  &Urb,
  sizeof(_URB_SELECT_CONFIGURATION),
  NULL
);
```

## <a name="related-topics"></a>関連トピック
[既定ではない USB 構成を選択する構成で、Usbccgp.sys](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)  
[USB デバイスの構成](configuring-usb-devices.md)  
[割り当てと翻訳の構築](how-to-add-xrb-support-for-client-drivers.md)  



