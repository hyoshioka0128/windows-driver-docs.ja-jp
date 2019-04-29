---
title: usbkd.usbhcdlist
description: Usbkd.usbhcdlist コマンドでは、USB ポート ドライバー (Usbport.sys) で表される、すべての USB ホスト コント ローラーに関する情報が表示されます。
ms.assetid: 877A6361-0DB9-4089-AF85-BABFBED8C440
keywords:
- デバッグ usbkd.usbhcdlist Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80a300a75432a4793426d0d7251511a0979988da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335579"
---
# <a name="usbkdusbhcdlist"></a>!usbkd.usbhcdlist


[ **! Usbkd.usbhcdlist** ](https://msdn.microsoft.com/library/windows/hardware/dn367074)コマンドは、USB ポート ドライバー (Usbport.sys) で表される、すべての USB ホスト コント ローラーに関する情報を表示します。 USB ポート ドライバーと関連付けられているミニポート ドライバーについては、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkId=251983)します。

```dbgcmd
!usbkd.usbhcdlist
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

出力の一部の例を次に示します[ **! usbhcdlist**](https://msdn.microsoft.com/library/windows/hardware/dn367074)します。

```dbgcmd
0: kd> !usbkd.usbhcdlist
MINIPORT List @ fffff80001e5bbd0

## List of UHCI controllers

!drvobj ffffe00002000060 dt USBPORT!_USBPORT_MINIPORT_DRIVER ffffe00001f48010 Registration Packet ffffe00001f48048

01
...

## List of EHCI controllers

!drvobj ffffe00001fd33a0 dt USBPORT!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0 Registration Packet ffffe00001f48c08

01. Xxxxx Corporation PCI: VendorID Xxxx DeviceID Xxxx RevisionId 0002
    !devobj ffffe00001ca1050
    !ehci_info ffffe00001ca11a0
    Operational Registers ffffd000228bf020
    Device Data ffffe00001ca2da0
    !usbhcdlog ffffe00001ca11a0
    nt!_KINTERRUPT ffffe000020abe78
    Device Capabilities ffffe00001ca135c
    Pending IRP's: 0, Transfers: 0 (Periodic(0), Async(0))
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






