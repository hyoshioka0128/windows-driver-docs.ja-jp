---
title: usb3kd.xhci_eventring
description: Usb3kd.xhci_eventring 拡張機能では、USB 3.0 ホスト コント ローラーに関連付けられているイベントのリングのデータ構造に関する情報が表示されます。
ms.assetid: D3A40372-5473-48B0-94C7-5D3B80801F16
keywords:
- デバッグ usb3kd.xhci_eventring Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_eventring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6063ee93e56eaf37fa4b16a0819d7108097bd877
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529679"
---
# <a name="usb3kdxhcieventring"></a>!usb3kd.xhci\_eventring


[ **! Usb3kd.xhci\_eventring** ](-usb3kd-device-info.md)拡張機能は、USB 3.0 ホスト コント ローラーに関連付けられているイベント リング データ構造に関する情報を表示します。

```dbgcmd
!usb3kd.xhci_eventring DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
ホスト コント ローラーの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

出力 **! xhci\_eventring**コマンドは、USB 3.0 ホスト コント ローラー ドライバー (UsbXhci.sys) によって管理されるデータ構造に基づきます。 USB 3.0 ホスト コント ローラーのドライバーと USB スタック内の他のドライバーの詳細については、[USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)を参照してください。

イベントのリングは、ドライバー操作が完了したことを通知するために、USB 3.0 ホスト コント ローラーによって使用される構造です。

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
    !xhci_commandring 0xfffffa800536e2d0 (No commands are pending)
    !xhci_deviceslots 0xfffffa800536e2d0
    !xhci_eventring 0xfffffa800536e2d0
    ...
```

デバイスの拡張機能のアドレスを渡すことができますので、 **! xhci\_eventring**コマンド。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






