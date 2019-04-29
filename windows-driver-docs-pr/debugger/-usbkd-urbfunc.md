---
title: usbkd.urbfunc
description: Usbkd.urbfunc コマンドは、URB 関数のコードの名前を表示します。
ms.assetid: 111DD6CD-D7DB-4772-B6DD-8EA88587FD1F
keywords:
- デバッグ usbkd.urbfunc Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.urbfunc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: afbe8a9d5915483a3dbeae3f7ede46815c934dc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334119"
---
# <a name="usbkdurbfunc"></a>!usbkd.urbfunc


**! Usbkd.urbfunc**コマンド URB 関数のコードの名前を表示します。

```dbgcmd
!usbkd.urbfunc FunctionCode
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______FunctionCode______"></span><span id="_______functioncode______"></span><span id="_______FUNCTIONCODE______"></span> *FunctionCode*   
URB 関数のコードの 16 進値。 これらのコードは、usb.h で定義されます。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

出力の例を次に示します **! urbfunc**します。

```dbgcmd
0: kd> !usbkd.urbfunc 0xA

URB_FUNCTION_ISOCH_TRANSFER (0xA)
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






