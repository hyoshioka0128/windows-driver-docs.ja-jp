---
title: hidkd.hidppd HID 拡張機能
description: Hidkd.hidppd コマンドには、HID preparsed データが表示されます。
ms.assetid: 049D206D-669D-49F4-81FE-2D8E443F9A9E
keywords:
- デバッグ hidkd.hidppd Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidppd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a9cceb8130bc5e27a87eedec775aad6c3f0748f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558878"
---
# <a name="hidkdhidppd"></a>!hidkd.hidppd


**! Hidkd.hidppd**コマンド preparsed HID データを表示します。

```dbgcmd
!hidkd.hidppd ppd
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______ppd______"></span><span id="_______PPD______"></span> *ppd*   
アドレスを**HIDP\_PREPARSED\_データ**構造体。 アドレスを取得する、 **HIDP\_PREPARSED\_データ**構造体を使用して[ **! hidfdo** ](-hidkd-hidfdo.md)または[ **! hidpdo**](-hidkd-hidpdo.md).

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Hidkd.dll

<a name="examples"></a>例
--------

この例は、使用する方法を示します[ **! hidpdo** ](-hidkd-hidpdo.md)続けて **! hidppd**します。 出力 **! hidpdo**のアドレスを示します、 **HIDP\_PREPARSED\_データ**構造体。

```dbgcmd

0: kd> !hidpdo 0xffffe000029f6060
## PDO 0xffffe000029f6060  (!devobj/!devstack)

  Collection Num  : 1
  Name            : \Device\_HID00000000#COLLECTION00000001
  ...
  Pre-parsed Data : 0xffffe000029d1010
  ...

0: kd> !hidkd.hidppd 0xffffe000029d1010
Reading preparsed data...
Preparsed Data at 0xffffe000029d1010  

## Summary

  UsagePage             : Vendor-defined (0xFFA0)
  Usage                 : 0x01
  Report Length         : 0x2(Input) 0x2(Output) 0x0(Feature)
  Link Collection Nodes : 2
  Button Caps           : 0(Input) 0(Output) 0(Feature)
  Value Caps            : 1(Input) 1(Output) 0(Feature)
  Data Indices          : 1(Input) 1(Output) 0(Feature)

## Input Value Capability #0

  Report ID         : 0x0
  Usage Page        : Vendor-defined (0xFFA1)
  Bit Size          : 0x8
  Report Count      : 0x1
  ...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HID の拡張機能](hid-extensions.md)

 

 






