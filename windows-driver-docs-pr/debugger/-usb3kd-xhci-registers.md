---
title: xhci_registers usb3kd
description: Xhci_registers usb3kd 拡張機能は、USB 3.0 ホストコントローラーの登録を表示します。
ms.assetid: C695C23D-B617-4D1E-87F8-62CF99426CA3
keywords:
- usb3kd Windows デバッグの xhci_registers
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_registers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1956bd608ffa8446f64149bfd502d0b8eafe1cf8
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534889"
---
# <a name="usb3kdxhci_registers"></a>! usb3kd. xhci \_ レジスタ


[**! Usb3kd xhci \_ register**](-usb3kd-device-info.md)拡張機能により、USB 3.0 ホストコントローラーのレジスタが表示されます。

```dbgcmd
!usb3kd.xhci_registers DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
ホストコントローラーの機能デバイスオブジェクト (FDO) のデバイス拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

**! Xhci \_ register**コマンドの出力は、USB 3.0 ホストコントローラードライバー (UsbXhci) によって管理されているデータ構造に基づいています。 Usb 3.0 ホストコントローラードライバーおよび USB スタック内のその他のドライバーの詳細については、「 [Windows の usb ホスト側ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

<a name="examples"></a>例
--------

デバイス拡張機能のアドレスを取得するには、 [**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)コマンドの出力を確認します。 次の例では、デバイス拡張機能のアドレスは0xfffffa800536e2d0 です。

```dbgcmd
3: kd> !xhci_dumpall

## Dumping all the XHCI controllers - DrvObj 0xfffffa80053072f0
------------------------------------------------------------
1)  ... - PCI: VendorId ... DeviceId ... RevisionId ... Firmware ...

    dt USBXHCI!_CONTROLLER_DATA 0xfffffa80052f20c0
    !rcdrlogdump USBXHCI -a 0xfffffa8005068520
    !rcdrlogdump USBXHCI -a 0xfffffa8004e8b9a0 (rundown)
    !wdfdevice 0x57ffac91fd8
    !xhci_capability 0xfffffa800536e2d0
    !xhci_registers 0xfffffa800536e2d0
    ...
```

これで、デバイス拡張機能のアドレスを **! xhci \_ register**コマンドに渡すことができます。

```dbgcmd
3: kd> !xhci_registers 0xfffffa800536e2d0

## Dumping controller registers
----------------------------

    dt USBXHCI!_OPERATIONAL_REGISTERS 0xfffff880046a8020

    DeviceContextBaseAddressArrayPointer: 00000001168b9000

    Command Registers
    -----------------
        RunStopBit: 1
        HostControllerReset: 0
        ...

    Status Registers
    ----------------
        HcHalted: 0
        HostSystemError: 0
        ...

    commandRingControl Registers
    ----------------------------
        RingCycleState: 0
        CommandStop: 0
        ...
    Runtime Registers
    -----------------
        dt USBXHCI!_RUNTIME_REGISTERS 0xfffff880046a8600
        MicroFrameIndex: 0x3f7a

        dt -ba8 USBXHCI!_INTERRUPTER_REGISTER_SET 0xfffff880046a8620

    RootPort Registers
    ------------------
        dt -a4 -r2 USBXHCI!_PORT_REGISTER_SET 0xfffff880046a8420
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






