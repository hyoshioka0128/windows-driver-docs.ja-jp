---
title: usbkd.usbportmddcontext
description: Usbkd.usbportmddcontext コマンドを表示し、USBPORT コンテキスト データがバグの結果として生成されたクラッシュ ダンプに存在する場合は、0 xfe を確認します。
ms.assetid: 774C7EAE-A33E-49A6-956F-C0791134C221
keywords:
- usbkd.usbportmddcontext Windows Debugging
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbportmddcontext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b50928970c5041158147bed443dedd2fc8a850d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328005"
---
# <a name="usbkdusbportmddcontext"></a>!usbkd.usbportmddcontext


**! Usbkd.usbportmddcontext**コマンドの結果として生成されたクラッシュ ダンプである場合にし、USBPORT コンテキスト データを表示します[**バグ チェック 0 xfe**](bug-check-0xfe--bugcode-usb-driver.md)します。

```dbgcmd
!usbkd.usbportmddcontext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>注釈
-------

結果として生成されたクラッシュ ダンプ ファイルをデバッグしている場合にのみ、このコマンドを使用して[ **0 xfe のバグ チェック。BUGCODE\_USB\_ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






