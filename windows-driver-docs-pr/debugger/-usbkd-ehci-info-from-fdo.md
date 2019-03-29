---
title: usbkd.ehci_info_from_fdo
description: Usbkd.ehci_info_from_fdo コマンドでは、USB ホスト コント ローラーに関する情報が表示されます。
ms.assetid: C7026EF3-F58D-45EB-83D5-8B4A3E661759
keywords:
- Windows デバッグ usbkd.ehci_info_from_fdo
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.ehci_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c13ea095d4d30e19b43dc91df331665a656130ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580566"
---
# <a name="usbkdehciinfofromfdo"></a>!usbkd.ehci\_info\_from\_fdo


[ **! Usbkd.ehci\_情報\_から\_fdo** ](https://msdn.microsoft.com/library/windows/hardware/dn367058)コマンドは、USB ホスト コント ローラーに関する情報を表示します。

```dbgcmd
!usbkd.ehci_info_from_fdo fdo
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______fdo______"></span><span id="_______FDO______"></span> *fdo*   
UHCI または EHCI USB ホスト コント ローラーの機能のデバイス オブジェクト (FDO) のアドレス。 出力から、FDO のアドレスを取得することができます、 [ **! usb2tree** ](-usbkd-usb2tree.md)コマンド。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>使用例
--------

まずを使用して、 [ **! usb2tree** ](-usbkd-usb2tree.md) FDO のアドレスを取得するコマンド。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

上記の出力で確認できます USB ホスト コント ローラーの FDO のアドレスが`ffffe00001ca1050`します。 FDO のアドレスを渡す[ **! ehci\_情報\_から\_fdo**](https://msdn.microsoft.com/library/windows/hardware/dn367058)します。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






