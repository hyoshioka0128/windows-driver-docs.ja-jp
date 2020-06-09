---
title: hub_info_from_fdo usb3kd
description: Usb3kd コマンドは、USB 3.0 ツリーのハブに関する情報を表示し hub_info_from_fdo ます。
ms.assetid: 07A1C3EC-76A9-49A5-8467-53FCE3667203
keywords:
- usb3kd Windows デバッグの hub_info_from_fdo
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.hub_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 170537d0d6f6d7235bff1905a52b053592852eb0
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534183"
---
# <a name="usb3kdhub_info_from_fdo"></a>! \_ \_ fdo からの usb3kd 情報 \_


**Fdo コマンドからの! \_ usb3kd \_ 情報 \_ **は、 [USB 3.0 ツリー](usb-3-extensions.md#usb-3-tree)のハブに関する情報を表示します。

```dbgcmd
!usb3kd.hub_info_from_fdo DeviceObject
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span>*DeviceObject*   
ハブを表す機能デバイスオブジェクト (FDO) のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="examples"></a>例
--------

FDO のアドレスは、 [**! usb \_ ツリー**](-usb3kd-usb-tree.md)の出力から、または他のさまざまなデバッガーコマンドから取得できます。 たとえば、 [**! devstack**](-devstack.md)コマンドは、FDO のアドレスを表示します。 次の例では、FDO のアドレスは fffffa800597a660 です。

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

これで、FDO のアドレスを** \_ FDO コマンド \_ から \_ ! usb3kd 情報**に渡すことができるようになりました。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! usb3kd \_ 情報**](-usb3kd-hub-info.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






