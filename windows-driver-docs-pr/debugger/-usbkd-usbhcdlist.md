---
title: usbkd. usbhcdlist
description: USB ポートドライバー (usbkd) によって表されるすべての USB ホストコントローラーに関する情報が表示されます。
ms.assetid: 877A6361-0DB9-4089-AF85-BABFBED8C440
keywords:
- usbkd. usbhcdlist Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0386e8e89780cd874a507cfa87e7256f29d518b8
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534697"
---
# <a name="usbkdusbhcdlist"></a>!usbkd.usbhcdlist


[**! Usbkd**](-usbkd-usbhcdlist.md)は、usb ポートドライバー (usbkd) によって表されるすべての usb ホストコントローラーに関する情報が表示されます。 USB ポートドライバーと関連するミニポートドライバーの詳細については、「 [Windows の usb ホスト側ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

```dbgcmd
!usbkd.usbhcdlist
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

次に、 [**! usbhcdlist**](-usbkd-usbhcdlist.md)の出力の一部の例を示します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






