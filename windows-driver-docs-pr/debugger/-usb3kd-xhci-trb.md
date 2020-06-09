---
title: xhci_trb usb3kd
description: Usb3kd 拡張機能は、USB 3.0 ホストコントローラーによって使用される1つ以上の転送要求ブロック (TRBs) を表示し xhci_trb ます。
ms.assetid: 6EC90908-320E-4908-BE53-1AD01A81B140
keywords:
- usb3kd Windows デバッグの xhci_trb
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_trb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 60ffcd92318d85827366001e83fc6d2cab3b9699
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534099"
---
# <a name="usb3kdxhci_trb"></a>! usb3kd. xhci \_ trb


! Usb3kd 拡張機能は、USB 3.0 ホストコントローラーによって使用される1つ以上の転送要求ブロック ( [** \_ trb**](-usb3kd-device-info.md) ) を表示します。

```dbgcmd
!usb3kd.xhci_trb VirtualAddress Count
!usb3kd.xhci_trb PhysicalAddress Count 1
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span>*Virtualaddress*   
TRB の仮想アドレス。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span>*PhysicalAddress*   
TRB の物理アドレス。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span>*カウント*   
*Virtualaddress*または*PhysicalAddress*を開始位置として、表示する連続した trbs の数。

<span id="_______1______"></span>1   
アドレスが物理アドレスであることを指定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

[**! Xhci \_ trb**](-usb3kd-device-info.md)コマンドの出力は、USB 3.0 ホストコントローラードライバー (UsbXhci) によって管理されているデータ構造に基づいています。 Usb 3.0 ホストコントローラードライバーおよび USB スタック内のその他のドライバーの詳細については、「 [Windows の usb ホスト側ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

<a name="examples"></a>例
--------

次の例では、 **0x844d7c00**は trb の仮想アドレスです。 **1**はカウントで、表示する連続する連続数を指定します。

```dbgcmd
0: kd> !xhci_trb 0x844d7c00 1

        [  0] ISOCH        0x844d7c00 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  2688 TDSize  0 TBC 0 TLBPC 2 Frame 0x3D2
```

次の例では、 **0x0dced7c00**は trb の物理アドレスです。 **4**はカウントで、表示する連続する連続数を指定します。 **1**は、アドレスが物理アドレスであることを指定します。

```dbgcmd
0: kd> !xhci_trb 0x0dced7c00 4 1

        [  0] ISOCH        0xdced7c00 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  2688 TDSize  0 TBC 0 TLBPC 2 Frame 0x3D2
        [  1] EVENT_DATA   0xdced7c10 CycleBit 1 IOC 1 CH 0 BEI 1 InterrupterTarget 1 Data 0x194c9bcf001b0001 PacketId 27 Frame 0x194c9bcf TotalBytes 2688
        [  2] ISOCH        0xdced7c20 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  1352 TDSize  2 TBC 0 TLBPC 2 Frame 0x3D2
        [  3] NORMAL       0xdced7c30 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  1336 TDSize  0
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






