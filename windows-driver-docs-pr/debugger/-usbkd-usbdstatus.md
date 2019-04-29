---
title: usbkd.usbdstatus
description: Usbkd.usbdstatus コマンドは、USBD ステータス コードの名前を表示します。
ms.assetid: 9983433E-1D17-47C6-972B-0A02B228A6AE
keywords:
- デバッグ usbkd.usbdstatus Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbdstatus
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed253e89d357651d2eb5dc6106ebb3adb2ab1c1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335593"
---
# <a name="usbkdusbdstatus"></a>!usbkd.usbdstatus


**! Usbkd.usbdstatus**コマンド USBD ステータス コードの名前を表示します。

```dbgcmd
!usbkd.usbdstatus StatusCode
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StatusCode______"></span><span id="_______statuscode______"></span><span id="_______STATUSCODE______"></span> *StatusCode*   
USBD ステータス コードの 16 進値。 これらのコードは、usb.h で定義されます。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

出力の例を次に示します **! usbdstatus**します。

```dbgcmd
1: kd> !usbkd.usbdstatus 0xC0000008

USBD_STATUS_DATA_OVERRUN (0xC0000008)
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






