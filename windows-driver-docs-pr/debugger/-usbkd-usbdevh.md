---
title: usbkd.usbdevh
description: Usbkd.usbdevh コマンドでは、USB デバイス ハンドルに関する情報が表示されます。
ms.assetid: 463DAA72-F3EB-4C76-BB63-DA2EFA1EE9B1
keywords:
- デバッグ usbkd.usbdevh Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbdevh
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2db7fa43250e0a9110a00e669f3d7d8c9786daa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556610"
---
# <a name="usbkdusbdevh"></a>!usbkd.usbdevh


**! Usbkd.usbdevh**コマンドには、USB デバイス ハンドルに関する情報が表示されます。

```dbgcmd
!usbkd.usbdevh StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**し、usbport!\_USBD\_デバイス\_処理**構造体。 USB ホスト コント ローラーに対するデバイス ハンドルの一覧を取得する、 [ **! usbkd.usbhcdext** ](-usbkd-usbhcdext.md)コマンド。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

以下のアドレスを検索する 1 つの方法を示します、**し、usbport!\_USBD\_デバイス\_処理**構造体。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
     ...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! ehci\_情報 ffffe00001ca11a0**します。

DML コマンドをクリックするか、デバイスの拡張機能のアドレスを渡す[ **! usbhcdext** ](https://msdn.microsoft.com/library/windows/hardware/dn367072)デバイス ハンドルの一覧を取得します。

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
...
```

使用して、 [ **! usbkd.usblist** ](-usbkd-usblist.md)のアドレスを取得するコマンド**し、usbport!\_USBD\_デバイス\_処理**構造体。

```dbgcmd
0: kd> !usblist ffffe00001ca23b8, DL
list: ffffe00001ca23b8 DL
----------
!usbdevh ffffe000020f9590
SSP [IdleReady] (0)
...
```

上記の出力で`ffffe000020f9590`のアドレスを **\_USBD\_デバイス\_処理**構造体。 このアドレスを渡す **! usbdevh**します。

```dbgcmd
0: kd> !usbkd.usbdevh ffffe000020f9590

dt USBPORT!_USBD_DEVICE_HANDLE ffffe000020f9590
SSP [IdleReady] (0)
PCI\VEN_8086&DEV_293C  Intel Corporation
Root Hub
DriverName :  

## DEVICE HANDLE HISTORY (latest at boottom)

##      EVENT                        STATE                        NEXT

[01] Ev_CreateRoothub_Success     Devh_Created                 Devh_Valid                   

## Referene List: Head(ffffe000020f9668)

[00] dt USBPORT!_DEVH_REF_OBJ ffffe000021944a0  Object: ffffe000020f9590 Tag: dvh+ PendingFlag(0)
[01] dt USBPORT!_DEVH_REF_OBJ ffffe000020bbcb0  Object: ffffe000020ba7e0 Tag: bsCT PendingFlag(0)
[02] dt USBPORT!_DEVH_REF_OBJ ffffe000032b91a0  Object: ffffe0000269e670 Tag: UrbT PendingFlag(1)

## TtList: Head(ffffe000020f9658)


## PipeHandleList: Head(ffffe000020f9640)

[00] dt USBPORT!_USBD_PIPE_HANDLE_I ffffe000020f95e0 !usbep ffffe000020f6970
        Device Address: 0x00, Endpoint Address 0x00 Endpoint Type: Control 
[01] dt USBPORT!_USBD_PIPE_HANDLE_I ffffe000023bd278 !usbep ffffe0000212d970
        Device Address: 0x00, Endpoint Address 0x81 Endpoint Type: Interrupt In

Config Information: dt USBPORT!_USBD_CONFIG_HANDLE ffffe000023cd0b0

## Interface List:

[00] dt USBPORT!_USBD_INTERFACE_HANDLE_I ffffe000023bd250
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






