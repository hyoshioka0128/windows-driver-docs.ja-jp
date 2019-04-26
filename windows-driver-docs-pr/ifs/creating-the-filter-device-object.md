---
title: フィルター デバイス オブジェクトの作成
description: フィルター デバイス オブジェクトの作成
ms.assetid: aca9a2ba-8630-4eb3-9312-a0c6454c3e44
keywords:
- フィルターをアタッチ、フィルター ドライバー WDK ファイル システム
- ファイル システム フィルター ドライバー WDK、フィルターをアタッチします。
- ファイル システムまたはボリュームにフィルターをアタッチします。
- WDK のボリュームのファイル システム、フィルターをアタッチします。
- IoCreateDevice
- DOs WDK ファイル システム フィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23855c49a21b874809fe998826d801e452f67d13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359346"
---
# <a name="creating-the-filter-device-object"></a>フィルター デバイス オブジェクトの作成


## <span id="ddk_creating_the_filter_device_object_if"></span><span id="DDK_CREATING_THE_FILTER_DEVICE_OBJECT_IF"></span>


呼び出す[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)次の例のように、ボリュームまたはファイル システム スタックにアタッチするフィルター デバイス オブジェクトを作成します。

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

上記のコード スニペットで*デバイス オブジェクト*フィルター デバイス オブジェクトをアタッチするする; ターゲット デバイスのオブジェクトへのポインターです*newDeviceObject*フィルター デバイス オブジェクト自体へのポインターです。

設定、 *DeviceExtensionSize*パラメーターを**sizeof**(MYLEGACYFILTER\_デバイス\_拡張機能) により、MYLEGACYFILTER\_デバイス\_フィルターのデバイス オブジェクトに割り当てられる拡張機能の構造体。 新しく作成したフィルター デバイス オブジェクトの**DeviceExtension**この構造体を指すメンバーが設定されます。 ファイル システム フィルター ドライバーは通常定義し、各フィルター デバイス オブジェクトのデバイスの拡張機能用のメモリを割り当てられません。 構造とデバイスの拡張機能の内容は、ドライバー固有です。 ただし、Microsoft Windows XP 以降およびフィルター ドライバーがデバイスを定義する\_以上で、次のメンバーを含むフィルター ドライバー オブジェクトの拡張機能の構造。

```cpp
PDEVICE_OBJECT AttachedToDeviceObject;
```

呼び出しで、上記[ **IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)で、設定、 *DeviceName*パラメーターを**NULL**フィルター デバイス オブジェクトを指定します。というされません。 オブジェクトが決してという名前のデバイスをフィルター処理します。 フィルターのデバイス オブジェクトがファイル システム ボリュームまたはボリューム ドライバー スタックにアタッチされている、ため、フィルター デバイス オブジェクトに名前を割り当てると、システム セキュリティ ホールは作成します。

*DeviceType*パラメーターは、フィルター デバイス オブジェクトをアタッチする (ファイル システムまたはフィルター) のターゲット デバイス オブジェクトの場合と同じデバイスの種類に常に設定する必要があります。 I/O マネージャーを使用し、アプリケーションに報告することができますので、この方法でデバイスの種類を反映されるまでに重要です。

**注**  ファイル システムとファイル システム フィルター ドライバーは設定しない必要があります、 *DeviceType*パラメーター ファイルを\_デバイス\_ファイル\_システム。 これは、このパラメーターの有効な値ではありません。 (ファイル\_デバイス\_ファイル\_FSCTL コードの定義に使用されるだけでシステムの定数が対象としています)。

 

理由の 1 つ理由、 *DeviceType*パラメーターが重要ですが、多くのフィルターがだけに特定の種類のファイル システムに接続します。 たとえば、CD-ROM のファイル システムまたはリモート ファイル システムにありませんが、すべてのディスクをローカル ファイル システムに、特定のフィルターをアタッチ可能性があります。 このようなフィルターは、ファイル システム ボリュームまたはボリューム ドライバー スタックの最上位のデバイス オブジェクトのデバイスの種類を調べることで、ファイル システムの種類を決定します。 ほとんどの場合は、スタックの最上位のデバイス オブジェクトは、フィルター デバイス オブジェクトです。 したがって、接続されているフィルターのすべてのデバイス オブジェクトの型としての基になるファイル システム ボリュームまたはボリューム デバイス オブジェクトの同じデバイスである重要なです。

 

 




