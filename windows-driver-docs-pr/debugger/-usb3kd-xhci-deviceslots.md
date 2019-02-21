---
title: usb3kd.xhci_deviceslots
description: Usb3kd.xhci_deviceslots 拡張機能には、USB 3.0 ホスト コント ローラーに接続されたデバイスに関する情報が表示されます。
ms.assetid: 471167EA-F7F8-470D-B09C-8627C5BE9566
keywords:
- デバッグ usb3kd.xhci_deviceslots Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_deviceslots
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0ce2c4b1bd84d16f3169c365e79c6389c30e6646
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535815"
---
# <a name="usb3kdxhcideviceslots"></a>! usb3kd.xhci\_deviceslots


[ **! Usb3kd.xhci\_deviceslots** ](-usb3kd-device-info.md)拡張機能は、USB 3.0 ホスト コント ローラーに接続されているデバイスに関する情報を表示します。

```dbgcmd
!usb3kd.xhci_deviceslots DeviceExtension [SlotNumber] [verbose]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
ホスト コント ローラーの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能のアドレス。

<span id="_______SlotNumber______"></span><span id="_______slotnumber______"></span><span id="_______SLOTNUMBER______"></span> *SlotNumber*   
表示するデバイスのスロットの数。 このパラメーターを省略すると、すべてのデバイスが表示されます。

<span id="_______verbose______"></span><span id="_______VERBOSE______"></span> **verbose**   
表示は冗長です。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

出力、 **! xhci\_deviceslots**コマンドは、USB 3.0 ホスト コント ローラー ドライバー (UsbXhci.sys) によって管理されるデータ構造に基づきます。 USB 3.0 ホスト コント ローラーのドライバーと USB スタック内の他のドライバーの詳細については、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)します。

USB 3.0 ホスト コント ローラーのドライバーは、コント ローラーに接続されているデバイスを表すデータ構造体のリストを保持します。 各データ構造体は、スロット番号によって識別されます。

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
    ...
```

デバイスの拡張機能のアドレスを渡すことができますので、 **! usb3kd.xhci\_deviceslots**コマンド。

```dbgcmd
3: kd> !xhci_deviceslots 0xfffffa800536e2d0

## Dumping dt _DEVICESLOT_DATA 0xfffffa8005226220
----------------------------------------------
DeviceContextBase: VA 0xfffffa8005ab9000 LA 0x1168b9000 !wdfcommonbuffer 0x57ffa65c9b8 Size 4096

## [1] SlotID : dt USBXHCI!_USBDEVICE_DATA 0xfffffa8005a427d0 dt _SLOT_CONTEXT32 0xfffffa8005aba000
------------------------------------------------------------------------------------------------
    USB\VID_125F&PID_312A ADATA Technology Co., Ltd.
    SlotEnabled IsDevice NumberOfTTs 0 TTThinkTime 0
    Speed: Super PortPathDepth: 1 PortPath: [ 2 ] DeviceAddress: 1
    !device_info_from_pdo 0xfffffa8005a36800
    DeviceContextBuffer: VA 0xfffffa8005aba000 LA 0x1168ba000 !wdfcommonbuffer 0x57ffa656948 Size 4096
    InputDeviceContextBuffer: VA 0xfffffa8005b65000 LA 0x116965000 !wdfcommonbuffer 0x57ffa5be958 Size 4096

    [1] DeviceContextIndex : dt USBXHCI!_ENDPOINT_DATA 0xfffffa8005a126f0 dt _ENDPOINT_CONTEXT32 0xfffffa8005aba020 ES_RUNNING
    --------------------------------------------------------------------------------------------------------------
        EndpointType_Control Address: 0x0 PacketSize: 512 Interval: 0
        !ucx_endpoint 0xfffffa8005a3f710
        RecorderLog: !rcdrlogdump USBXHCI -a 0xfffffa8005b60010

        [0] dt _TRANSFERRING_DATA 0xfffffa8005b64ec0 Events: 0x0 TransferRingState_Idle
     ...

## [2] SlotID : dt USBXHCI!_USBDEVICE_DATA 0xfffffa80052de320 dt _SLOT_CONTEXT32 0xfffffa8005b8b000
------------------------------------------------------------------------------------------------
    USB\VID_18A5&PID_0304 Verbatim Americas LLC
    SlotEnabled IsDevice NumberOfTTs 0 TTThinkTime 0
    Speed: High PortPathDepth: 1 PortPath: [ 3 ] DeviceAddress: 2
    !device_info_from_pdo 0xfffffa80058fb800
    DeviceContextBuffer: VA 0xfffffa8005b8b000 LA 0x11698b000 !wdfcommonbuffer 0x57ffa426b18 Size 4096
    InputDeviceContextBuffer: VA 0xfffffa8005b8c000 LA 0x11698c000 !wdfcommonbuffer 0x57ffadbe3c8 Size 4096

    [1] DeviceContextIndex : dt USBXHCI!_ENDPOINT_DATA 0xfffffa800714b050 dt _ENDPOINT_CONTEXT32 0xfffffa8005b8b020 ES_RUNNING
    --------------------------------------------------------------------------------------------------------------
        EndpointType_Control Address: 0x0 PacketSize: 64 Interval: 0
        !ucx_endpoint 0xfffffa80036a20c0
        RecorderLog: !rcdrlogdump USBXHCI -a 0xfffffa8005bd0b60

        [0] dt _TRANSFERRING_DATA 0xfffffa8004ed8df0 Events: 0x0 TransferRingState_Idle
        ------------------------------------------------------------------------------
    ...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






