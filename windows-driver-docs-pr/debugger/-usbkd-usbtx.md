---
title: usbkd.usbtx
description: Usbkd.usbtx コマンドは、し、usbport _HCD_TRANSFER_CONTEXT 構造から情報を表示します。
ms.assetid: 603AD207-69D5-4DED-80B5-ADA21E191D47
keywords:
- デバッグ usbkd.usbtx Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbtx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aa91dd9e40441df750420fd6deb7b11713f6bf80
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327974"
---
# <a name="usbkdusbtx"></a>!usbkd.usbtx


**! Usbkd.usbtx**コマンドからの情報を表示、**し、usbport!\_HCD\_転送\_コンテキスト**構造体。

```dbgcmd
!usbkd.usbtx StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**し、usbport!\_HCD\_転送\_コンテキスト**構造体。 USB ホスト コント ローラーに対する転送リストを取得する、 [ **! usbkd.usbhcdext** ](-usbkd-usbhcdext.md)コマンド。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

以下のアドレスを検索する 1 つの方法を示します、**し、usbport!\_HCD\_転送\_コンテキスト**構造体。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! uhci\_情報 ffffe00001c8f1a0**します。

DML コマンドをクリックするか、デバイスの拡張機能のアドレスを渡す[ **! usbhcdext** ](https://msdn.microsoft.com/library/windows/hardware/dn367072)転送リストを取得します。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001c8f1a0
...
## I/O TRANSFER LIST(s)

1.) Transfer Request Priority List: (TxQueued) Type: 0-NotSplit, 1-Parent, 2-Child
    --------------------------------------------------------------------------------
    [000]!usbtx ffffe0000653401c !usbep ffffe00004730c60 !irp ffffe00004221220 State: (7)TX_Mapped_inMp
        Priority: 0, Type: 0, Flags= 0000000a, SequenceNum: 10, SplitIdx: 0
        InLen: 4096, OutLen: 0 Status: USBD_STATUS_PENDING (0x40000000)
    ...
```

上記の出力で`ffffe0000653401c`のアドレス、  **\_HCD\_転送\_コンテキスト**構造体。 このアドレスを渡す **! usbtx**します。

```dbgcmd
0: kd> !usbkd.usbtx ffffe0000653401c

dt usbport!_HCD_TRANSFER_CONTEXT ffffe0000653401c
dt usbport!_TRANSFER_PARAMETERS ffffe0000653417c

## TX HISTORY

## EVENT, STATE, NEXT (latest at bottom)

[01]    (23)Ev_TX_Icsq, (0)TX_Undefined, (1)TX_InQueue
[02]    (5)Ev_TX_MapTransfer, (1)TX_InQueue, (2)TX_MapPending
[03]    (7)Ev_TX_MpSubmitSuccess, (2)TX_MapPending, (7)TX_Mapped_inMp

**DMA**
dt usbport!_TRANSFER_SG_LIST ffffe0000653439c
SgCount:  1  MdlVirtualAddress: ffffe00000437000  MdlSystemAddress: ffffe00000437000
    [0] dt usbport!_TRANSFER_SG_ENTRY ffffe000065343bc
    : sysaddr: 0000000000000000 len 0x00001000(4096) offset 0x00000000(0) phys 00000000'ded90000
---
dt usbport!_SCATTER_GATHER_ENTRY ffffe000065343ec
dt _SCATTER_GATHER_LIST ffffe00001bc231c
NumberOfElements = 1
    [0] dt _SCATTER_GATHER_ELEMENT ffffe00001bc232c
     :phys 00000000'ded90000 len 0x00001000(4096)
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






