---
title: usb3kd.usbdstatus
description: Usb3kd.usbdstatus 拡張機能は、USBD ステータス コードの名前を表示します。
ms.assetid: B79B4E6E-7281-4BB0-9708-23F1462171BB
keywords:
- デバッグ usb3kd.usbdstatus Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.usbdstatus
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f66742efc8fbb18b9eb51c94d8247354dec7645e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558460"
---
# <a name="usb3kdusbdstatus"></a>!usb3kd.usbdstatus


[ **! Usb3kd.usbdstatus** ](-usb3kd-device-info.md)拡張子 USBD ステータス コードの名前を表示します。

```dbgcmd
!usb3kd.ucx_usbdstatus UrbStatus
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______UsbdStatus______"></span><span id="_______usbdstatus______"></span><span id="_______USBDSTATUS______"></span> *UsbdStatus*   
USBD ステータス コードの数値。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

USBD 状態コードは、Usb.h で定義されます。

<a name="examples"></a>例
--------

次の例では、渡す 0x80000200 数値を **! usbdstatus**コマンド。 コマンドは、状態コード、USBD の名前を返します\_状態\_無効な\_URB\_関数。

```dbgcmd
3: kd> !usbdstatus 0x80000200
USBD_STATUS_INVALID_URB_FUNCTION (0x80000200)
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






