---
title: usbkd. usbkd
description: Usbkd. usbkd コマンドを実行すると、usbkd _HCD_TRANSFER_CONTEXT 構造の情報が表示されます。
ms.assetid: 603AD207-69D5-4DED-80B5-ADA21E191D47
keywords:
- usbkd. usbkd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbtx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ebfa930c07a75f0c1ab6b010f6af82bc4733f658
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534675"
---
# <a name="usbkdusbtx"></a>!usbkd.usbtx


**! Usbkd. usbkd**コマンドを実行すると、 **usbkd \_ から情報が表示されます。HCD \_ TRANSFER \_ コンテキスト**構造体。

```dbgcmd
!usbkd.usbtx StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
**Usbport のアドレス。 \_HCD \_ TRANSFER \_ コンテキスト**構造体。 USB ホストコントローラーの転送リストを取得するには、 [**! usbhcdext**](-usbkd-usbhcdext.md)コマンドを使用します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

Usbport のアドレスを確認する方法の1つを次に示し**ます。 \_HCD \_ TRANSFER \_ コンテキスト**構造体。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
...
```

上記の出力では、FDO のデバイス拡張機能のアドレスが、 [DML](debugger-markup-language-commands.md)コマンド **! uhci \_ info ffffe00001c8f1a0**の引数として表示されます。

[DML] コマンドをクリックするか、デバイス拡張機能のアドレスを[**! usbhcdext**](-usbkd-usbhcdext.md)に渡して、転送リストを取得します。

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

前の出力で、 `ffffe0000653401c` は** \_ HCD \_ TRANSFER \_ コンテキスト**構造のアドレスです。 このアドレスを **! usbtx**に渡します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






