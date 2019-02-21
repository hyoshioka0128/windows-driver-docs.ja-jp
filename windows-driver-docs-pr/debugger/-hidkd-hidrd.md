---
title: hidkd.hidrd
description: Hidkd.hidrd コマンドでは、生と解析の両方の形式で、HID レポート記述子を表示します。
ms.assetid: 8A9D76F2-7A36-4458-83A4-EDCB153EC45A
keywords:
- デバッグ hidkd.hidrd Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidrd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1ef10fc0c2fb125fcec072f26ffc5f5501b8d217
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549757"
---
# <a name="hidkdhidrd"></a>!hidkd.hidrd


**! Hidkd.hidrd**コマンドは、生と解析の両方の形式で、HID レポート記述子を表示します。

```dbgcmd
!hidkd.hidrd rd Length
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______rd______"></span><span id="_______RD______"></span> *rd*   
生のレポート記述子のデータのアドレス。 記述子のデータのアドレスを取得する、 [ **! hidfdo** ](-hidkd-hidfdo.md)コマンド。

<span id="_______Length______"></span><span id="_______length______"></span><span id="_______LENGTH______"></span> *長さ*   
生のレポート記述子のデータの長さ、(バイト単位)。 長さを取得するには、使用、 [ **! hidfdo** ](-hidkd-hidfdo.md)コマンド。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Hidkd.dll

<a name="examples"></a>例
--------

この例は、使用する方法を示します、 [ **! hidfdo** ](-hidkd-hidfdo.md)コマンドに続けて、 **! hidrd**コマンド。 出力 **! hidfdo**アドレスと生のレポート記述子のデータの長さの両方を示しています。

```dbgcmd
0: kd> !hidfdo 0xffffe00004f466e0
# FDO 0xffffe00004f466e0  (!devobj/!devstack)

  Name              : \Device\_HID00000002
  ...
  Report Descriptor : !hidrd 0xffffe00004281a80 0x127
  ...

0: kd> !hidrd 0xffffe00004281a80 0x127
Report Descriptor at 0xffffe00004281a80

## Raw Data

0x0000: 05 01 09 02 A1 01 05 01-09 02 A1 02 85 1A 09 01
0x0010: A1 00 05 09 19 01 29 05-95 05 75 01 15 00 25 01
0x0020: 81 02 75 03 95 01 81 01-05 01 09 30 09 31 95 02
...

## Parsed

Usage Page (Generic Desktop Controls)....................0x0000: 05 01
Usage (Mouse)............................................0x0002: 09 02
Collection (Application).................................0x0004: A1 01
..Usage Page (Generic Desktop Controls)..................0x0006: 05 01
..Usage (Mouse)..........................................0x0008: 09 02
..Collection (Logical)...................................0x000A: A1 02
....Report ID (26).......................................0x000C: 85 1A
...
End Collection ()........................................0x0126: C0
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HID の拡張機能](hid-extensions.md)

 

 






