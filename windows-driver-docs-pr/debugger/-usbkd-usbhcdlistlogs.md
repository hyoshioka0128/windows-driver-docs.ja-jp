---
title: usbkd。 usbhcdlistlogs
description: USB ポートドライバー (Usbkd) およびデバッグログに関連付けられているすべての機能デバイスオブジェクト (FDOs) の一覧が表示されます。
ms.assetid: C86646D3-7B39-4C8C-9FDA-FD07AA7A880A
keywords:
- usbkd. usbhcdlistlogs Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlistlogs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b9d5aea4ae0528ed5683d95d3c2d95d865c16fe
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534013"
---
# <a name="usbkdusbhcdlistlogs"></a>!usbkd.usbhcdlistlogs


この**コマンドは**、USB ポートドライバー (usbkd) に関連付けられているすべての機能デバイスオブジェクト (fdos) の一覧を表示します。 このコマンドでは、すべての EHCI ホストコントローラーの完全なデバッグログも表示されます。

```dbgcmd
!usbkd.usbhcdlistlogs
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

この例では、 **! usbhcdlistlogs**コマンドの出力の一部を示します。

```dbgcmd
0: kd> !usbkd.usbhcdlistlogs

MINIPORT List @ fffff80001e5bbd0
*flink, blink ffffe00001f48018,ffffe00001f48bd8

[0] entry @: ffffe00001f48010 dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48010
UHCI MINIPORT @ ffffe00001f48010 !drvobj ffffe00002000060 regpkt ffffe00001f48048
02. !devobj ffffe00001ca4050 !usbhcdext ffffe00001ca41a0  HFDO 8086 2938  RHPDO ffffe0000213a050
03. !devobj ffffe00001ca7050 !usbhcdext ffffe00001ca71a0  HFDO 8086 2937  RHPDO ffffe00002140050

[1] entry @: ffffe00001f48bd0 dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0
EHCI MINIPORT @ ffffe00001f48bd0 !drvobj ffffe00001fd33a0 regpkt ffffe00001f48c08
01. !devobj ffffe00001ca1050 !usbhcdext ffffe00001ca11a0  HFDO 8086 293c  RHPDO ffffe0000213c050

LOG@: ffffe00001ca11b8 
>LOG mask = 3ff idx = fff69e8d (28d)
*LOG: ffffe000020191a0  LOGSTART: ffffe00002014000 *LOGEND: ffffe0000201bfe0 # -1 
[ 000] ffffe000020191a0 Tmt0 0000000000000000 0000000000000000 0000000000000000 
[ 001] ffffe000020191c0 _Pop 0000000000000003 0000000000003000 0000000000000000 
...
[ 005] ffffe00002019240 chgZ 0000000000000000 0000000000b7228f 0000000000000000 
[ 006] ffffe00002019260 nes- 0000000000000000 0000000000000000 0000000000000000 
[ 007] ffffe00002019280 nes+ ffffe00001ca2370 ffffe00001ca2370 00000000000ced39 
...
[1014] ffffe00002019060 tmo4 0000000000000000 0000000000000040 ffffe00001ca1c20 
...
[1022] ffffe00002019160 xdw2 ffffe00001ca1b88 ffffe00001ca1050 0000000000000002 
[1023] ffffe00002019180 xdB0 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
```

コマンドの出力には、UHCI ホストコントロールを表す2つの FDOs と、EHCI ホストコントローラーを表す1つの FDO が示されています。 次に、1つの EHCI ホストコントローラーのデバッグログが出力に表示されます。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






