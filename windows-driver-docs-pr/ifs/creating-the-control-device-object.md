---
title: コントロールのデバイス オブジェクトを作成します。
description: コントロールのデバイス オブジェクトを作成します。
ms.assetid: 9f89fd24-59b8-4529-b151-4e91e6334173
keywords:
- デバイス オブジェクトの WDK ファイル システムを制御します。
- CDOs WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87cb1f62e103544254cf6909a5ce23c0db6e574b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531895"
---
# <a name="creating-the-control-device-object"></a>コントロールのデバイス オブジェクトを作成します。


## <span id="ddk_creating_the_control_device_object_if"></span><span id="DDK_CREATING_THE_CONTROL_DEVICE_OBJECT_IF"></span>


ファイル システム フィルター ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンが通常作成して開始、*制御デバイス オブジェクト*します。 コントロールのデバイス オブジェクトの目的は、フィルターはファイル システム ボリュームまたはボリューム デバイス オブジェクトにアタッチする前に、直接フィルター ドライバーと通信を許可するのにです。

ファイル システムもオブジェクトを作成できるコントロール デバイスに注意してください。 ファイル システム フィルター ドライバーは、個々 のファイル システム ボリュームではなく、ファイル システムに自体をアタッチ、するときに、ファイル システムの制御デバイス オブジェクトをアタッチすること自体では。

次の例では、コントロールのデバイス オブジェクトを作成します。

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

ファイル システム フィルター ドライバーは、ファイル システムとは異なり、デバイス オブジェクト、コントロールに名前を付ける必要はありません。 ユーザー モードのアプリケーションへの呼び出しからデバイス名でフィルター ドライバーにアクセスできません[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)はデバイスのコントロール オブジェクトは無効です。 以外の場合**NULL**値が渡された、 *DeviceName*制御デバイス オブジェクトの名前をパラメーターでは、この値になります。 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンを呼び出して、 [ **IoCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff549043)リンク前のコード例で示すように、ルーチンアプリケーションに表示されるユーザー モードの名前に、オブジェクトのカーネル モードの名前。

**注**  ドライバー スタックにアタッチされていない唯一のデバイス オブジェクトのため、コントロールのデバイス オブジェクトが唯一の種類のデバイス オブジェクトを安全に付けることができます。 そのため、ファイル システム フィルター ドライバーのデバイス オブジェクトをコントロール必要に応じて名前を指定できます。 ファイル システムのデバイス オブジェクトをコントロールの指定する必要がありますに注意してください。 デバイス オブジェクトをフィルターを指定しない必要があります。

 

割り当てられている値、 *DeviceType*パラメーターは、ファイルなどの ntifs.h で定義されているデバイスの種類のいずれかを指定する必要があります\_デバイス\_ディスク\_ファイル\_システム。

以外の場合**NULL**値が渡された、 *DeviceName*パラメーター、 *DeviceCharacteristics*フラグは、ファイルを含める必要があります\_デバイス\_セキュリティで保護された\_開きます。 このフラグは、コントロールのデバイス オブジェクトに送信される要求を開いているすべてのセキュリティ チェックを実行する I/O マネージャーに指示します。 名前付きのデバイス オブジェクトの ACL に対しては、これらのセキュリティ チェックが行われました。

ディスパッチ ルーチンで、独自の制御デバイス オブジェクトを識別するためには、ファイル システム フィルター ドライバーの効果的な方法では、デバイスのポインターと制御デバイス オブジェクトを以前に保存されたグローバル ポインターの比較です。 したがって、上記のサンプルが格納、*デバイス オブジェクト*によって返されたポインター [ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)に`gControlDeviceObject`、グローバルに定義されたポインター変数。

 

 




