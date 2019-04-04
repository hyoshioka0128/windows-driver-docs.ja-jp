---
title: usb3kd.xhci_transferring
description: Usb3kd.xhci_transferring 拡張機能の表示 (USB 3.0 ホスト コント ローラーによって使用される) 転送リングまでサイクル ビットの変更を検出します。
ms.assetid: BCF6DEF0-FB58-4FE6-88AD-BF778E00F052
keywords:
- デバッグ usb3kd.xhci_transferring Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_transferring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa9d4a24348284957ddf781bd93382ec4c9fada8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570698"
---
# <a name="usb3kdxhcitransferring"></a>! usb3kd.xhci\_を転送します。


[ **! Usb3kd.xhci\_転送**](-usb3kd-device-info.md)拡張機能の表示 (USB 3.0 ホスト コント ローラーによって使用される) 転送リング サイクル ビットの変更を検出するまでです。

```dbgcmd
!usb3kd.xhci_transferring VirtualAddress
!usb3kd.xhci_transferring PhysicalAddress 1
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *virtualAddress*   
転送のリングの仮想アドレス。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span> *PhysicalAddress*   
転送のリングの物理アドレスです。

<span id="_______1______"></span> 1   
アドレスが物理アドレスを指定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>コメント
-------

出力、 **! xhci\_転送**コマンドは、USB 3.0 ホスト コント ローラー ドライバー (UsbXhci.sys) によって管理されるデータ構造に基づきます。 USB 3.0 ホスト コント ローラーのドライバーと USB スタック内の他のドライバーの詳細については、[USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)を参照してください。

転送のリングは、転送要求のブロック (TRBs) の一覧を維持するために、USB 3.0 ホスト コント ローラー ドライバーによって使用される構造です。 このコマンドは、転送のリングでは、仮想または物理アドレスを受け取りますが、TRBs の物理アドレスが表示されます。 これは、コマンドが正しくリンク TRBs を走査できるようにします。

<a name="examples"></a>使用例
--------

転送リングのアドレスを取得する出力の確認、 [ **! xhci\_deviceslots** ](-usb3kd-xhci-deviceslots.md)コマンド。 次の例では、転送のリングの仮想アドレスは、0xfffffa8005b2fe00 です。

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

転送リングのアドレスを渡すことができますので、 **! xhci\_転送**コマンド。

```dbgcmd
kd> !xhci_transferring 0xfffffa8005b2fe00

        [  0] NORMAL       0x000000011692fe00 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 0 TransferLength    13 TDSize  0
        [  1] EVENT_DATA   0x000000011692fe10 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 0 Data  0 0xfffffa8005986850 TotalBytes 13
        [  2] NORMAL       0x000000011692fe20 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 0 TransferLength    13 TDSize  0
        [  3] EVENT_DATA   0x000000011692fe30 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 0 Data  0 0xfffffa8005b96210 TotalBytes 13
        [  4] NORMAL       0x000000011692fe40 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 0 TransferLength    13 TDSize  0
        [  5] EVENT_DATA   0x000000011692fe50 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 0 Data  0 0xfffffa8005b96210 TotalBytes 13
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






