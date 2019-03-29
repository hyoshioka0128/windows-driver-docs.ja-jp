---
title: usb3kd.hub_info
description: Usb3kd.device_info コマンドでは、USB 3.0 ツリー内のハブに関する情報が表示されます。
ms.assetid: B46B48C1-C14A-410D-9C34-F8AB1640682C
keywords:
- デバッグ usb3kd.hub_info Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.hub_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 399a35aeaee39f782bc7e0b1fc19ac62c91d2d9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578131"
---
# <a name="usb3kdhubinfo"></a>!usb3kd.hub\_info


[ **! Usb3kd.device\_情報**](-usb3kd-device-info.md)コマンド内のハブに関する情報を表示、 [USB 3.0 ツリー](usb-3-extensions.md#usb-3-tree)します。

```dbgcmd
!usb3kd.hub_info DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
ハブの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="examples"></a>使用例
--------

デバイス拡張機能のアドレスを取得する出力の確認、 [ **! usb\_ツリー** ](-usb3kd-usb-tree.md)コマンド。 次の例では、ルート ハブにデバイスの拡張機能のアドレスは、0xfffffa8005ad92d0 です。

```dbgcmd
3: kd> !usb_tree

## Dumping HUB Tree - !drvObj 0xfffffa800597f770
--------------------------------------------
Topology
--------
1)  !xhci_info 0xfffffa80051d1940  ... - PCI: VendorId 0x1033 ...
    !hub_info 0xfffffa8005ad92d0 (ROOT)
        !port_info 0xfffffa8005a5ca80 !device_info 0xfffffa8005b410c0 Desc: <none> Speed: High
        ...
```

デバイスの拡張機能のアドレスを渡すことができますので、 **! ハブ\_情報**コマンド。

```dbgcmd
3: kd> !hub_info fffffa8005ad92d0 

## Dumping HUB Information fffffa8005ad92d0
----------------------------------------
dt USBHUB3!_HUB_FDO_CONTEXT 0xfffffa8005ad92d0
!rcdrlogdump usbhub3 -a 0xfffffa8005ad8010
Capabilities: Initialized, Configured, HasOverCurrentProtection, ...

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

[**!usb3kd.hub\_info\_from\_fdo**](-usb3kd-hub-info-from-fdo.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






