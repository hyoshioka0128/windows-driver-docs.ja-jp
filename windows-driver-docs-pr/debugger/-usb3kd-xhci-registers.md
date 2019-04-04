---
title: usb3kd.xhci_registers
description: Usb3kd.xhci_registers 拡張機能には、USB 3.0 ホスト コント ローラーのレジスタが表示されます。
ms.assetid: C695C23D-B617-4D1E-87F8-62CF99426CA3
keywords:
- デバッグ usb3kd.xhci_registers Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_registers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 47fdb22af1a2a6e18a908bce158f9c2619e407b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537811"
---
# <a name="usb3kdxhciregisters"></a>! usb3kd.xhci\_を登録します


[ **! Usb3kd.xhci\_登録**](-usb3kd-device-info.md)拡張機能には、USB 3.0 ホスト コント ローラーのレジスタが表示されます。

```dbgcmd
!usb3kd.xhci_registers DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
ホスト コント ローラーの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

出力、 **! xhci\_登録**コマンドは、USB 3.0 ホスト コント ローラー ドライバー (UsbXhci.sys) によって管理されるデータ構造に基づきます。 USB 3.0 ホスト コント ローラーのドライバーと USB スタック内の他のドライバーの詳細については、[USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)を参照してください。

<a name="examples"></a>例
--------

デバイス拡張機能のアドレスを取得する出力の確認、 [ **! xhci\_dumpall** ](-usb3kd-xhci-dumpall.md)コマンド。 次の例では、デバイスの拡張機能のアドレスは、0xfffffa800536e2d0 です。

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

デバイスの拡張機能のアドレスを渡すことができますので、 **! xhci\_登録**コマンド。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






