---
title: usbkd. usbhcdlogex
description: Usbkd-usbhcdlogex コマンドは、USB ホストコントローラーの注釈付きデバッグログを表示します。
ms.assetid: 47274AEE-0BDB-4C25-9158-6213366434E0
keywords:
- usbkd. usbhcdlogex Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlogex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 323cc9f88ca406185b02173e6ba00391f1bb8fdb
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533995"
---
# <a name="usbkdusbhcdlogex"></a>!usbkd.usbhcdlogex


この**コマンドは**、USB ホストコントローラーの注釈付きデバッグログを表示します。

```dbgcmd
!usbkd.usbhcdlogex DeviceExtension[, NumberOfEntries]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
UHCI または EHCI USB ホストコントローラーの機能デバイスオブジェクト (FDO) のデバイス拡張機能のアドレス。

<span id="_______NumberOfEntries______"></span><span id="_______numberofentries______"></span><span id="_______NUMBEROFENTRIES______"></span>*Numberofentries*   
表示するログエントリの数。 ログ全体を表示するには、このパラメーターを-1 に設定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

USB ホストコントローラーの FDO のデバイス拡張機能のアドレスを確認する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0 kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

上記の出力では、FDO のデバイス拡張機能のアドレスが、 [DML](debugger-markup-language-commands.md)コマンドの引数として表示されます **! ehci \_ info ffffe00001ca11a0**です。

次に、デバイス拡張機能のアドレスを **! usbhcdlogex**コマンドに渡します。 この例では、2番目の引数によって、表示が20個のログエントリに制限されます。

```dbgcmd
0: kd> !usbkd.usbhcdlogex ffffe00001ca11a0, 20
LOG@: ffffe00001ca11b8 
>LOG mask = 3ff idx = fff68e95 (295)
*LOG: ffffe000020192a0  LOGSTART: ffffe00002014000 *LOGEND: ffffe0000201bfe0 # 20 
[ 000] ffffe000020192a0 xSt0 ffffe00001ca1b88 0000000000000006 0000000000000001 
[ 001] ffffe000020192c0 xnd8 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
[ 002] ffffe000020192e0 xnd0 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
//
// USBPORT_Xdpc_End()    - USBPORT_Core_UsbHcIntDpc_Worker() DPC/XDPC: 2 of 4

[ 003] ffffe00002019300 gNX0 0000000000000000 0000000000000000 ffffe00001ca1b88 
[ 004] ffffe00002019320 xbg1 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
[ 005] ffffe00002019340 xbg0 ffffe00001ca1b88 ffffe00001ca1050 ffffe00001ca22e8 
//
// USBPORT_Xdpc_iBegin() - USBPORT_Core_UsbHcIntDpc_Worker() DPC/XDPC: 2 of 4

[ 006] ffffe00002019360 tmo4 0000000000000000 0000000000000040 ffffe00001ca1c20 
[ 007] ffffe00002019380 tmo3 0000000000000000 0000000000989680 ffffe00001ca1c20 
[ 008] ffffe000020193a0 tmo2 0000000000000000 00000000000003e8 ffffe00001ca1c20 
[ 009] ffffe000020193c0 tmo1 0000000000000000 000000000002625a ffffe00001ca1c20 
[ 010] ffffe000020193e0 tmo0 00000000000003e8 ffffe00001ca1b88 ffffe00001ca1c20 
[ 011] ffffe00002019400 hci0 0000000000000000 0000000000000000 0000000000000000 
[ 012] ffffe00002019420 xSt0 ffffe00001ca1b88 0000000000000008 0000000000000003 
[ 013] ffffe00002019440 xdw4 ffffe00001ca1b88 0000000000000000 0000000000000000 
[ 014] ffffe00002019460 xdw2 ffffe00001ca1b88 ffffe00001ca1050 0000000000000002 
[ 015] ffffe00002019480 xdB0 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
//
// USBPORT_Xdpc_Worker_HcIntDpc()  DPC/XDPC: 2 of 4

[ 016] ffffe000020194a0 iDP- 0000000000000000 0000000000b73e26 0000000000000000 
//
// USBPORT_IsrDpc() - Exit()

[ 017] ffffe000020194c0 xSt0 ffffe00001ca1b88 0000000000000007 0000000000000002 
[ 018] ffffe000020194e0 Xsi1 ffffe00001ca1b88 0000000000000000 0000000000000000 
//
// USBPORT_Xdpc_iSignal()- USBPORT_Core_UsbHcIntDpc_Worker() DPC/XDPC: 2 of 4

[ 019] ffffe00002019500 chgZ 0000000000000000 0000000000b73e26 0000000000000000 
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






