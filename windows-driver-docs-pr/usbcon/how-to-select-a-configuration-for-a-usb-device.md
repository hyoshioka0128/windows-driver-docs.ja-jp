---
Description: このトピックでは、ユニバーサルシリアルバス (USB) デバイスで構成を選択する方法について説明します。
title: USB デバイス用の構成の選択方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2a911048cf4083e3e2287ab67e787308d35cf68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844367"
---
# <a name="how-to-select-a-configuration-for-a-usb-device"></a>USB デバイス用の構成の選択方法


このトピックでは、ユニバーサルシリアルバス (USB) デバイスで構成を選択する方法について説明します。

USB デバイスの構成を選択するには、デバイスのクライアントドライバーで、サポートされている構成のうち少なくとも1つを選択し、使用する各インターフェイスの代替設定を指定する必要があります。 クライアントドライバーは、*選択構成要求*でこれらの選択をパッケージ化し、Microsoft 提供の usb ドライバースタック (特に USB ハブ PDO) に要求を送信します。 USB バスドライバーは、指定された構成内の各インターフェイスを選択し、インターフェイス内の各エンドポイントへの通信チャネル (*パイプ*) を設定します。 要求が完了すると、クライアントドライバーは、選択された構成のハンドルと、各インターフェイスのアクティブな代替設定で定義されているエンドポイントのパイプハンドルを受け取ります。 クライアントドライバーは、受信したハンドルを使用して、構成設定を変更し、特定のエンドポイントに対して i/o 読み取り要求と書き込み要求を送信します。

クライアントドライバーは、種類が URB\_関数の[USB 要求ブロック (urb)](communicating-with-a-usb-device.md)で選択構成要求を送信し\_\_構成を選択します。 このトピックの手順では、 [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)ルーチンを使用してその URB を作成する方法について説明します。 このルーチンは、URB にメモリを割り当て、選択構成要求の URB をフォーマットし、クライアントドライバーに URB のアドレスを返します。

または、 [**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造を割り当てて、手動で、または[**Usbbuildselectconfigurationrequest**](https://docs.microsoft.com/previous-versions/ff538968(v=vs.85))マクロを呼び出して、urb をフォーマットすることもできます。

### <a name="prerequisites"></a>前提条件

-   Windows 8 では、 [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)は[**USBD\_CreateConfigurationRequestEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex)に置き換わるものです。
-   選択構成要求を送信する前に、クライアントドライバーの USB ドライバースタックへの登録を USBD ハンドルする必要があります。 USBD ハンドル呼び出しを作成するには、 [**CreateHandle を\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)します。
-   選択する構成の構成記述子 ([**USB\_構成\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)構造) を取得していることを確認します。 通常、デバイスに関する情報を取得するには、型の urb\_関数の URB を送信し\_\_デバイスから\_記述子\_を取得します (「 [ **\_URB\_CONTROL\_DESCRIPTOR\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request))」を参照してください。configuration. 詳細については、「 [USB 構成記述子](usb-configuration-descriptors.md)」を参照してください。

<a name="instructions"></a>手順
------------

### <a href="" id="create-an-array-of-usbd-interface-list-entry-structures-"></a>手順 1: USBD\_INTERFACE\_LIST\_エントリ構造体の配列を作成します。

1.  構成内のインターフェイスの数を取得します。 この情報は、 [**USB\_構成\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)構造体の**bnuminterfaces**メンバーに含まれています。
2.  [**USBD\_INTERFACE\_LIST\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)構造体の配列を作成します。 配列内の要素の数は、インターフェイスの数より1つ多くする必要があります。 [**Rtlゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)を呼び出して配列を初期化します。

    クライアントドライバーは、有効にする各インターフェイスの代替設定を指定します。これは、 [**USBD\_interface\_LIST\_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)構造体の配列に含まれています。

    -   各構造体の**interfacedescriptor**メンバーは、代替設定を含むインターフェイス記述子を指します。
    -   各構造体の**インターフェイス**メンバーは **、パイプのメンバーに**パイプ情報を格納する[**USBD\_インターフェイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information)構造体を指します。 **パイプ**は、別の設定で定義されている各エンドポイントに関する情報を格納します。

3.  構成内の各インターフェイス (またはその代替設定) のインターフェイス記述子を取得します。 これらのインターフェイス記述子は、 [**USBD\_ParseConfigurationDescriptorEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex)を呼び出すことによって取得できます。

    **USB 複合デバイスの関数ドライバーについて:  **

    USB デバイスが複合デバイスの場合、構成は、Microsoft 提供の[Usb 汎用親ドライバー](usb-common-class-generic-parent-driver.md) (Usbccgp) によって選択されます。 複合デバイスの機能ドライバーの1つであるクライアントドライバーは、構成を変更することはできませんが、ドライバーは Usbccgp を使用して、選択的な構成要求を送信することができます。

    クライアントドライバーは、要求を送信する前に、\_デバイス要求から\_記述子\_を取得\_ために、URB\_関数を送信する必要があります。 応答として、Usbccgp は、クライアントドライバーが読み込まれる特定の関数に関連するインターフェイス記述子とその他の記述子だけを含む*部分構成記述子*を取得します。 部分構成記述子の**Bnuminterfaces**フィールドで報告されるインターフェイスの数が、USB 複合デバイス全体に対して定義されているインターフェイスの合計数よりも少なくなっています。 さらに、部分構成記述子では、インターフェイス記述子の**bInterfaceNumber**は、デバイス全体に対する実際のインターフェイス番号を示します。 たとえば、Usbccgp は、最初のインターフェイスに対して**Bnuminterfaces**値が2、 **bInterfaceNumber**値が4の部分構成記述子を報告する場合があります。 インターフェイス番号が、報告されたインターフェイスの数よりも大きいことに注意してください。

    部分構成でインターフェイスを列挙するときに、インターフェイスの数に基づいてインターフェイス番号を計算することで、インターフェイスを検索しないようにします。 前の例では、 [**USBD\_ParseConfigurationDescriptorEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex)が0から始まるループで呼び出され、`(bNumInterfaces - 1)`で終了し、各反復で ( *InterfaceNumber*パラメーターで指定された) インターフェイスインデックスをインクリメントします。ルーチンは、正しいインターフェイスを取得できませんでした。 代わりに、 *InterfaceNumber*で-1 を渡して、構成記述子内のすべてのインターフェイスを検索するようにしてください。 実装の詳細については、このセクションのコード例を参照してください。

    クライアントドライバーによって送信される選択構成要求を Usbccgp が処理する方法の詳細については、「 [Usbccgp を構成して既定以外の USB 構成を選択する」を](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)参照してください。

4.  配列内の各要素 (最後の要素を除く) に対して、 **interfacedescriptor**メンバーをインターフェイス記述子のアドレスに設定します。 配列内の最初の要素に対して、 **interfacedescriptor**メンバーを、構成内の最初のインターフェイスを表すインターフェイス記述子のアドレスに設定します。 同様に、配列内の*n*番目の要素については、 **interfacedescriptor**メンバーを、構成内の*n*番目のインターフェイスを表すインターフェイス記述子のアドレスに設定します。
5.  最後の要素の**Interfacedescriptor**メンバーは、NULL に設定する必要があります。

### <a href="" id="get-a-pointer-to-an-urb-allocated-by-the-usb-driver-stack-"></a>手順 2: USB ドライバースタックによって割り当てられた URB へのポインターを取得します。

次に、 [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)を呼び出します。これには、選択する構成と、 [**USBD\_インターフェイス\_リスト\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)構造の設定された配列を指定します。 ルーチンは、次のタスクを実行します。

-   URB を作成し、指定された構成、そのインターフェイス、およびエンドポイントに関する情報を入力して、要求の種類を URB\_機能に設定し\_\_構成を選択します。
-   この URB 内で、クライアントドライバーが指定する各インターフェイス記述子に対して、 [**USBD\_インターフェイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information)構造体を割り当てます。
-   呼び出し元が指定した[**USBD\_インターフェイス\_リスト\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)配列の*n*番目の要素の**インターフェイス**メンバーを、対応する[**USBD\_インターフェイスの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information)のアドレスに設定します。URB 内の構造体。
-   **InterfaceNumber**、 **alternatesetting**、 **numberofpipes**、パイプ\[\]を初期化し**ます。MaximumTransferSize**と**パイプ\[\]。PipeFlags**のメンバー。

    Windows 7 と USBD では、クライアントドライバーは[ **\_CreateConfigurationRequestEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex)を呼び**出すことに**よって、選択構成要求の URB を作成しました。   Windows 2000 **USBD\_CreateConfigurationRequestEx**は、 **\]\[パイプを初期化します。MaximumTransferSize**は、単一の URB 読み取り/書き込み要求の既定の最大転送サイズに設定します。 クライアントドライバーは、\]\[パイプで異なる最大転送サイズを指定でき**ます。MaximumTransferSize**。 USB スタックは、Windows XP、Windows Server 2003、およびそれ以降のバージョンのオペレーティングシステムでは、この値を無視します。 **MaximumTransferSize**の詳細については、「 [usb 帯域幅の割り当て](usb-bandwidth-allocation.md)」の「Usb 転送とパケットサイズの設定」を参照してください。

### <a href="" id="submit-the-urb-to-the-usb-driver-stack-"></a>手順 3: URB を USB ドライバースタックに送信します。

USB ドライバースタックに URB を送信するには、クライアントドライバーが\_URB I/o 制御要求を[**送信\_の内部\_usb\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)送信する必要があります。 URB の送信の詳細については、「 [urb を送信する方法](send-requests-to-the-usb-driver-stack.md)」を参照してください。

URB を受信すると、USB ドライバースタックによって、各[**USBD\_インターフェイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information)構造体の残りのメンバーがいっぱいになります。 特に、**パイプ**の配列メンバーには、インターフェイスのエンドポイントに関連付けられているパイプに関する情報が格納されます。

### <a href="" id="on-request-completion--inspect-the-usbd-interface-information-structures-and-the-urb-"></a>手順 4: 要求の完了時に、USBD\_インターフェイス\_情報構造と URB を調べます。

USB ドライバースタックが要求の IRP を完了すると、スタックは、代替設定の一覧と、 [**USBD\_インターフェイス\_リスト\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)配列内の関連インターフェイスを返します。

1.  各[**USBD\_インターフェイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information)構造体の**パイプ**メンバーは、各エンドポイントに関連付けられているパイプに関する情報を含む[**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)構造体の配列を指します。特定のインターフェイスの。 クライアントドライバーは、\]\[パイプからパイプハンドルを取得でき**ます。PipeHandle**を使用して、特定のパイプに i/o 要求を送信します。 **パイプ\[\]。PipeType**メンバーは、そのパイプでサポートされているエンドポイントと転送の種類を指定します。

2.  USB ドライバースタックは、URB の**Urbselectconfiguration**メンバー内で、種類の URB\_関数の別の urb を送信することによって代替インターフェイス設定を選択するために使用できるハンドルを返し\_\_インターフェイスを選択します ( *[インターフェイス要求] を選択*します。 その要求の URB 構造を割り当ててビルドするには、 [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)を呼び出します。

    有効なインターフェイス内のアイソクロナス、制御、および割り込みエンドポイントをサポートするための帯域幅が不足している場合は、構成要求と選択インターフェイスの要求が失敗する可能性があります。 この場合、USB バスドライバーは、URB ヘッダーの**status**メンバーを USBD\_status\_\_帯域幅なしに設定します。

次のコード例では、 [**USBD\_インターフェイス\_LIST\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)構造体の配列を作成し、 [**SelectConfigUrbAllocateAndBuild\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)を呼び出す方法を示します。 この例では、SubmitUrbSync を呼び出して要求を同期的に送信します。 SubmitUrbSync のコード例については、「 [URB を送信する方法](send-requests-to-the-usb-driver-stack.md)」を参照してください。

```C++
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

**USB デバイスの構成を無効にする:**

USB デバイスを無効にするには、構成記述子が NULL の選択構成要求を作成して送信します。 この種類の要求については、デバイスで構成を選択した要求に対して作成した URB を再利用できます。 または、USBD を呼び出すことによって新しい URB を割り当てることもできます。 [ **\_を指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)します。 要求を送信する前に、次のコード例に示すように、 [**Usbbuildselectconfigurationrequest**](https://docs.microsoft.com/previous-versions/ff538968(v=vs.85))マクロを使用して URB をフォーマットする必要があります。

```C++
URB Urb;
UsbBuildSelectConfigurationRequest(
  &Urb,
  sizeof(_URB_SELECT_CONFIGURATION),
  NULL
);
```

## <a name="related-topics"></a>関連トピック
[既定以外の USB 構成を選択するように Usbccgp を構成する](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)  
[USB デバイスの構成](configuring-usb-devices.md)  
[URBs の割り当てとビルド](how-to-add-xrb-support-for-client-drivers.md)  



