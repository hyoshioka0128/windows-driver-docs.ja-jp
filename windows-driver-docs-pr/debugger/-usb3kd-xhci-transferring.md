---
title: xhci_transferring usb3kd
description: Xhci_transferring usb3kd 拡張機能は、サイクルビットの変更が検出されるまで、(USB 3.0 ホストコントローラーによって使用される) 転送リングを表示します。
ms.assetid: BCF6DEF0-FB58-4FE6-88AD-BF778E00F052
keywords:
- usb3kd Windows デバッグの xhci_transferring
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_transferring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3875fa7074ee6f8296fe14fa35ac54f5b31a3516
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534887"
---
# <a name="usb3kdxhci_transferring"></a>! usb3kd. xhci \_ 転送


[**Xhci \_ 転送**](-usb3kd-device-info.md)拡張機能は、サイクルビットの変更が検出されるまで、USB 3.0 ホストコントローラーによって使用される転送リングを表示します。

```dbgcmd
!usb3kd.xhci_transferring VirtualAddress
!usb3kd.xhci_transferring PhysicalAddress 1
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span>*Virtualaddress*   
転送リングの仮想アドレス。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span>*PhysicalAddress*   
転送リングの物理アドレス。

<span id="_______1______"></span>1   
アドレスが物理アドレスであることを指定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

**! Xhci の \_ 転送**コマンドの出力は、USB 3.0 ホストコントローラードライバー (UsbXhci) によって管理されているデータ構造に基づいています。 Usb 3.0 ホストコントローラードライバーおよび USB スタック内のその他のドライバーの詳細については、「 [Windows の usb ホスト側ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

転送リングは、転送要求ブロック (TRBs) の一覧を維持するために USB 3.0 ホストコントローラードライバーによって使用される構造体です。 このコマンドは、転送リングの仮想アドレスまたは物理アドレスを受け取りますが、その物理アドレスを表示します。 これは、コマンドがリンクを正しくスキャンできるようにするためです。

<a name="examples"></a>例
--------

転送リングのアドレスを取得するには、 [**! xhci \_ デバイスロット**](-usb3kd-xhci-deviceslots.md)コマンドの出力を確認します。 次の例では、転送リングの仮想アドレスは0xfffffa8005b2fe00 です。

```dbgcmd
3: kd> !usb3kd.xhci_deviceslots 0xfffffa800523a2d0

## Dumping dt _DEVICESLOT_DATA 0xfffffa80051a3300
----------------------------------------------
DeviceContextBase: VA 0xfffffa8005a41000 LA 0x116841000 !wdfcommonbuffer 0x57ffa6ff9b8 Size 4096

## [1] SlotID : dt USBXHCI!_USBDEVICE_DATA 0xfffffa800598c7d0 dt _SLOT_CONTEXT32 0xfffffa8005a42000
------------------------------------------------------------------------------------------------
    USB\VID_125F&PID_312A ADATA Technology Co., Ltd.
    SlotEnabled IsDevice NumberOfTTs 0 TTThinkTime 0
    Speed: Super PortPathDepth: 1 PortPath: [ 2 ] DeviceAddress: 1
    !device_info_from_pdo 0xfffffa800597d720
    DeviceContextBuffer: VA 0xfffffa8005a42000 LA 0x116842000 !wdfcommonbuffer 0x57ffa7009b8 Size 4096
    InputDeviceContextBuffer: VA 0xfffffa8005b2d000 LA 0x11692d000 !wdfcommonbuffer 0x57ffa674958 Size 4096
    ...

    [3] DeviceContextIndex : dt USBXHCI!_ENDPOINT_DATA 0xfffffa8005b394e0 dt _ENDPOINT_CONTEXT32 0xfffffa8005a42060 ES_RUNNING
    --------------------------------------------------------------------------------------------------------------
       ...
            CurrentRingBufferData: VA 0xfffffa8005b2fe00 LA 0x11692fe00 !wdfcommonbuffer 0x57ffa67c988 Size 512
            Current:  !xhci_transferring 0xfffffa8005b2fe00
            PendingTransferList: 
                [0] dt _TRANSFER_DATA 0xfffffa8005b961b0 !urb 0xfffffa8005b52be8 !wdfrequest 0x57ffa469fd8 TransferState_Pending
```

これで、転送リングのアドレスを **! xhci \_ ** transfer コマンドに渡すことができます。

```dbgcmd
kd> !xhci_transferring 0xfffffa8005b2fe00

        [  0] NORMAL       0x000000011692fe00 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 0 TransferLength    13 TDSize  0
        [  1] EVENT_DATA   0x000000011692fe10 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 0 Data  0 0xfffffa8005986850 TotalBytes 13
        [  2] NORMAL       0x000000011692fe20 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 0 TransferLength    13 TDSize  0
        [  3] EVENT_DATA   0x000000011692fe30 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 0 Data  0 0xfffffa8005b96210 TotalBytes 13
        [  4] NORMAL       0x000000011692fe40 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 0 TransferLength    13 TDSize  0
        [  5] EVENT_DATA   0x000000011692fe50 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 0 Data  0 0xfffffa8005b96210 TotalBytes 13
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






