---
title: xhci_commandring usb3kd
description: Xhci_commandring usb3kd 拡張機能は、USB 3.0 ホストコントローラーに関連付けられているコマンドリングデータ構造に関する情報を表示します。
ms.assetid: 3099F3F1-B881-4BBD-90F5-59DC2DFECF3B
keywords:
- usb3kd Windows デバッグの xhci_commandring
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_commandring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a7abf79b9d58000e76d36f0a5aea5bb657d569b3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534895"
---
# <a name="usb3kdxhci_commandring"></a>! usb3kd \_ . xhci


[**! Usb3kd xhci \_ **](-usb3kd-device-info.md)には、USB 3.0 ホストコントローラーに関連付けられているコマンドリングデータ構造に関する情報が表示されます。

```dbgcmd
!usb3kd.xhci_commandring DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
ホストコントローラーの機能デバイスオブジェクト (FDO) のデバイス拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

**! Xhci \_ **コマンドの出力は、USB 3.0 ホストコントローラードライバー (UsbXhci) によって管理されているデータ構造に基づいています。 Usb 3.0 ホストコントローラードライバーおよび USB スタック内のその他のドライバーの詳細については、「 [Usb ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

コマンドリングは、ホストコントローラーにコマンドを渡すために USB 3.0 ホストコントローラードライバーによって使用されるデータ構造です。

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
    !xhci_commandring 0xfffffa800536e2d0 (No commands are pending)
    ...
```

これで、デバイス拡張機能のアドレスを **! xhci \_ **コマンドに渡すことができます。

```dbgcmd
3: kd> !xhci_commandring 0xfffffa800536e2d0

## Dumping dt _COMMAND_DATA 0xfffffa8005362f70 !rcdrlogdump USBXHCI -a 0xfffffa8005a8f010
-------------------------------------------------------------------------------------
Stop: OFF Abort: OFF Running: ON
CommandRingBufferData: VA 0xfffffa8005aeb200 LA 0x1168eb200 !wdfcommonbuffer 0x57ffa65d988 Size 512
DequeueIndex: 24 EnqueueIndex: 24 CycleState: 0

    Command Ring TRBs:
        [  0] Unknown TRB Type 49 0xfffffa8005aeb200

        [  1] ENABLE_SLOT                 0xfffffa8005aeb210 CycleBit 1
        [  2] ADDRESS_DEVICE              0xfffffa8005aeb220 CycleBit 1 SlotId  1 BlockSetAddressRequest 1
        ...

    PendingList:
        Empty List

    WaitingList:
        Empty List
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






