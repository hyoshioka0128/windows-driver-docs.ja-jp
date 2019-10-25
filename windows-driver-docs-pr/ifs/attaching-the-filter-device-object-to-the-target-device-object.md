---
title: フィルターデバイスオブジェクトをターゲットデバイスオブジェクトにアタッチしています
description: フィルターデバイスオブジェクトをターゲットデバイスオブジェクトにアタッチしています
ms.assetid: 1df293db-417a-4fee-afb8-06ab527331fb
keywords:
- フィルタードライバー WDK ファイルシステム、フィルターのアタッチ
- ファイルシステムフィルタードライバー WDK、添付フィルター
- ファイルシステムまたはボリュームへのフィルターのアタッチ
- ボリューム WDK ファイルシステム、フィルターのアタッチ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8407979851e70b765bc771becd8eda59804eba72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841487"
---
# <a name="attaching-the-filter-device-object-to-the-target-device-object"></a>フィルターデバイスオブジェクトをターゲットデバイスオブジェクトにアタッチしています


## <span id="ddk_attaching_the_filter_device_object_to_the_target_device_object_if"></span><span id="DDK_ATTACHING_THE_FILTER_DEVICE_OBJECT_TO_THE_TARGET_DEVICE_OBJECT_IF"></span>


[**Ioattachdevicetodevicestacksafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)を呼び出して、フィルターデバイスオブジェクトをターゲットファイルシステムまたはボリュームのフィルタードライバースタックにアタッチします。

```cpp
devExt = myLegacyFilterDeviceObject->DeviceExtension;

status = IoAttachDeviceToDeviceStackSafe(
           myLegacyFilterDeviceObject,        //SourceDevice
           DeviceObject,                      //TargetDevice
           &devext->AttachedToDeviceObject);  //AttachedToDeviceObject
```

*ほか*によってポイントされているデバイスオブジェクトの上に他のフィルターが既にチェーンされている場合は、 *AttachedToDeviceObject* output パラメーターによって受け取るデバイスオブジェクトのポインターが*ほか*と異なる場合があることに注意してください。

### <a name="span-idattaching_to_a_file_system_by_namespanspan-idattaching_to_a_file_system_by_namespanspan-idattaching_to_a_file_system_by_namespanattaching-to-a-file-system-by-name"></a><span id="Attaching_to_a_File_System_by_Name"></span><span id="attaching_to_a_file_system_by_name"></span><span id="ATTACHING_TO_A_FILE_SYSTEM_BY_NAME"></span>名前によるファイルシステムへのアタッチ

すべてのファイルシステムで、1つまたは複数の名前付きコントロールデバイスオブジェクトを作成する必要があります。 特定のファイルシステムに直接アタッチする場合、ファイルシステムフィルタードライバーは、適切なファイルシステムコントロールデバイスオブジェクトの名前を[**Iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)に渡して、デバイスオブジェクトポインターを取得します。 次のコードスニペットは、RAW ファイルシステムの2つのコントロールデバイスオブジェクトのいずれかへのポインターを取得する方法を示しています。

```cpp
RtlInitUnicodeString(&nameString, L"\\Device\\RawDisk");

status = IoGetDeviceObjectPointer(
            &nameString,                    //ObjectName
            FILE_READ_ATTRIBUTES,           //DesiredAccess
            &fileObject,                    //FileObject
            &rawDeviceObject);              //DeviceObject

if (NT_SUCCESS(status)) {
            ObDereferenceObject(fileObject);
}
```

[**Iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)への呼び出しが成功した場合、ファイルシステムフィルタードライバーは、 [**Ioattachdevicetodevicestacksafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)を呼び出して、返されたコントロールデバイスオブジェクトにアタッチできます。

**注**   コントロールデバイスオブジェクトポインター (*rawDeviceObject*) に加えて、 [**iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)は、ユーザーモードでデバイスオブジェクトを表すファイルオブジェクト (*fileObject*) へのポインターを返します。 上記のコードスニペットでは、ファイルオブジェクトは必要ないため、 [**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出すことによって閉じられます。 **Iogetdeviceobjectpointer**によって返されるファイルオブジェクトの参照カウントをデクリメントすると、デバイスオブジェクトの参照カウントもデクリメントされることに注意する必要があります。 そのため、デバイスオブジェクトの参照カウントがの追加の呼び出し[**によってインクリメントされていない限り、この ObDereferenceObject を呼び出した後に、fileObject ポインターと rawDeviceObject ポインターの両方が無効であると見なされる必要があります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject) **ObDereferenceObject**がファイルオブジェクトに対して呼び出される前に、obreferenceobject が呼び出されます。

 

 

 




