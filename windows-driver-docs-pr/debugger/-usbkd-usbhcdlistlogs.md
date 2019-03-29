---
title: usbkd.usbhcdlistlogs
description: Usbkd.usbhcdlistlogs ログとデバッグ ログ (Fdo) のすべての機能のデバイス オブジェクトの一覧が表示されますが、USB ポート ドライバー (Usbport.sys) に関連付けられているコマンドします。
ms.assetid: C86646D3-7B39-4C8C-9FDA-FD07AA7A880A
keywords:
- デバッグ usbkd.usbhcdlistlogs Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlistlogs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: da59ea96bd8beec1d7d43e5e6e7e32989d10261f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572537"
---
# <a name="usbkdusbhcdlistlogs"></a>!usbkd.usbhcdlistlogs


**! Usbkd.usbhcdlistlogs**コマンドは、USB ポート ドライバー (Usbport.sys) に関連付けられている機能のデバイス オブジェクト (Fdo) すべての一覧を表示します。 コマンドには、すべての EHCI ホスト コント ローラーの完全なデバッグ ログも表示されます。

```dbgcmd
!usbkd.usbhcdlistlogs
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>使用例
--------

この例の出力の一部を示しています、 **! usbhcdlistlogs**コマンド。

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

UHCI ホスト コント ローラーを表す 2 つの Fdo と EHCI ホスト コント ローラーを表す 1 つの FDO コマンドの出力を示しています。 出力には、1 つの EHCI ホスト コント ローラーのデバッグ ログが表示されます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






