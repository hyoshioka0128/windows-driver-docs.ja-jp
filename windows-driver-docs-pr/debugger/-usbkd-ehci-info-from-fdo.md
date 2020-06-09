---
title: usbkd. ehci_info_from_fdo
description: Usbkd. ehci_info_from_fdo コマンドは、USB ホストコントローラーに関する情報を表示します。
ms.assetid: C7026EF3-F58D-45EB-83D5-8B4A3E661759
keywords:
- usbkd. ehci_info_from_fdo Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.ehci_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cf9da8b15c2bfbe6c69a88cf526ed2b4f93778c2
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534057"
---
# <a name="usbkdehci_info_from_fdo"></a>! usbkd. \_ \_ fdo からの ehci 情報 \_


[**Fdo コマンド \_ \_ から \_ の! usbkd. EHCI info**](-usbkd-ehci-info-from-fdo.md)は、USB ホストコントローラーに関する情報を表示します。

```dbgcmd
!usbkd.ehci_info_from_fdo fdo
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______fdo______"></span><span id="_______FDO______"></span>*fdo*   
UHCI または EHCI USB ホストコントローラーの機能デバイスオブジェクト (FDO) のアドレス。 [**! Usb2tree**](-usbkd-usb2tree.md)コマンドの出力から FDO のアドレスを取得できます。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

最初に、 [**! usb2tree**](-usbkd-usb2tree.md)コマンドを使用して、FDO のアドレスを取得します。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

上記の出力では、USB ホストコントローラーの FDO のアドレスがであることがわかり `ffffe00001ca1050` ます。 [** \_ \_ \_ FDO から! ehci INFO**](-usbkd-ehci-info-from-fdo.md)のアドレスを FDO に渡します。

```dbgcmd
0: kd> !usbkd.ehci_info_from_fdo ffffe00001ca1050

HC Flavor 1000  FDO ffffe00001ca1050
Root Hub: FDO ffffe00002320050 !hub2_info ffffe000023201a0
Operational Registers ffffd000228bf020
Device Data ffffe00001ca2da0
dt USBPORT!_FDO_EXTENSION ffffe00001ca15a0
DM Timer Flags ffffe00001ca16d4
FDO Flags ffffe00001ca16d0
HCD Log ffffe00001ca11a0

DeviceHandleList: !usblist ffffe00001ca23b8, DL 
DeviceHandleDeletedList: !usblist ffffe00001ca23c8, DL [Empty]
GlobalEndpointList: !usblist ffffe00001ca2388, EP 
EpNeoStateChangeList: !usblist ffffe00001ca2370, SC [Empty]
GlobalTtListHead: !usblist ffffe00001ca23a8, TT [Empty]
BusContextHead: !usblist ffffe00001ca16b0, BC 

## Pending Requests

[001] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe00001ca1450 Tag: AddD Obj: ffffe00001ca11a0
...

## XDPC List

01) dt USBPORT!_XDPC_CONTEXT ffffe00001ca1f18
...

## PnP FUNC HISTORY (latest at bottom)

[01] IRP_MN_QUERY_CAPABILITIES
...
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






