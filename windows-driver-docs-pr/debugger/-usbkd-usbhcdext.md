---
title: usbhcdext
description: Usbhcdext コマンドは、USB ホストコントローラーまたは USB ルートハブのデバイス拡張機能の情報を表示します。
ms.assetid: 83811F9F-5899-4EC8-83D7-39EE884C0A01
keywords:
- usbhcdext Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0f318c5dd53465f624fc43e42bcea4cb2e35a313
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534699"
---
# <a name="usbkdusbhcdext"></a>!usbkd.usbhcdext


[**Usbhcdext**](-usbkd-usbhcdext.md)コマンドは、usb ホストコントローラーまたは usb ルートハブのデバイス拡張機能の情報を表示します。

```dbgcmd
!usbkd.usbhcdext DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
次のいずれかのアドレス。

-   USB ホストコントローラーの機能デバイスオブジェクト (FDO) のデバイス拡張機能。
-   物理デバイスオブジェクト (PDO) の USB ルートハブのデバイス拡張機能。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

EHCI ホストコントローラーの FDO のデバイス拡張機能のアドレスを確認する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
 ...
```

上記の出力では、FDO のデバイス拡張機能のアドレスが、 [DML](debugger-markup-language-commands.md)コマンドの引数として表示されます **! ehci \_ info ffffe00001ca11a0**です。

次に、デバイス拡張機能のアドレスを[**! usbhcdext**](-usbkd-usbhcdext.md)コマンドに渡します。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0

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
```

ルートハブの PDO のデバイス拡張機能のアドレスを確認する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
 ...
```

上記の出力には、コマンド **! devstack ffffe00002320050**の引数として表示されるルートハブの FDO のアドレスが表示されます。 [**! Devstack**](-devstack.md)コマンドを使用して、pdo のアドレスと pdo デバイス拡張機能を検索します。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

前の出力では、ルートハブの PDO のデバイス拡張機能のアドレスがであることがわかり `ffffe0000213c1a0` ます。

次に、デバイス拡張機能のアドレスを[**! usbhcdext**](-usbkd-usbhcdext.md)コマンドに渡します。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe0000213c1a0

Root Hub PDO Extension
Parent HC: FDO ffffe00001ca1050 !ehci_info ffffe00001ca11a0
HUB FDO ffffe00002320050 !hub2_info ffffe000023201a0
dt USBPORT!_PDO_EXTENSION ffffe0000213c5a0

## Pending Requests

[001] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe0000213c450 Tag: RHcr Obj: ffffe0000213c1a0
[002] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe00003ce5800 Tag: iIRP Obj: ffffe00002182210

## POWER FUNC HISTORY (latest at bottom)

[00] IRP_MN_WAIT_WAKE (PowerSystemHibernate)
...

## PnP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvPDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted 
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






