---
title: xhci_deviceslots usb3kd
description: Xhci_deviceslots usb3kd 拡張機能には、USB 3.0 ホストコントローラーに接続されているデバイスに関する情報が表示されます。
ms.assetid: 471167EA-F7F8-470D-B09C-8627C5BE9566
keywords:
- usb3kd Windows デバッグの xhci_deviceslots
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_deviceslots
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 098d97a4f07301b7962c66376e4f80bf74bdee24
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534123"
---
# <a name="usb3kdxhci_deviceslots"></a>! usb3kd. xhci の大 \_ 多数のデバイス


[**! Usb3kd xhci \_ **](-usb3kd-device-info.md)は、USB 3.0 ホストコントローラーに接続されているデバイスに関する情報を表示します。

```dbgcmd
!usb3kd.xhci_deviceslots DeviceExtension [SlotNumber] [verbose]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
ホストコントローラーの機能デバイスオブジェクト (FDO) のデバイス拡張機能のアドレス。

<span id="_______SlotNumber______"></span><span id="_______slotnumber______"></span><span id="_______SLOTNUMBER______"></span>*SlotNumber*   
表示されるデバイスのスロット番号。 このパラメーターを省略すると、すべてのデバイスが表示されます。

<span id="_______verbose______"></span><span id="_______VERBOSE______"></span>**詳細**   
表示は verbose です。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

出力の **! xhci は \_ ** 、USB 3.0 ホストコントローラードライバー (UsbXhci) によって管理されているデータ構造に基づいています。 Usb 3.0 ホストコントローラードライバーおよび USB スタック内のその他のドライバーの詳細については、「 [Usb ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

USB 3.0 ホストコントローラードライバーは、コントローラーに接続されているデバイスを表すデータ構造の一覧を保持します。 これらの各データ構造体は、スロット番号によって識別されます。

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
    ...
```

これで、デバイス拡張機能のアドレスを **! usb3kd. xhci デバイス \_ ロット**コマンドに渡すことができます。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






