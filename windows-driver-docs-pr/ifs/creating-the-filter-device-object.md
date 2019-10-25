---
title: フィルター デバイス オブジェクトの作成
description: フィルター デバイス オブジェクトの作成
ms.assetid: aca9a2ba-8630-4eb3-9312-a0c6454c3e44
keywords:
- フィルタードライバー WDK ファイルシステム、フィルターのアタッチ
- ファイルシステムフィルタードライバー WDK、添付フィルター
- ファイルシステムまたはボリュームへのフィルターのアタッチ
- ボリューム WDK ファイルシステム、フィルターのアタッチ
- IoCreateDevice
- DOs WDK ファイルシステムをフィルター処理する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99bfb9dce61f5ed0c4469bf04b5de448ef7dcbed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841444"
---
# <a name="creating-the-filter-device-object"></a>フィルター デバイス オブジェクトの作成


## <span id="ddk_creating_the_filter_device_object_if"></span><span id="DDK_CREATING_THE_FILTER_DEVICE_OBJECT_IF"></span>


[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出して、ボリュームまたはファイルシステムスタックにアタッチするフィルターデバイスオブジェクトを作成します。次に例を示します。

```cpp
status = IoCreateDevice(
          gFileSpyDriverObject,                     //DriverObject
          sizeof(MYLEGACYFILTER_DEVICE_EXTENSION),  //DeviceExtensionSize
          NULL,                                     //DeviceName
          DeviceObject->DeviceType,                 //DeviceType
          0,                                        //DeviceCharacteristics
          FALSE,                                    //Exclusive
          &newDeviceObject);                        //DeviceObject
```

上記のコードスニペットでは、 *DeviceObject*は、フィルターデバイスオブジェクトがアタッチされるターゲットデバイスオブジェクトへのポインターです。*newDeviceObject*は、フィルターデバイスオブジェクト自体へのポインターです。

*Deviceextensionsize*パラメーターを**sizeof**(MYLEGACYFILTER\_DEVICE\_extension) に設定すると、フィルターデバイスオブジェクトに対して MYLEGACYFILTER\_デバイス\_拡張構造が割り当てられます。 新しく作成されたフィルターデバイスオブジェクトの**Deviceextension**メンバーは、この構造体を指すように設定されます。 通常、ファイルシステムフィルタードライバーは、各フィルターデバイスオブジェクトのデバイス拡張機能のメモリを定義し、割り当てます。 デバイス拡張機能の構造と内容は、ドライバーによって異なります。 ただし、Microsoft Windows XP 以降では、フィルタードライバーによって、少なくとも次のメンバーを含むフィルタードライバーオブジェクトのデバイス\_拡張構造が定義されている必要があります。

```cpp
PDEVICE_OBJECT AttachedToDeviceObject;
```

上記の[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)の呼び出しで、 *DeviceName*パラメーターを**NULL**に設定すると、フィルターデバイスオブジェクトの名前は指定されません。 フィルターデバイスオブジェクトには名前が付けられません。 フィルターデバイスオブジェクトはファイルシステムまたはボリュームドライバースタックにアタッチされるので、フィルターデバイスオブジェクトに名前を割り当てると、システムセキュリティホールが作成されます。

*(Devicetype*パラメーターは、フィルターデバイスオブジェクトをアタッチするターゲット (ファイルシステムまたはフィルター) デバイスオブジェクトと同じデバイスの種類に常に設定する必要があります。 この方法でデバイスの種類を伝達することが重要です。この方法は、i/o マネージャーによって使用され、アプリケーションにレポートすることができます。

**注**  ファイルシステムとファイルシステムフィルタードライバーでは、 *(devicetype*パラメーターを FILE\_DEVICE\_file\_system に設定しないでください。 これは、このパラメーターの有効な値ではありません。 (ファイル\_デバイス\_ファイル\_システム定数は、FSCTL コードを定義する目的でのみ使用されます)。

 

*(Devicetype*パラメーターが重要であるもう1つの理由は、特定の種類のファイルシステムにのみ、多くのフィルターがアタッチされることです。 たとえば、特定のフィルターはすべてのローカルディスクファイルシステムにアタッチできますが、CD-ROM ファイルシステムやリモートファイルシステムにはアタッチできません。 このようなフィルターは、ファイルシステムまたはボリュームドライバースタック内の最上位のデバイスオブジェクトのデバイスの種類を調べることによって、ファイルシステムの種類を決定します。 ほとんどの場合、スタック内の最上位のデバイスオブジェクトはフィルターデバイスオブジェクトです。 したがって、添付されているすべてのフィルターデバイスオブジェクトが、基になるファイルシステムまたはボリュームデバイスオブジェクトと同じ種類のデバイスであることが不可欠です。

 

 




