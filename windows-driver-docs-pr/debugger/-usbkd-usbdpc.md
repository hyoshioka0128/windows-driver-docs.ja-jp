---
title: usbkd.usbdpc
description: Usbkd.usbdpc コマンドでは、_XDPC_CONTEXT 構造体に格納されている情報が表示されます。
ms.assetid: 51ED1BB0-416B-4B2B-9F4D-61F841224126
keywords:
- デバッグ usbkd.usbdpc Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbdpc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b342e26fa856acfd2e457f61ffe635e81d64fe60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367991"
---
# <a name="usbkdusbdpc"></a>!usbkd.usbdpc


**! Usbkd.usbdpc**コマンドに格納されている情報を表示、  **\_XDPC\_コンテキスト**構造体。

```dbgcmd
!usbkd.usbdpc StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**し、usbport!\_XDPC\_コンテキスト**構造体。 USB ホスト コント ローラーの XDPC 一覧を取得する、 [ **! usbkd.usbhcdext** ](-usbkd-usbhcdext.md)コマンド。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

以下のアドレスを検索する 1 つの方法を示します、**し、usbport!\_XDPC\_コンテキスト**構造体。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
UHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001e77010
...
4)!uhci_info ffffe00001c7d1a0 !devobj ffffe00001c7d050 PCI: VendorId...
...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! uhci\_情報 ffffe00001c7d1a0**します。

DML コマンドをクリックするか、デバイスの拡張機能のアドレスを渡す[ **! usbhcdext** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-usbkd-usbhcdext) XDPC 一覧を取得します。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001c7d1a0
...
## XDPC List

01) dt USBPORT!_XDPC_CONTEXT ffffe00001c7df18
02) dt USBPORT!_XDPC_CONTEXT ffffe00001c7db88
03) dt USBPORT!_XDPC_CONTEXT ffffe00001c7dd50
04) dt USBPORT!_XDPC_CONTEXT ffffe00001c7e0e0
...
```

上記の出力で`ffffe00001c7df18`のアドレス、  **\_XDPC\_コンテキスト**構造体。 このアドレスを渡す **! usbdpc**します。

```dbgcmd
0: kd> !usbkd.usbdpc ffffe00001c7df18

dt USBPORT!_XDPC_CONTEXT ffffe00001c7df18

## XDPC HISTORY (latest at boottom)

##      EVENT                STATE                   NEXT

[01] Ev_Xdpc_End          XDPC_Running            XDPC_Enabled            
[02] Ev_Xdpc_Signal       XDPC_Enabled            XDPC_DpcQueued          
[03] Ev_Xdpc_Signal       XDPC_DpcQueued          XDPC_DpcQueued          
[04] Ev_Xdpc_Worker       XDPC_DpcQueued          XDPC_Running            
[05] Ev_Xdpc_Signal       XDPC_Running            XDPC_Signaled           
[06] Ev_Xdpc_End          XDPC_Signaled           XDPC_DpcQueued          
[07] Ev_Xdpc_Worker       XDPC_DpcQueued          XDPC_Running            
[08] Ev_Xdpc_End          XDPC_Running            XDPC_Enabled
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






