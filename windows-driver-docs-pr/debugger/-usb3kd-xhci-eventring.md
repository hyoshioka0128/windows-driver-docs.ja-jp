---
title: xhci_eventring usb3kd
description: Xhci_eventring usb3kd 拡張機能は、USB 3.0 ホストコントローラーに関連付けられているイベントリングデータ構造に関する情報を表示します。
ms.assetid: D3A40372-5473-48B0-94C7-5D3B80801F16
keywords:
- usb3kd Windows デバッグの xhci_eventring
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_eventring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 372a6fc85dfa9dae5333386fab515765e02fcf2d
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534115"
---
# <a name="usb3kdxhci_eventring"></a>! usb3kd. xhci \_ eventring


[**Xhci \_ eventring**](-usb3kd-device-info.md)拡張機能には、USB 3.0 ホストコントローラーに関連付けられているイベントリングデータ構造に関する情報が表示されます。

```dbgcmd
!usb3kd.xhci_eventring DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
ホストコントローラーの機能デバイスオブジェクト (FDO) のデバイス拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

Output **! xhci \_ eventring**コマンドは、USB 3.0 ホストコントローラードライバー (UsbXhci) によって管理されているデータ構造に基づいています。 Usb 3.0 ホストコントローラードライバーおよび USB スタック内のその他のドライバーの詳細については、「 [Windows の usb ホスト側ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

イベントリングは、アクションが完了したことをドライバーに通知するために USB 3.0 ホストコントローラーによって使用される構造体です。

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
    !xhci_deviceslots 0xfffffa800536e2d0
    !xhci_eventring 0xfffffa800536e2d0
    ...
```

これで、デバイス拡張機能のアドレスを **! xhci \_ eventring**コマンドに渡すことができます。

```dbgcmd
3: kd> !xhci_eventring 0xfffffa800536e2d0

## Dumping dt _PRIMARY_INTERRUPTER_DATA fffffa800536b5b0
-----------------------------------------------------

## [0] Interrupter : dt _INTERRUPTER_DATA 0xfffffa800536b7d0  !rcdrlogdump USBXHCI -a 0xfffffa8005aeab60
------------------------------------------------------------------------------------------------------
    DequeueSegment: 1 DequeueIndex: 217 TotalEventRingSegments: 2 TRBsPerSegment: 256
    CurrentBufferData : VA 0xfffffa8005373000 LA 0x117173000 !wdfcommonbuffer 0x57ffa65b9b8 Size 4096
    EventRingTableBufferData : VA 0xfffffa8005aeb000 LA 0x1168eb000 !wdfcommonbuffer 0x57ffa65d988 Size 512

    [0] VA 0xfffffa8005370000 LA 0x117170000 !wdfcommonbuffer 0x57ffa6599b8 Size 4096
    [1] VA 0xfffffa8005373000 LA 0x117173000 !wdfcommonbuffer 0x57ffa65b9b8 Size 4096

    Event Ring TRBs:
        [207] TRANSFER_EVENT      0xfffffa8005373cf0 CycleBit 0 SlotId  2 EndpointID  4 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [208] TRANSFER_EVENT      0xfffffa8005373d00 CycleBit 0 SlotId  2 EndpointID  3 EventData 1 Pointer 0xfffffa8005a3d850 CC_SHORT_PACKET
        [209] TRANSFER_EVENT      0xfffffa8005373d10 CycleBit 0 SlotId  1 EndpointID  4 EventData 1 Pointer 0xfffffa8005a3d850 CC_SUCCESS
        [210] TRANSFER_EVENT      0xfffffa8005373d20 CycleBit 0 SlotId  1 EndpointID  3 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [211] TRANSFER_EVENT      0xfffffa8005373d30 CycleBit 0 SlotId  2 EndpointID  4 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [212] TRANSFER_EVENT      0xfffffa8005373d40 CycleBit 0 SlotId  2 EndpointID  3 EventData 1 Pointer 0xfffffa8005a3d850 CC_SHORT_PACKET
        [213] TRANSFER_EVENT      0xfffffa8005373d50 CycleBit 0 SlotId  1 EndpointID  4 EventData 1 Pointer 0xfffffa8005a3d850 CC_SUCCESS
        [214] TRANSFER_EVENT      0xfffffa8005373d60 CycleBit 0 SlotId  1 EndpointID  3 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [215] TRANSFER_EVENT      0xfffffa8005373d70 CycleBit 0 SlotId  2 EndpointID  4 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [216] TRANSFER_EVENT      0xfffffa8005373d80 CycleBit 0 SlotId  2 EndpointID  3 EventData 1 Pointer 0xfffffa8005a3d850 CC_SHORT_PACKET
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






