---
title: コントロール デバイス オブジェクトの作成
description: コントロール デバイス オブジェクトの作成
ms.assetid: 9f89fd24-59b8-4529-b151-4e91e6334173
keywords:
- デバイスオブジェクトの管理 WDK ファイルシステム
- CDOs WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e1284bb6d259a855e2d464929b90880d26eeb9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841447"
---
# <a name="creating-the-control-device-object"></a>コントロール デバイス オブジェクトの作成


## <span id="ddk_creating_the_control_device_object_if"></span><span id="DDK_CREATING_THE_CONTROL_DEVICE_OBJECT_IF"></span>


通常、ファイルシステムフィルタードライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、*コントロールデバイスオブジェクト*を作成することから始まります。 コントロールデバイスオブジェクトの目的は、フィルターがファイルシステムまたはボリュームデバイスオブジェクトにアタッチされる前であっても、アプリケーションがフィルタードライバーと直接通信できるようにすることです。

ファイルシステムでは、コントロールデバイスオブジェクトも作成されることに注意してください。 ファイルシステムフィルタードライバーは、個々のファイルシステムボリュームではなく、ファイルシステムにそれ自体をアタッチするときに、ファイルシステムのコントロールデバイスオブジェクトにそれ自体をアタッチします。

次の例では、コントロールデバイスオブジェクトを作成します。

```cpp
RtlInitUnicodeString(&nameString, MYLEGACYFILTER_FULLDEVICE_NAME);
status = IoCreateDevice(
        DriverObject,                  //DriverObject
        0,                             //DeviceExtensionSize
        &nameString,                   //DeviceName
        FILE_DEVICE_DISK_FILE_SYSTEM,  //DeviceType
        FILE_DEVICE_SECURE_OPEN,       //DeviceCharacteristics
        FALSE,                         //Exclusive
        &gControlDeviceObject);        //DeviceObject

RtlInitUnicodeString(&linkString, MYLEGACYFILTER_DOSDEVICE_NAME);
status = IoCreateSymbolicLink(&linkString, &nameString);
```

ファイルシステムとは異なり、ファイルシステムフィルタードライバーは、コントロールデバイスオブジェクトに名前を指定する必要はありません。 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)への呼び出しはコントロールデバイスオブジェクトに対して無効であるため、ユーザーモードアプリケーションは、デバイス名を使用してフィルタードライバーにアクセスすることはできません。 *DeviceName*パラメーターに**NULL**以外の値が渡された場合、この値はコントロールデバイスオブジェクトの名前になります。 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、前のコード例に示されているように、 [**Ioiostream Ymの iclink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)ルーチンを呼び出して、オブジェクトのカーネルモード名をアプリケーションから参照できるユーザーモード名にリンクさせることができます。

**注**  コントロールデバイスオブジェクトは、ドライバースタックにアタッチされていない唯一のデバイスオブジェクトであるため、安全に名前を付けることができるデバイスオブジェクトの唯一の種類です。 このため、ファイルシステムフィルタードライバーのデバイスオブジェクトの制御には、必要に応じて名前を付けることができます。 ファイルシステムのコントロールデバイスオブジェクトには名前を付ける必要があることに注意してください。 フィルターデバイスオブジェクトに名前を付けることはできません。

 

*(Devicetype*パラメーターに割り当てられる値は、ntifs で定義されているデバイスの種類の1つである必要があります。たとえば、ファイル\_デバイス\_ディスク\_ファイル\_システムなどです。

*DeviceName*パラメーターに**NULL**以外の値が渡された場合、 *DEVICECHARACTERISTICS*フラグには、ファイル\_デバイス\_セキュリティで保護された\_を開く必要があります。 このフラグは、コントロールデバイスオブジェクトに送信されるすべての開いている要求に対してセキュリティチェックを実行するように i/o マネージャーに指示します。 これらのセキュリティチェックは、名前付きデバイスオブジェクトの ACL に対して行われます。

ファイルシステムフィルタードライバーがディスパッチルーチンで独自のコントロールデバイスオブジェクトを識別する効果的な方法は、デバイスポインターと、以前に格納されていたグローバルポインターをコントロールデバイスオブジェクトに比較することです。 したがって、前のサンプルでは、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)によって返された*DeviceObject*ポインターを、グローバルに定義されたポインター変数 `gControlDeviceObject`に格納しています。

 

 




