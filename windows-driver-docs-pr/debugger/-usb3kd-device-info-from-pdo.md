---
title: usb3kd.device_info_from_pdo
description: Usb3kd.device_info_from_pdo コマンドでは、USB 3.0 ツリーの中に USB デバイスに関する情報が表示されます。
ms.assetid: 74FD68E6-78DF-452F-80C2-91A37877DE52
keywords:
- デバッグ usb3kd.device_info_from_pdo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.device_info_from_pdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 48e5d06b96c0dc41678c9fc30f8c11a7e2d71016
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334141"
---
# <a name="usb3kddeviceinfofrompdo"></a>! usb3kd.device\_情報\_から\_pdo


**! Usb3kd.device\_情報\_から\_pdo**コマンドで USB デバイスに関する情報を表示、 [USB 3.0 ツリー](usb-3-extensions.md#usb-3-tree)します。

```dbgcmd
!usb3kd.device_info_from_pdo DeviceObject
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
USB デバイスまたはハブの物理デバイス オブジェクト (PDO) のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

**! デバイス\_情報\_から\_pdo**と[ **! ucx\_デバイス**](-usb3kd-ucx-device.md)デバイスに関する情報、情報が両方表示表示が異なります。 出力 **! デバイス\_情報\_から\_pdo**は USB 3.0 ハブのドライバーの point of view およびの出力から **! ucx\_デバイス**からは、USB ホスト コント ローラーの拡張機能ドライバーのポイントのビュー。 たとえば、 **! デバイス\_情報\_から\_pdo**出力には、構成と記述子にはインターフェイスに関する情報が含まれていますと **! ucx\_デバイス。** 出力にはエンドポイントに関する情報が含まれています。

<a name="examples"></a>例
--------

出力から、PDO のアドレスを取得できる[ **! usb\_ツリー** ](-usb3kd-usb-tree.md)またはその他のデバッガー コマンドのさまざまな。 たとえば、 [ **! devnode** ](-devnode.md)コマンドは、Pdo のアドレスを表示します。 次の例では、USBSTOR デバイス ノードは、USBHUB3 ノードの直接の子が。 PDO USBSTOR ノードのアドレスは、0xfffffa80059c3800 です。

```dbgcmd
3: kd> !devnode 0 1 usbhub3

Dumping IopRootDeviceNode (= 0xfffffa8003609cc0)
DevNode 0xfffffa8005981730 for PDO 0xfffffa8004ffc550
  InstancePath is "USB\ROOT_HUB30\5&11db9684&0&0"
  ServiceName is "USBHUB3"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)

  DevNode 0xfffffa8005a546a0 for PDO 0xfffffa80059c3800
    InstancePath is "USB\VID_125F&PID_312A\09021000000000000342192873"
    ServiceName is "USBSTOR"
    State = DeviceNodeStarted (0x308)
    Previous State = DeviceNodeEnumerateCompletion (0x30d)

    DevNode 0xfffffa8005a09730 for PDO 0xfffffa8005b3a650
      InstancePath is "USBSTOR\Disk&Ven ...
      ServiceName is "disk"
      State = DeviceNodeStarted (0x308)
      Previous State = DeviceNodeEnumerateCompletion (0x30d)
```

PDO のアドレスを渡すことができますので、 **! usb3kd.device\_情報\_から\_pdo**コマンド。

```dbgcmd
3: kd> !device_info_from_pdo 0xfffffa80059c3800

## Dumping Device Information fffffa80059c3800
-------------------------------------------
!devobj 0xfffffa8004ffc550 (Root HUB)
!device_info 0xfffffa8005abd0c0 (dt usbhub3!_DEVICE_CONTEXT 0xfffffa8005abd0c0)
dt USBHUB3!_DEVICE_CONTEXT 0xfffffa8005abd0c0
dt USBHUB3!_HUB_PDO_CONTEXT 0xfffffa8005b118d0
!idle_info 0xfffffa8005b11920 (dt USBHUB3!_ISM_CONTEXT 0xfffffa8005b11920)
Parent !hub_info 0xfffffa8005ad92d0 (dt USBHUB3!_HUB_FDO_CONTEXT 0xfffffa8005ad92d0)
!port_info 0xfffffa8005abe0c0 (dt USBHUB3!_PORT_CONTEXT 0xfffffa8005abe0c0)
!ucx_device 0xfffffa8005992840 !xhci_deviceslots 0xfffffa80051d1940 1

LPMState: U1IsEnabledForUpStreamPort U2IsEnabledForUpStreamPort U1Timeout: 38, U2Timeout: 3
DeviceFlags: HasContainerId NoBOSContainerId Removable HasSerialNumber MsOsDescriptorNotSupported NoWakeUpSupport DeviceIsSuperSpeedCapable 
DeviceHackFlags: WillDisableOnSoftRemove SkipSetIsochDelay WillResetOnResumeS0 DisableOnSoftRemove 

Descriptors:
dt _USB_CONFIGURATION_DESCRIPTOR 0xfffffa80053f9250
dt _USB_INTERFACE_DESCRIPTOR 0xfffffa80053f9259
ProductId: ...
DeviceDescriptor: VID ...

UcxRequest: !wdfrequest 0x57ffa662948, 
ControlRequest: !wdfrequest 0x57ffa667798, !irp 0xfffffa8005997650 !urb 0xfffffa8005abd1c0, NumberOfBytes 0
Device working at SuperSpeed
Current Device State: ConfiguredInD0

Device State History: <Event> NewState (<Operation>(),..) :

    [16] <Yes> ConfiguredInD0 
    ...
Device Event History:
    [10] TransferSuccess
    ...
```

次の例は、出力の一部、 [ **! usb\_ツリー** ](-usb3kd-usb-tree.md)コマンド。 引数としてデバイスの子ノードのいずれかの PDO のアドレスを参照することができます、 [ **! devstack** ](-devstack.md)コマンド。 (**! devstack fffffa80059c3800**)

```dbgcmd
3: kd> !usb_tree

## Dumping HUB Tree - !drvObj 0xfffffa800597f770
--------------------------------------------

Topology
--------
1)  !xhci_info 0xfffffa80051d1940  ... - PCI: VendorId ...
    !hub_info 0xfffffa8005ad92d0 (ROOT)
        !port_info 0xfffffa8005a5ca80 !device_info 0xfffffa8005b410c0 Desc: <none> Speed: High
        ...
## Enumerated Device List
----------------------
...

2) !device_info 0xfffffa8005abd0c0, !devstack fffffa80059c3800
    Current Device State: ConfiguredInD0
    Desc: ... Flash Drive
    USB\VID_...
    !ucx_device 0xfffffa8005992840 !xhci_deviceslots 0xfffffa80051d1940 1
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! usb3kd.device\_情報**](-usb3kd-device-info.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






