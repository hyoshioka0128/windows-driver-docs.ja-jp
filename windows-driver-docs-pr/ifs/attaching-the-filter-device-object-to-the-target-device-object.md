---
title: フィルター デバイス オブジェクトのターゲット デバイス オブジェクトへのアタッチ
description: フィルター デバイス オブジェクトのターゲット デバイス オブジェクトへのアタッチ
ms.assetid: 1df293db-417a-4fee-afb8-06ab527331fb
keywords:
- フィルターをアタッチ、フィルター ドライバー WDK ファイル システム
- ファイル システム フィルター ドライバー WDK、フィルターをアタッチします。
- ファイル システムまたはボリュームにフィルターをアタッチします。
- WDK のボリュームのファイル システム、フィルターをアタッチします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 632edab4f8ae70809e4ab42e31f9a62dd1d23282
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385318"
---
# <a name="attaching-the-filter-device-object-to-the-target-device-object"></a>フィルター デバイス オブジェクトのターゲット デバイス オブジェクトへのアタッチ


## <span id="ddk_attaching_the_filter_device_object_to_the_target_device_object_if"></span><span id="DDK_ATTACHING_THE_FILTER_DEVICE_OBJECT_TO_THE_TARGET_DEVICE_OBJECT_IF"></span>


呼び出す[ **IoAttachDeviceToDeviceStackSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)のターゲット ファイル システムまたはボリューム フィルター ドライバー スタックに、フィルター デバイス オブジェクトをアタッチします。

```cpp
devExt = myLegacyFilterDeviceObject->DeviceExtension;

status = IoAttachDeviceToDeviceStackSafe(
           myLegacyFilterDeviceObject,        //SourceDevice
           DeviceObject,                      //TargetDevice
           &devext->AttachedToDeviceObject);  //AttachedToDeviceObject
```

受信したデバイス オブジェクトへのポインターに注意してください、 *AttachedToDeviceObject*出力パラメーターとは異なる*台*場合、その他のフィルターは、既に上であるデバイス オブジェクト チェーンが指す*台*します。

### <a name="span-idattachingtoafilesystembynamespanspan-idattachingtoafilesystembynamespanspan-idattachingtoafilesystembynamespanattaching-to-a-file-system-by-name"></a><span id="Attaching_to_a_File_System_by_Name"></span><span id="attaching_to_a_file_system_by_name"></span><span id="ATTACHING_TO_A_FILE_SYSTEM_BY_NAME"></span>名前でファイル システムに接続します。

1 つを作成するすべてのファイル システムが必要またはデバイス オブジェクトがコントロールの詳細はという名前です。 直接、ファイル システムで特定のファイル システムに接続するフィルター ドライバーが適切なファイル システム コントロールのデバイス オブジェクトの名前を渡す[ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)デバイス オブジェクトを取得するにはポインター。 次のコード スニペットでは、2 つの制御のデバイス オブジェクトの 1 つに、RAW ファイル システムのようなポインターを取得する方法を示します。

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

場合に呼び出し[ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)成功すると、ファイル システム フィルター ドライバーを呼び出して[ **IoAttachDeviceToDeviceStackSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)制御が返されるデバイス オブジェクトにアタッチします。

**注**  デバイス オブジェクトのポインターをコントロールに加え (*rawDeviceObject*)、 [ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)へのポインターを返しますファイル オブジェクト (*fileObject*) ユーザー モードでデバイス オブジェクトを表します。 上記のコード スニペットで、ファイル オブジェクトは必要ありません、ため、呼び出すことによって閉じられている[ **ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)します。 によって返されるファイル オブジェクトの参照カウントをデクリメントを確認することが重要**IoGetDeviceObjectPointer**もデクリメントされるデバイスのオブジェクトで参照カウントが発生します。 したがって、 *fileObject*と*rawDeviceObject*ポインターが両方無効と見なされる上記の呼び出し後**ObDereferenceObject**の参照カウントがない限り、呼び出しを追加して、デバイス オブジェクトがインクリメントされます[ **ObReferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)する前に**ObDereferenceObject**は、ファイル オブジェクトに対して呼び出されます。

 

 

 




