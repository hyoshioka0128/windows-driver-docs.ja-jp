---
title: hidkd.hidfdo
description: Hidkd.hidfdo コマンドでは、機能のデバイス オブジェクト (FDO) に関連付けられた HID 情報が表示されます。
ms.assetid: CB8E8844-B5A7-4273-8401-D4F3C8CBAC4C
keywords:
- デバッグ hidkd.hidfdo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidfdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd543510a68f1455ef54fa71376a5eeedaf7ee24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336511"
---
# <a name="hidkdhidfdo"></a>!hidkd.hidfdo


**! Hidkd.hidfdo**コマンドには、機能のデバイス オブジェクト (FDO) に関連付けられた HID 情報が表示されます。

```dbgcmd
!hidkd.hidfdo fdo
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______fdo______"></span><span id="_______FDO______"></span> *fdo*   
FDO のアドレス。 HID ドライバーに関連付けられている Fdo のアドレスを取得する、 [ **! usbhid.hidtree** ](-hidkd-hidtree.md)コマンド。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Hidkd.dll

<a name="examples"></a>例
--------

出力の例を次に示します、 **! hidfdo**コマンド。 例の最初の呼び出し[ **! hidtree** ](-hidkd-hidtree.md) FDO のアドレスを取得します。

```dbgcmd
0: kd> !hidkd.hidtree
HID Device Tree
...
FDO  VendorID:0x045E(Microsoft Corporation) ProductID:0x0745 Version:0x0634
!hidfdo 0xffffe00004f466e0
...
0: kd> !hidfdo 0xffffe00004f466e0
# FDO 0xffffe00004f466e0  (!devobj/!devstack)

  Name              : \Device\_HID00000002
  Vendor ID         : 0x045E(Microsoft Corporation)
  Product ID        : 0x0745
  Version Number    : 0x0634
  Is Present?       : Y
  Report Descriptor : !hidrd 0xffffe00004281a80 0x127
  Per-FDO IFR Log   : !rcdrlogdump HIDCLASS -a 0xFFFFE0000594D000

  Position in HID tree

  dt FDO_EXTENSION 0xffffe00004f46850
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HID の拡張機能](hid-extensions.md)

 

 






