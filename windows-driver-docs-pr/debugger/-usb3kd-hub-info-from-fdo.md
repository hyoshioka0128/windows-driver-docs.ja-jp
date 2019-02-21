---
title: usb3kd.hub_info_from_fdo
description: Usb3kd.hub_info_from_fdo コマンドでは、USB 3.0 ツリー内のハブに関する情報が表示されます。
ms.assetid: 07A1C3EC-76A9-49A5-8467-53FCE3667203
keywords:
- デバッグ usb3kd.hub_info_from_fdo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.hub_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0932f332e22ec602b0860685b0ea443f711a5e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530208"
---
# <a name="usb3kdhubinfofromfdo"></a>!usb3kd.hub\_info\_from\_fdo


**! Usb3kd.hub\_情報\_から\_fdo**コマンド内のハブに関する情報を表示、 [USB 3.0 ツリー](usb-3-extensions.md#usb-3-tree)します。

```dbgcmd
!usb3kd.hub_info_from_fdo DeviceObject
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
機能のデバイス (FDO) を表すオブジェクトをハブのアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="examples"></a>例
--------

出力から、FDO のアドレスを取得できる[ **! usb\_ツリー** ](-usb3kd-usb-tree.md)またはその他のデバッガー コマンドのさまざまな。 たとえば、 [ **! devstack** ](-devstack.md)コマンド、FDO のアドレスを表示します。 次の例では、FDO のアドレスは、fffffa800597a660 です。

```dbgcmd
3: kd> !devnode 0 1 usbhub3
Dumping IopRootDeviceNode (= 0xfffffa8003609cc0)
DevNode 0xfffffa8005981730 for PDO 0xfffffa8004ffc550
...
3: kd> !devstack 0xfffffa8004ffc550
  !DevObj   !DrvObj            !DevExt   ObjectName
  fffffa800597a660  \Driver\USBHUB3    fffffa8005ad92d0  
> fffffa8004ffc550  \Driver\USBXHCI    fffffa8005251d00  USBPDO-0
...
```

FDO のアドレスを渡すことができますので、 **! usb3kd.hub\_情報\_から\_fdo**コマンド。

```dbgcmd
 3: kd> !hub_info_from_fdo fffffa800597a660

## Dumping HUB Information fffffa800597a660
----------------------------------------
dt USBHUB3!_HUB_FDO_CONTEXT 0xfffffa8005ad92d0
!rcdrlogdump usbhub3 -a 0xfffffa8005ad8010
Capabilities: Initialized, Configured, HasOverCurrentProtection, SelectiveSuspendSupportedByParentStack, CannotWakeOnConnect, NotArmedForWake

Total number of ports: 4, HUB depth is 0
Number of 3.0 ports: 2 (Range 1 - 2)
Number of 2.0 ports: 2 (Range 3 - 4)

Descriptors:
    dt _USB_HUB_DESCRIPTOR 0xfffffa8005ad9728
    dt _USB_30_HUB_DESCRIPTOR 0xfffffa8005ad9728
    dt _USB_DEVICE_DESCRIPTOR 0xfffffa8005ad92d0
    dt _USB_CONFIGURATION_DESCRIPTOR 0xfffffa8005ad9770

List of PortContext: 4
    [1] !port_info 0xfffffa8005a5ca80    !device_info 0xfffffa8005b410c0
            Last Port Status(2.0): Connected Enabled Powered HighSpeedDeviceAttached
            Last Port Change: <none>
            Current Port(2.0) State: ConnectedEnabled.WaitingForPortChangeEvent
            Current Device State: ConfiguredInD0
         ...

Current Hub State: ConfiguredWithIntTransfer

Hub State History: <Event> NewState (<Operation>(),..) :

    [43] <OperationSuccess> ConfiguredWithIntTransfer 
    ...

Hub Event History:
    [ 0] PortEnableInterruptTransfer
    ...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**!usb3kd.hub\_info**](-usb3kd-hub-info.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






