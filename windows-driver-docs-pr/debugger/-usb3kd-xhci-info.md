---
title: xhci_info usb3kd
description: Usb3kd 拡張子は、個々の USB 3.0 ホストコントローラーのすべての XHCI コマンドを表示し xhci_info ます。
ms.assetid: C3C3B379-4871-4293-9C35-B64F3A5E1348
keywords:
- usb3kd Windows デバッグの xhci_info
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1def7d692ba420c23fe1194b835962c58ac425d6
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534113"
---
# <a name="usb3kdxhci_info"></a>! usb3kd. xhci \_ info


[**! Usb3kd xhci \_ info**](-usb3kd-device-info.md)拡張機能により、個々の USB 3.0 ホストコントローラーのすべての xhci コマンドが表示されます。

```dbgcmd
!usb3kd.xhci_info DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
ホストコントローラーの機能デバイスオブジェクト (FDO) のデバイス拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

**Xhci \_ info**コマンドの出力は、USB 3.0 ホストコントローラードライバー (UsbXhci) によって管理されているデータ構造に基づいています。 Usb 3.0 ホストコントローラードライバーおよび USB スタック内のその他のドライバーの詳細については、「 [Windows の usb ホスト側ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

<a name="examples"></a>例
--------

デバイス拡張機能のアドレスは、 [**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)コマンドから、または他のさまざまなデバッガーコマンドから取得できます。 たとえば、 [**! devstack**](-devstack.md)コマンドは、デバイス拡張機能のアドレスを表示します。 次の例では、ホストコントローラーの FDO のデバイス拡張機能のアドレスが fffffa800536e2d0 です。

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

これで、デバイス拡張機能のアドレスを **! xhci \_ info**コマンドに渡すことができます。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






