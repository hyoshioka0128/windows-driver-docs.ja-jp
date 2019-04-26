---
title: usbkd.usbhubmddevext
description: Usbkd.usbhubmddevext コマンドでは、0 xfe のバグ チェックの結果として生成されたクラッシュ ダンプに存在する場合、usbhub _DEVICE_EXTENSION_HUB 構造が表示されます。
ms.assetid: 2A3C1AD4-0537-43B1-BD87-734047D242B9
keywords:
- デバッグ usbkd.usbhubmddevext Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubmddevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6a7fdfc915c9e7f8040a7c9841897c867ea278b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340622"
---
# <a name="usbkdusbhubmddevext"></a>!usbkd.usbhubmddevext


**! Usbkd.usbhubmddevext**コマンドが表示されます、 **usbhub!\_デバイス\_拡張子\_ハブ**構造の結果として生成されたクラッシュ ダンプに存在する場合、 [**バグ チェック 0 xfe**](bug-check-0xfe--bugcode-usb-driver.md)します。

```dbgcmd
!usbkd.usbhubmddevext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>注釈
-------

結果として生成されたクラッシュ ダンプ ファイルをデバッグしている場合にのみ、このコマンドを使用して[ **0 xfe のバグ チェック。BUGCODE\_USB\_ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






