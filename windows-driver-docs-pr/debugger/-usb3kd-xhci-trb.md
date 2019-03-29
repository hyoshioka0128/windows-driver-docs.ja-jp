---
title: usb3kd.xhci_trb
description: Usb3kd.xhci_trb 拡張機能は、1 つまたは複数の転送要求 (TRBs) によって使用されるブロック、USB 3.0 ホスト コント ローラーを表示します。
ms.assetid: 6EC90908-320E-4908-BE53-1AD01A81B140
keywords:
- デバッグ usb3kd.xhci_trb Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_trb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4a3a39bb133dc3827b3dc0b94421669c05e9ab2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573197"
---
# <a name="usb3kdxhcitrb"></a>! usb3kd.xhci\_trb


[ **! Usb3kd.xhci\_trb** ](-usb3kd-device-info.md)拡張機能は、1 つまたは複数の転送要求 (TRBs) によって使用されるブロック、USB 3.0 ホスト コント ローラーを表示します。

```dbgcmd
!usb3kd.xhci_trb VirtualAddress Count
!usb3kd.xhci_trb PhysicalAddress Count 1
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *virtualAddress*   
TRB の仮想アドレス。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span> *PhysicalAddress*   
TRB の物理アドレスです。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
表示するには連続する TRBs の数を開始位置として*VirtualAddress*または*PhysicalAddress*します。

<span id="_______1______"></span> 1   
アドレスが物理アドレスを指定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>コメント
-------

出力、 [ **! xhci\_trb** ](-usb3kd-device-info.md)コマンドは、USB 3.0 ホスト コント ローラー ドライバー (UsbXhci.sys) によって管理されるデータ構造に基づきます。 USB 3.0 ホスト コント ローラーのドライバーと USB スタック内の他のドライバーの詳細については、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)します。

<a name="examples"></a>使用例
--------

次の例では、 **0x844d7c00** TRB の仮想アドレスです。 **1**は、数は、表示する数の連続する TRBs を指定します。

```dbgcmd
0: kd> !xhci_trb 0x844d7c00 1

        [  0] ISOCH        0x844d7c00 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  2688 TDSize  0 TBC 0 TLBPC 2 Frame 0x3D2
```

次の例では、 **0x0dced7c00** TRB の物理アドレスです。 **4**は、数は、表示する数の連続する TRBs を指定します。 **1**アドレスが物理アドレスを指定します。

```dbgcmd
0: kd> !xhci_trb 0x0dced7c00 4 1

        [  0] ISOCH        0xdced7c00 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  2688 TDSize  0 TBC 0 TLBPC 2 Frame 0x3D2
        [  1] EVENT_DATA   0xdced7c10 CycleBit 1 IOC 1 CH 0 BEI 1 InterrupterTarget 1 Data 0x194c9bcf001b0001 PacketId 27 Frame 0x194c9bcf TotalBytes 2688
        [  2] ISOCH        0xdced7c20 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  1352 TDSize  2 TBC 0 TLBPC 2 Frame 0x3D2
        [  3] NORMAL       0xdced7c30 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  1336 TDSize  0
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






