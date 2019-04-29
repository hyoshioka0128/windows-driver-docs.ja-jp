---
title: usbkd._ehcitd
description: Usbkd._ehcitd コマンドは、usbehci _TRANSFER_CONTEXT 構造から情報を表示します。
ms.assetid: C0EE04CF-E059-4064-9791-3500E66B24FA
keywords:
- Windows デバッグ usbkd._ehcitd
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehcitd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d4548be97550c059ba74e851a3b23d4b39d4afb9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334120"
---
# <a name="usbkdehcitd"></a>! usbkd します。\_ehcitd


**! Usbkd\_ 。ehcitd**コマンドからの情報を表示、 **usbehci!\_転送\_コンテキスト**構造体。 非同期のエンドポイント (つまり、コントロールと一括エンドポイント) に関する情報を表示するのにには、このコマンドを使用します。

```dbgcmd
!usbkd._ehcitd StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**usbehci!\_転送\_コンテキスト**構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

この例のアドレスを取得する 1 つの方法を示しています、 **usbehci!\_転送\_コンテキスト**構造体。 使用[ **!\_ehciep** ](-usbkd--ehciep.md)エンドポイントに関する情報を表示します。

```dbgcmd
0: kd> !_ehciep ffffe000001ab618
*USBEHCI
dt usbehci!_ENDPOINT_DATA ffffe000001ab618
Flags: 0x00000000
dt usbehci!_HCD_QUEUEHEAD_DESCRIPTOR ffffd00021e65080
*HwQH ffffd00021e65080
HwQH
     HwQH.HLink dea2e002
     HwQH.EpChars 02002201
         DeviceAddress: 0x1
         IBit: 0x0
         EndpointNumber: 0x2
    ...
slot[0] dt usbehci!_ENDPOINT_SLOT ffffe000001ab798 - slot_NotBusy
----
     ffffd00021e65100
     dt usbehci!_HCD_TRANSFER_DESCRIPTOR ffffd00021e65100
    ....
```

上記の出力で`ffffd00021e65100`のアドレスを**usbehci!\_転送\_コンテキスト**構造体。 このアドレスを渡す **!\_ehcitd**します。

```dbgcmd
0: kd> !_ehcitd ffffd00021e65100
*USBEHCI TD 21e65100
Sig 20td
     qTD
     Next_qTD: d83cc200
     AltNext_qTD: d83cc180
     Token: 0x00000c00
         PingState: 0x0
         SplitXstate: 0x0
         MissedMicroFrame: 0x0
         XactErr: 0x0
         BabbleDetected: 0x0
         DataBufferError: 0x0
         Halted: 0x0
         Active: 0x0
         Pid: 0x0 - HcTOK_Out
         ErrorCounter: 0x3
         C_Page: 0x0
         InterruptOnComplete: 0x0
         BytesToTransfer: 0x0
         DataToggle: 0x0
     BufferPage[0]: 0x 0bad0-000  0bad0000  BufferPage64[0]: 00000000
     BufferPage[1]: 0x 0bad0-000  0bad0000  BufferPage64[1]: 00000000
     BufferPage[2]: 0x 0bad0-000  0bad0000  BufferPage64[2]: 00000000
     BufferPage[3]: 0x 0bad0-000  0bad0000  BufferPage64[3]: 00000000
     BufferPage[4]: 0x 0bad0-000  0bad0000  BufferPage64[4]: 00000000
Packet:00 52 e6 21 00 d0 ff ff 
PhysicalAddress: d83cc100
EndpointData: 001ab618
TransferLength : 0000001f
TransferContext: 00000000
Flags: 00000041
    TD_FLAG_BUSY
NextHcdTD: 21e65200
AltNextHcdTD: 21e65180
SlotNextHcdTD: 21e65200
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






