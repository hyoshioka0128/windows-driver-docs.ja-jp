---
title: usbkd._ehcidd
description: Usbkd._ehcidd コマンドは、usbehci _DEVICE_DATA 構造から情報を表示します。
ms.assetid: 8D594564-6506-44A8-A109-A76DA5AE7D89
keywords:
- Windows デバッグ usbkd._ehcidd
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehcidd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 19dd6101aa5c31de95b634a7bbfa67525de500fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335644"
---
# <a name="usbkdehcidd"></a>!usbkd.\_ehcidd


**! Usbkd\_ 。ehcidd**コマンドからの情報を表示、 **usbehci!\_デバイス\_データ**構造体。

```dbgcmd
!usbkd._ehcidd StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**usbehci!\_デバイス\_データ**構造体。 アドレスを検索する**usbehci!\_デバイス\_データ**構造体を使用して、 [ **! usbhcdext** ](-usbkd-usbhcdext.md)または[ **! usbhcdlist**](-usbkd-usbhcdlist.md)します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

以下のアドレスを取得する 1 つの方法を示します、 **usbehci!\_デバイス\_データ**構造体。 最初に入力[ **! usbkd.usbhcdlist**](-usbkd-usbhcdlist.md)します。

```dbgcmd
0: kd> !usbkd.usbhcdlist

MINIPORT List @ fffff80001e5bbd0

## List of EHCI controllers

!drvobj ffffe00001fd33a0 dt USBPORT!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0 Registration Packet ffffe00001f48c08

01. Xxxx Corporation PCI: VendorID Xxxx DeviceID Xxxx RevisionId 0002
    !devobj ffffe0000781a050
    !ehci_info ffffe0000781a1a0
    Operational Registers ffffd00021fb8420
    Device Data ffffe0000781bda0
    ...
```

上記の出力で`ffffe0000781bda0`のアドレスを**\_デバイス\_データ**構造体。

今すぐに構造体のアドレスを渡す **!\_ehcidd**

```dbgcmd
0: kd> !usbkd._ehcidd ffffe0000781bda0

*USBEHCI DEVICE DATA ffffe0000781bda0
** dt usbehci!_DEVICE_DATA ffffe0000781bda0 

get_field_ulong ffffe0000781bda0 usbehci!_DEVICE_DATA Flags
*All Enpoints list:
head @ ffffe0000781bdb0 f_link ffffe0000781bdb0 b_link ffffe0000781bdb0
AsyncQueueHead ffffd00021cf5000 !_ehciqh ffffd00021cf5000
    PhysicalAddress: 0xde79a000
    NextQh: ffffd00021cf5000 Hlink de79a002
    PrevQh: ffffd00021cf5000
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






