---
title: usbkd.usbver
description: Usbkd.usbver コマンドでは、USB ドライバー スタックの USBD インターフェイスのバージョンが表示されます。
ms.assetid: E3F5A971-64FB-4826-8DC0-59F3615C106A
keywords:
- デバッグ usbkd.usbver Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0098679bab02db3486e2dc6f4128231744b3262
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327954"
---
# <a name="usbkdusbver"></a>!usbkd.usbver


**! Usbkd.usbver**コマンドは、USB ドライバー スタックの USBD インターフェイスのバージョンを表示します。

```dbgcmd
!usbkd.usbver
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>注釈
-------

USBD インターフェイスのバージョンの値が変数に格納されている`usbport!usbd_version`します。

<a name="examples"></a>例
--------

出力の例を次に示します **! usbkd.usbver**します。

```dbgcmd
1: kd> !usbkd.usbver

USBD VER 600 USB stack is VISTA
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

**USBD\_IsInterfaceVersionSupported**
 

 






