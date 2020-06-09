---
title: usbkd. usbkd
description: Usbkd. usbkd コマンドを実行すると、_XDPC_CONTEXT 構造に格納されている情報が表示されます。
ms.assetid: 51ED1BB0-416B-4B2B-9F4D-61F841224126
keywords:
- usbkd. usbkd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbdpc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: df23362fab8d5f2585926c483251ab1f9f2593c3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534703"
---
# <a name="usbkdusbdpc"></a>!usbkd.usbdpc


**! Usbkd. usbkd**コマンドを実行すると、 ** \_ xdpc \_ コンテキスト**構造に格納されている情報が表示されます。

```dbgcmd
!usbkd.usbdpc StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
**Usbport のアドレス。 \_XDPC \_ コンテキスト**構造体。 USB ホストコントローラーの XDPC リストを取得するには、 [**! usbhcdext**](-usbkd-usbhcdext.md)コマンドを使用します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

Usbport のアドレスを確認する方法の1つを次に示し**ます。 \_XDPC \_ コンテキスト**構造体。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
UHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001e77010
...
4)!uhci_info ffffe00001c7d1a0 !devobj ffffe00001c7d050 PCI: VendorId...
...
```

上記の出力では、FDO のデバイス拡張機能のアドレスが、 [DML](debugger-markup-language-commands.md)コマンド **! uhci \_ info ffffe00001c7d1a0**の引数として表示されます。

DML コマンドをクリックするか、デバイス拡張機能のアドレスを[**! usbhcdext**](-usbkd-usbhcdext.md)に渡して、xdpc リストを取得します。

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

前の出力で、 `ffffe00001c7df18` は** \_ xdpc \_ コンテキスト**構造のアドレスです。 このアドレスを **! usbdpc**に渡します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






