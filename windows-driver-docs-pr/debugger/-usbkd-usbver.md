---
title: usbkd. usbkd
description: USBD インターフェイスバージョンの USB ドライバースタックが表示されます。
ms.assetid: E3F5A971-64FB-4826-8DC0-59F3615C106A
keywords:
- usbkd. usbkd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6c1fe4efe0c3c24c623e6e34819e5210a5a2ffb4
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533975"
---
# <a name="usbkdusbver"></a>!usbkd.usbver


**! Usbkd. usbkd**コマンドは、USB ドライバースタックの USBD インターフェイスバージョンを表示します。

```dbgcmd
!usbkd.usbver
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="remarks"></a>注釈
-------

USBD インターフェイスのバージョンの値は、変数に格納され `usbport!usbd_version` ます。

<a name="examples"></a>例
--------

次に、 **! usbkd. usbkd**の出力例を示します。

```dbgcmd
1: kd> !usbkd.usbver

USBD VER 600 USB stack is VISTA
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

**USBD \_ isinterfaceversionsupported**
 

 






