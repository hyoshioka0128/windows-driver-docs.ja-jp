---
title: usbkd. _ehcidd
description: Usbehci コマンドを実行 _ehcidd すると、_DEVICE_DATA 構造の情報が表示されます。
ms.assetid: 8D594564-6506-44A8-A109-A76DA5AE7D89
keywords:
- usbkd. _ehcidd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehcidd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0612c1ba5c5d33a7665f8163071c1a599c172907
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534885"
---
# <a name="usbkd_ehcidd"></a>! usbkd。 \_ehcidd


**! Usbkd。 \_ehcidd**コマンドを実行すると、usbehci からの情報が表示され**ます。 \_デバイスの \_ データ**構造。

```dbgcmd
!usbkd._ehcidd StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbehci のアドレス** \_デバイスの \_ データ**構造。 Usbehci のアドレスを検索するには** \_デバイス \_ データ**構造では、 [**! usbhcdext**](-usbkd-usbhcdext.md)または[**! usbhcdlist**](-usbkd-usbhcdlist.md)を使用します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

Usbehci のアドレスを取得する方法の1つを次に示し**ます。 \_デバイスの \_ データ**構造。 最初に「 [**! usbkd. usbhcdlist**](-usbkd-usbhcdlist.md)」と入力します。

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

前の出力で、 `ffffe0000781bda0` は** \_ デバイス \_ データ**構造のアドレスです。

ここで、構造体のアドレスをに渡し**ます。 \_ehcidd**

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






