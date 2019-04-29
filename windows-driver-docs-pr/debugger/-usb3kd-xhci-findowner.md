---
title: usb3kd-xhci_findowner
description: Usb3kd.xhci_findowner コマンドは、共通のバッファーに所有者を検索します。
ms.assetid: 6AA3E41C-5838-4425-B1CE-37A13E8F755E
keywords:
- デバッグ usb3kd.xhci_findowner Windows
ms.date: 10/18/2018
topic_type:
- apiref
api_name:
- usb3kd.xhci_findowner
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed0c94f1e05aa891a77ba29406af2d84c4adbef1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330778"
---
# <a name="usb3kdxhcifindowner"></a>!usb3kd.xhci\_findowner


**! Usb3kd.xhci\_findowner**コマンドは、一般的なバッファーの所有者を検索します。

```dbgcmd
!usb3kd.xhci_findowner Address
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
一般的なバッファーのアドレスを仮想または物理です。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

共通のバッファーは、ハードウェアによってアドレス指定可能な物理的に連続するメモリのブロックです。 USB 3.0 ドライバー スタックは、USB 3.0 ホスト コント ローラーと通信する一般的なバッファーを使用します。 たとえば、システムのクラッシュとバッファー メモリの一般的な場合がありますが疑われるアドレスに遭遇します。 メモリが (場合は、複数の USB 3.0 コント ローラーがあること) に属する場合、アドレスは共通のバッファー メモリでは、このコマンドでは、USB 3.0 ホスト コント ローラーのメモリが使用されます。

<a name="examples"></a>例
--------

次の例では[ **! xhci\_resourceusage** ](-usb3kd-xhci-resourceusage.md)いくつかの一般的なバッファーのアドレスを一覧表示します。

```dbgcmd
0: kd> !usb3kd.xhci_resourceusage 0x867fbff0

## Dumping CommonBuffer Resources
------------------------------
    dt USBXHCI!_COMMON_BUFFER_DATA 0x868d61c0
    DmaEnabler:!wdfdmaenabler 0x79729fe8

    CommonBuffers Large: Total 8 Available 2 Used 6 TotalBytes 32768
        [ 1] dt _TRACKING_DATA 0x868d73a4 VA 0x868e0000 LA 0xdb2e0000 -- Owner 0x86801690 Tag: Int2 Size 4096
        [ 2] dt _TRACKING_DATA 0x868d6d1c VA 0x868e1000 LA 0xdb2e1000 -- Owner 0x86801690 Tag: Int2 Size 4096
        [ 3] dt _TRACKING_DATA 0x868d6c54 VA 0x868e2000 LA 0xdb2e2000 -- Owner 0x86801690 Tag: Int2 Size 4096
        [ 4] dt _TRACKING_DATA 0x868d6b8c VA 0x868e3000 LA 0xdb2e3000 -- Owner 0x86801690 Tag: Int2 Size 4096
        [ 5] dt _TRACKING_DATA 0x868d67b4 VA 0x868e5000 LA 0xdb2e5000 -- Owner 0x86801548 Tag: Slt1 Size 4096
        [ 6] dt _TRACKING_DATA 0x868d50b4 VA 0x868e6000 LA 0xdb2e6000 -- Owner 0x86801548 Tag: Slt3 Size 4096

    CommonBuffers Small: Total 16 Available 13 Used 3 TotalBytes 8192
        [ 1] dt _TRACKING_DATA 0x868d6974 VA 0x868e4000 LA 0xdb2e4000 -- Owner 0x86801690 Tag: Int1 Size 512
        [ 2] dt _TRACKING_DATA 0x868d69a4 VA 0x868e4200 LA 0xdb2e4200 -- Owner 0x86801548 Tag: Slt2 Size 512
        [ 3] dt _TRACKING_DATA 0x868d69d4 VA 0x868e4400 LA 0xdb2e4400 -- Owner 0x86801488 Tag: Cmd1 Size 512
```

上記の出力に表示されている仮想アドレスの 1 つは、0x868e2000 です。 次の例には、そのアドレスを渡します **! xhci\_findowner**します。 上記の出力に表示されている物理アドレスの 1 つは、0xdb2e4400 です。 次の例に 0xdb2e4440 (オフセット 0x40 0xdb2e4400 からバイト単位) を渡す **! xhci\_findowner**します。

```dbgcmd
0: kd> !xhci_findowner 0x868e2000 

!xhci_info 0x867fbff0  Texas Instruments - PCI: VendorId 0x104c DeviceId 0x8241 RevisionId 0x02

    dt _TRACKING_DATA 0x868d6c54 VA 0x868e2000 LA 0xdb2e2000 -- Owner 0x86801690 Tag: Int2 Size 4096

    dt _INTERRUPTER_DATA 0x86801690 
    !xhci_eventring 0x867fbff0  <-- This memory is used for event ring.


0: kd> !xhci_findowner 0xdb2e4440  <-- Note the offset difference.

!xhci_info 0x867fbff0  Texas Instruments - PCI: VendorId 0x104c DeviceId 0x8241 RevisionId 0x02

    dt _TRACKING_DATA 0x868d69d4 VA 0x868e4400 LA 0xdb2e4400 -- Owner 0x86801488 Tag: Cmd1 Size 512

    dt _COMMAND_DATA 0x86801488 
    !xhci_commandring 0x867fbff0  <-- This memory is used for command ring.
```

**! Xhci\_findowner**コマンドは、転送要求のブロック (TRB) で、アドレスを場合し、が属しているデバイスのスロットにそれを追跡したい場合に特に便利です。 次の例で、アドレスのいずれかの出力に表示[ **! xhci\_転送**](-usb3kd-xhci-transferring.md) 0xda452230、これは、TRB の物理アドレスですが。 この例でそのアドレスを渡して **! xhci\_findowner**します。 出力は、デバイスのスロット 8、TRB が属していることを示しています (**! xhci\_deviceslots 0x8551d370 8**)。

```dbgcmd
0: kd> !usb3kd.xhci_transferring 0x87652200

        [  0] NORMAL       0xda452200 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 2 TransferLength     6 TDSize  0
        [  1] EVENT_DATA   0xda452210 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 2 Data 0x8511375c TotalBytes 6
        [  2] NORMAL       0xda452220 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 2 TransferLength     6 TDSize  0
        [  3] EVENT_DATA   0xda452230 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 2 Data 0x857d076c TotalBytes 6

0: kd> !xhci_findowner 0xda452230 

!xhci_info 0x8551d370  Renesas - PCI: VendorId 0x1912 DeviceId 0x0015 RevisionId 0x02 Firmware 0x0020.0006

    dt _TRACKING_DATA 0x8585fd5c VA 0x87652200 LA 0xda452200 -- Owner 0x85894548 Tag: Rng1 Size 512

    !xhci_deviceslots 0x8551d370 8

    [0] dt _TRANSFERRING_DATA 0x85894548 Events: 0x0 TransferRingState_Idle
    ------------------------------------------------------------------------------
        WdfQueue: !wdfqueue 0x7a76bcb0 (0 waiting)
        CurrentRingBufferData: VA 0x87652200 LA 0xda452200 !wdfcommonbuffer 0x7a7a0370 Size 512
        Current:  !xhci_transferring 0x87652200
        PendingTransferList: 
            [0] dt _TRANSFER_DATA 0x851136f0 !urb 0x84e55468 !wdfrequest 0x7aeec9e8 TransferState_Pending
            [1] dt _TRANSFER_DATA 0x857d0700 !urb 0x85733be8 !wdfrequest 0x7a82f9d8 TransferState_Pending
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






