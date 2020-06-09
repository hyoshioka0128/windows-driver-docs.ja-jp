---
title: usbhubmddevext
description: Usbhubmddevext コマンドは、バグチェック0xFE の結果として生成されたクラッシュダンプに存在する場合、usbhub _DEVICE_EXTENSION_HUB 構造体を表示します。
ms.assetid: 2A3C1AD4-0537-43B1-BD87-734047D242B9
keywords:
- usbhubmddevext Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubmddevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b82ae8a2c2108c8c5084ce01f48813f200039384
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534429"
---
# <a name="usbkdusbhubmddevext"></a>!usbkd.usbhubmddevext


**Usbhubmddevext**コマンドを実行すると、 **usbhub \_ が表示されます。\_ \_ ** [**バグチェック 0xfe**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプに1つが存在する場合は、デバイス拡張機能のハブ構造。

```dbgcmd
!usbkd.usbhubmddevext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="remarks"></a>注釈
-------

このコマンドは、[**バグチェック 0xfe: バグコード \_ USB \_ ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプファイルをデバッグする場合にのみ使用します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






