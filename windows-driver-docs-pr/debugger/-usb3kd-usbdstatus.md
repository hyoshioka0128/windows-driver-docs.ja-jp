---
title: usb3kd
description: Usb3kd 拡張機能によって、USBD 状態コードの名前が表示されます。
ms.assetid: B79B4E6E-7281-4BB0-9708-23F1462171BB
keywords:
- usb3kd Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.usbdstatus
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 84903b3200c021be75214d2d0307d6bd28bb3d57
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534897"
---
# <a name="usb3kdusbdstatus"></a>!usb3kd.usbdstatus


[**! Usb3kd**](-usb3kd-device-info.md)拡張機能は、USBD ステータスコードの名前を表示します。

```dbgcmd
!usb3kd.ucx_usbdstatus UrbStatus
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______UsbdStatus______"></span><span id="_______usbdstatus______"></span><span id="_______USBDSTATUS______"></span>*Usbdstatus*   
USBD ステータスコードの数値。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

USBD の状態コードは、Usb .h で定義されています。

<a name="examples"></a>例
--------

次の例では、数値0x80000200 を **! usbdstatus**コマンドに渡します。 このコマンドは、ステータスコード USBD \_ status INVALID URB 関数の名前を返し \_ \_ \_ ます。

```dbgcmd
3: kd> !usbdstatus 0x80000200
USBD_STATUS_INVALID_URB_FUNCTION (0x80000200)
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






