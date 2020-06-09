---
title: usbkd. urbfunc
description: Usbkd. urbfunc コマンドは、URB 関数のコードの名前を表示します。
ms.assetid: 111DD6CD-D7DB-4772-B6DD-8EA88587FD1F
keywords:
- usbkd. urbfunc Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.urbfunc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1323dd2421891b344e9f32df9eba3a001cf1cbe
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534871"
---
# <a name="usbkdurbfunc"></a>!usbkd.urbfunc


**! Usbkd. urbfunc**コマンドは、URB 関数のコードの名前を表示します。

```dbgcmd
!usbkd.urbfunc FunctionCode
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______FunctionCode______"></span><span id="_______functioncode______"></span><span id="_______FUNCTIONCODE______"></span>*Functioncode*   
URB 関数のコードの16進数の値。 これらのコードは、usb .h で定義されています。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

**! Urbfunc**の出力の例を次に示します。

```dbgcmd
0: kd> !usbkd.urbfunc 0xA

URB_FUNCTION_ISOCH_TRANSFER (0xA)
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






