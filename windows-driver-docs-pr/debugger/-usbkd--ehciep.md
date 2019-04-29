---
title: usbkd._ehciep
description: Usbkd._ehciep コマンドは、usbehci _ENDPOINT_DATA 構造から情報を表示します。 非同期のエンドポイント (つまり、コントロールと一括エンドポイント) に関する情報を表示するのにには、このコマンドを使用します。
ms.assetid: 0DA42FDD-41D6-4234-9D9C-36872F0CE0C1
keywords:
- Windows デバッグ usbkd._ehciep
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciep
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 963aa03f2012ee0fb4826d64b365b14385eaf571
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335641"
---
# <a name="usbkdehciep"></a>!usbkd.\_ehciep


**! Usbkd\_ 。ehciep**コマンドからの情報を表示、 **usbehci!\_エンドポイント\_データ**構造体。 非同期のエンドポイント (つまり、コントロールと一括エンドポイント) に関する情報を表示するのにには、このコマンドを使用します。

```dbgcmd
!usbkd._ehciep StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**usbehci!\_エンドポイント\_データ**構造体。 アドレスを検索する**usbehci!\_エンドポイント\_データ**構造体を使用して、 [ **! usbhcdext** ](-usbkd-usbhcdext.md)と[ **! usblist**](-usbkd-usblist.md)します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

この例のアドレスを取得する 1 つの方法を示しています、 **usbehci!\_エンドポイント\_データ**構造体。 始まり、 [ **! usb2tree** ](-usbkd-usb2tree.md)コマンド。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe0000206e1a0 !devobj ffffe0000206e050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000024a61a0 !devstack ffffe000024a6050
        Port 1: !port2_info ffffe000026dd000 
        Port 2: !port2_info ffffe000026ddb40 
        Port 3: !port2_info ffffe000026de680 !devstack ffffe00001ec3060
            !device2_info ffffe00001ec31b0 (USB Mass Storage Device: Xxx Corporation)
        Port 4: !port2_info ffffe000026df1c0 
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! ehci\_情報 ffffe0000206e1a0**します。 DML コマンドをクリックするか、デバイスの拡張機能のアドレスを渡す[ **! usbhcdext**](https://msdn.microsoft.com/library/windows/hardware/dn367072)します。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe0000206e1a0
...
DeviceHandleList: !usblist ffffe0000206f3b8, DL 
DeviceHandleDeletedList: !usblist ffffe0000206f3c8, DL [Empty]
GlobalEndpointList: !usblist ffffe0000206f388, EP 
...
```

上記の出力には、コマンドが表示されます。 **! usblist ffffe0000206f388、EP**します。 このコマンドを使用すると、エンドポイントの一覧を表示できます。

```dbgcmd
0: kd> !usblist ffffe0000206f388, EP 
list: ffffe0000206f388 EP
...
dt usbport!_HCD_ENDPOINT ffffe000026dc970  !usbep ffffe000026dc970
common buffer bytes 0x00003000 (12288) @ va 0000000021e6e000 pa 00000000d83c9000
Device Address: 0x01, ep 0x81 Bulk In Flags: 00000041 dt _USB_ENDPOINT_FLAGS ffffe000026dc990
... usbehci!_ENDPOINT_DATA ffffe000026dcc38
...
```

上記の出力で`ffffe000026dcc38`のアドレスを**usbehci!\_エンドポイント\_データ**構造体。 このアドレスを渡す **!\_ehciep**します。

```dbgcmd
0: kd> !usbkd._ehciep ffffe000026dcc38
*USBEHCI
dt usbehci!_ENDPOINT_DATA ffffe000026dcc38
Flags: 0x00000000
dt usbehci!_HCD_QUEUEHEAD_DESCRIPTOR ffffd00021e6e080
*HwQH ffffd00021e6e080
HwQH
     HwQH.HLink dea2e002
     HwQH.EpChars 02002101
         DeviceAddress: 0x1
         IBit: 0x0
         EndpointNumber: 0x1
         EndpointSpeed: 0x2 HcEPCHAR_HighSpeed
         DataToggleControl: 0x0
         HeadOfReclimationList: 0x0
         MaximumPacketLength: 0x200 - 512
   ...
current slot 0000000000000000
slot[0] dt usbehci!_ENDPOINT_SLOT ffffe000026dcdb8 - slot_NotBusy
----
     ffffd00021e6e100
     dt usbehci!_HCD_TRANSFER_DESCRIPTOR ffffd00021e6e100
    tdphys: d83c9100'200 txlen 00000000 tx ffffd00000000041 flags 6d4e695d  _BUSY _SLOT_RESET
    Next_qTD: d83c9200'd83c9180 AltNext_qTD 77423c00'41 
    NextTD: ffffd00021e6e200 AltNextTD ffffd00021e6e180 SlotNextTd ffffd00021e6e200 tok 00000c00  Xbytes x0 (0)
.
     ffffd00021e6e200
     dt usbehci!_HCD_TRANSFER_DESCRIPTOR ffffd00021e6e200
    tdphys: d83c9200'5000 txlen 00000000 tx ffffd00000000041 flags 6d4e695d  _BUSY _SLOT_RESET
    Next_qTD: d83c9280'd83c9180 AltNext_qTD 77423c00'41 
    NextTD: ffffd00021e6e280 AltNextTD ffffd00021e6e180 SlotNextTd ffffd00021e6e280 tok 00000c00  Xbytes x0 (0)
...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






