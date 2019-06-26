---
title: usbkd.usbep
description: Usbkd.usbep コマンドでは、USB エンドポイントに関する情報が表示されます。
ms.assetid: FEF66394-0502-4F3F-ACBE-57AA1945CC74
keywords:
- デバッグ usbkd.usbep Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbep
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e044f021598cff11d913860252e17b82ff5c7580
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367987"
---
# <a name="usbkdusbep"></a>!usbkd.usbep


**! Usbkd.usbep**コマンドは、USB エンドポイントに関する情報を表示します。

```dbgcmd
!usbkd.usbep StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**し、usbport!\_HCD\_エンドポイント**構造体。 USB ホスト コント ローラーのエンドポイントの一覧を取得する、 [ **! usbkd.usbhcdext** ](-usbkd-usbhcdext.md)コマンド。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

以下のアドレスを検索する 1 つの方法を示します、**し、usbport!\_HCD\_エンドポイント**構造体。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
     ...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! ehci\_情報 ffffe00001ca11a0**します。

DML コマンドをクリックするか、デバイスの拡張機能のアドレスを渡す[ **! usbhcdext** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-usbkd-usbhcdext)グローバル エンドポイント一覧を取得します。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0
...
DeviceHandleList: !usblist ffffe00001ca23b8, DL 
DeviceHandleDeletedList: !usblist ffffe00001ca23c8, DL [Empty]
GlobalEndpointList: !usblist ffffe00001ca2388, EP 
...
```

使用して、 [ **! usbkd.usblist** ](-usbkd-usblist.md)のアドレスを取得するコマンド **\_HCD\_エンドポイント**構造体。

```dbgcmd
0: kd> !usblist ffffe00001ca2388, EP

list: ffffe00001ca2388 EP
----------
dt usbport!_HCD_ENDPOINT ffffe000020f6970  !usbep ffffe000020f6970
Device Address: 0x00, ep 0x00 Control  Flags: 00000002 dt _USB_ENDPOINT_FLAGS ffffe000020f6990
dt usbport!_ENDPOINT_PARAMETERS ffffe000020f6b18    RootHub Endpoint
...
```

上記の出力で`ffffe000020f6970 `のアドレス、  **\_HCD\_エンドポイント**構造体。 このアドレスを渡す **! usbkd.usbep**します。

```dbgcmd
0: kd> !usbep ffffe000020f6970
Device Address: 0x00, Endpoint Address 0x00 Endpoint Type: Control 
dt USBPORT!_HCD_ENDPOINT ffffe000020f6970
dt USBPORT!_ENDPOINT_PARAMETERS ffffe000020f6b18
RootHub Endpoint

## Transfer(s) List: (HwPendingListHead)

    [EMPTY]

## Endpoint Reference List: (EpRefListHead)

[00] dt USBPORT!_USBOBJ_REF ffffe000021a64a0 Object ffffe000020f6970 Tag:EPop Endpoint:ffffe000020f6970
[01] dt USBPORT!_USBOBJ_REF ffffe000021264a0 Object ffffe000020f95e0 Tag:EPpi Endpoint:ffffe000020f6970

## GEP HISTORY (latest at bottom)

##      EVENT                   STATE                     NEXT                      HwEpState

[01] Ev_gEp_Open             GEp_Init                  GEp_Paused                ENDPOINT_PAUSE
[02] Ev_gEp_ReqActive        GEp_Paused                GEp_Active                ENDPOINT_ACTIVE
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






