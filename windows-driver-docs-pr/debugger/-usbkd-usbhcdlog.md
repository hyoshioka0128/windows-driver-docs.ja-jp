---
title: usbkd.usbhcdlog
description: Usbkd.usbhcdlog コマンドでは、USB ホスト コント ローラーのデバッグ ログの一部が表示されます。
ms.assetid: 78FDC557-7791-422A-AB7B-5C9B6A1DF481
keywords:
- デバッグ usbkd.usbhcdlog Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 83f4f717e87a9dc35aac053467012d4818ef95e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363082"
---
# <a name="usbkdusbhcdlog"></a>!usbkd.usbhcdlog


[ **! Usbkd.usbhcdlog** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-usbkd-usbhcdlog)コマンドは、デバッグ ログを USB ホスト コント ローラーの一部を表示します。

```dbgcmd
!usbkd.usbhcdlog DeviceExtension[, NumberOfEntries]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
UHCI または EHCI USB ホスト コント ローラーの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能のアドレス。

<span id="_______NumberOfEntries______"></span><span id="_______numberofentries______"></span><span id="_______NUMBEROFENTRIES______"></span> *NumberOfEntries*   
表示するログ エントリの数。 全体のログを表示するには、このパラメーターを-1 に設定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

USB ホスト コント ローラーの FDO のデバイスの拡張機能のアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0 kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! ehci\_情報 ffffe00001ca11a0**します。

今すぐに、デバイスの拡張機能のアドレスを渡す、 **! usbhcdlog**コマンド。 この例では、2 番目の引数は、4 つのログ エントリを表示を制限します。

```dbgcmd
0: kd> !usbkd.usbhcdlog ffffe00001ca11a0, 4

LOG@: ffffe00001ca11b8 
>LOG mask = 3ff idx = fff68e95 (295)
*LOG: ffffe000020192a0  LOGSTART: ffffe00002014000 *LOGEND: ffffe0000201bfe0 # 4 
[ 000] ffffe000020192a0 xSt0 ffffe00001ca1b88 0000000000000006 0000000000000001 
[ 001] ffffe000020192c0 xnd8 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
[ 002] ffffe000020192e0 xnd0 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
[ 003] ffffe00002019300 gNX0 0000000000000000 0000000000000000 ffffe00001ca1b88 
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






