---
title: usb3kd.xhci_info
description: Usb3kd.xhci_info 拡張機能では、個々 の USB 3.0 ホスト コント ローラーのすべての XHCI コマンドが表示されます。
ms.assetid: C3C3B379-4871-4293-9C35-B64F3A5E1348
keywords:
- usb3kd.xhci_info Windows Debugging
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a2c15b15393d1eeca1045222e89884f00edf1feb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335634"
---
# <a name="usb3kdxhciinfo"></a>!usb3kd.xhci\_info


[ **! Usb3kd.xhci\_情報**](-usb3kd-device-info.md)拡張機能には、個々 の USB 3.0 ホスト コント ローラーのすべての XHCI コマンドが表示されます。

```dbgcmd
!usb3kd.xhci_info DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
ホスト コント ローラーの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

出力、 **! usb3kd.xhci\_情報**コマンドは、USB 3.0 ホスト コント ローラー ドライバー (UsbXhci.sys) によって管理されるデータ構造に基づきます。 USB 3.0 ホスト コント ローラーのドライバーと USB スタック内の他のドライバーの詳細については、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)します。

<a name="examples"></a>例
--------

デバイスの拡張機能のアドレスを取得することができます、 [ **! xhci\_dumpall** ](-usb3kd-xhci-dumpall.md)コマンドまたはさまざまな他のデバッガー コマンド。 たとえば、 [ **! devstack** ](-devstack.md)コマンドは、デバイスの拡張機能のアドレスを表示します。 次の例では、ホスト コント ローラーの FDO のデバイスの拡張機能のアドレスは、fffffa800536e2d0 です。

```dbgcmd
3: kd> !devnode 0 1 usbxhci
Dumping IopRootDeviceNode (= 0xfffffa8003609cc0)
DevNode 0xfffffa8003df3010 for PDO 0xfffffa8003dd5870
  InstancePath is "PCI\VEN_...
  ServiceName is "USBXHCI"
  ...

3: kd> !devstack 0xfffffa8003dd5870
  !DevObj   !DrvObj            !DevExt   ObjectName
  fffffa800534b060  \Driver\USBXHCI    fffffa800536e2d0  USBFDO-3
  fffffa8003db5790  \Driver\ACPI       fffffa8003701cb0  
> fffffa8003dd5870  \Driver\pci        fffffa8003dd59c0  NTPNP_PCI0020
...
```

デバイスの拡張機能のアドレスを渡すことができますので、 **! xhci\_情報**コマンド。

```dbgcmd
3: kd> !xhci_info 0xfffffa80`0536e2d0

## Dumping XHCI controller commands - DeviceExtension 0xfffffa800536e2d0
------------------------------------------------------------
 ... - PCI: VendorId ... DeviceId ... RevisionId ... Firmware ...

    dt USBXHCI!_CONTROLLER_DATA 0xfffffa80052f20c0
    !rcdrlogdump USBXHCI -a 0xfffffa8005068520
    !rcdrlogdump USBXHCI -a 0xfffffa8004e8b9a0 (rundown)
    !wdfdevice 0x57ffac91fd8
    !xhci_capability 0xfffffa800536e2d0
    !xhci_registers 0xfffffa800536e2d0
    !xhci_commandring 0xfffffa800536e2d0 (No commands are pending)
    !xhci_deviceslots 0xfffffa800536e2d0
    !xhci_eventring 0xfffffa800536e2d0
    !xhci_resourceusage 0xfffffa800536e2d0
    !pci 100 0x30 0x0 0x0
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






