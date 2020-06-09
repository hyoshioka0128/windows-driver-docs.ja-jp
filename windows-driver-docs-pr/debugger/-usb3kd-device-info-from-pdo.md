---
title: device_info_from_pdo usb3kd
description: Device_info_from_pdo usb3kd コマンドは、usb 3.0 ツリーの USB デバイスに関する情報を表示します。
ms.assetid: 74FD68E6-78DF-452F-80C2-91A37877DE52
keywords:
- usb3kd Windows デバッグの device_info_from_pdo
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.device_info_from_pdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 645fe27ebbe8557f54c763e878eda1b71f747a12
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534905"
---
# <a name="usb3kddevice_info_from_pdo"></a>! usb3kd \_ \_ pdo からのデバイス \_ 情報


[ **Usb3kd \_ info \_ from \_ pdo** ] コマンドを実行すると、usb デバイスに関する情報が[usb 3.0 ツリー](usb-3-extensions.md#usb-3-tree)に表示されます。

```dbgcmd
!usb3kd.device_info_from_pdo DeviceObject
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span>*DeviceObject*   
USB デバイスまたはハブの物理デバイスオブジェクト (PDO) のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

! pdo および[**! ucx \_ デバイス**](-usb3kd-ucx-device.md) ** \_ \_ からの \_ デバイス情報**はどちらもデバイスに関する情報を表示しますが、表示される情報は異なります。 ** \_ \_ \_ P から**の出力は、usb 3.0 ハブドライバーの観点から見たものであり、 **! UCX \_ デバイス**の出力は、usb ホストコントローラー拡張機能ドライバーの観点からのものです。 たとえば、 ** \_ \_ \_ pdo からのデバイス情報**には、構成記述子とインターフェイス記述子に関する情報が含まれています。また、 **! ucx \_ デバイス**の出力には、エンドポイントに関する情報が含まれています。

<a name="examples"></a>例
--------

P のアドレスは、 [**! usb \_ ツリー**](-usb3kd-usb-tree.md)の出力、または他のさまざまなデバッガーコマンドから取得できます。 たとえば、 [**! devnode**](-devnode.md)コマンドを実行すると、pdos のアドレスが表示されます。 次の例では、USBSTOR.SYS device ノードが USBHUB3 ノードの直接の子になります。 USBSTOR.SYS ノードの PDO のアドレスは、0xfffffa80059c3800 です。

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

Pdo のアドレスを、 ** \_ pdo コマンド \_ から \_ の! usb3kd info**に渡すことができるようになりました。

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

次の例は、 [**! usb \_ ツリー**](-usb3kd-usb-tree.md)コマンドの出力の一部を示しています。 子デバイスノードのいずれかの PDO のアドレスは、 [**! devstack**](-devstack.md)コマンドの引数として確認できます。 (**! devstack fffffa80059c3800**)

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! usb3kd. デバイス \_ 情報**](-usb3kd-device-info.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






