---
title: usbkd. usbportmddcontext
description: Usbkd. usbportmddcontext コマンドは、バグチェック0xFE の結果として生成されたクラッシュダンプに存在する場合、USBKD コンテキストデータを表示します。
ms.assetid: 774C7EAE-A33E-49A6-956F-C0791134C221
keywords:
- usbkd. usbportmddcontext Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbportmddcontext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8dc4c5e0a7363598dcee6a9e14f9c45389988330
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534849"
---
# <a name="usbkdusbportmddcontext"></a>!usbkd.usbportmddcontext


[**バグチェック 0xfe**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプに存在する場合、 **! usbkd. usbportmddcontext**コマンドは、usbkd コンテキストデータを表示します。

```dbgcmd
!usbkd.usbportmddcontext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="remarks"></a>注釈
-------

このコマンドは、[**バグチェック 0xfe: バグコード \_ USB \_ ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプファイルをデバッグする場合にのみ使用します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






