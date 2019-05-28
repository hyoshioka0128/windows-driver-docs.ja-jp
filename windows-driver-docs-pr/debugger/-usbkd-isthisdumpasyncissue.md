---
title: usbkd.isthisdumpasyncissue
description: このコマンドは、クラッシュの原因が割り込み USB EHCI ホスト コント ローラーに関連付けられている非同期の高度な問題にするかどうかを確認する、0 xfe クラッシュ ダンプ ファイルを確認します。
ms.assetid: 1729E52F-F943-4062-94AC-7890C2E25EBF
keywords:
- デバッグ usbkd.isthisdumpasyncissue Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.isthisdumpasyncissue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b7799b3ecc66f8b22deab723b144a3a46293efc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334099"
---
# <a name="usbkdisthisdumpasyncissue"></a>!usbkd.isthisdumpasyncissue


**! Usbkd.isthisdumpasyncissue**コマンドによって生成された、クラッシュ ダンプ ファイルを確認します[**バグ チェック 0 xfe**](bug-check-0xfe--bugcode-usb-driver.md)上、クラッシュの原因が、割り込みをしたかどうかを確認するには、。USB EHCI ホスト コント ローラーに関連付けられている非同期の高度な問題です。

```dbgcmd
!usbkd.isthisdumpasyncissue
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>注釈
-------

結果として生成されたクラッシュ ダンプ ファイルをデバッグしている場合にのみ、このコマンドを使用して[ **0 xfe のバグ チェック。BUGCODE\_USB\_ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)します。

<a name="examples"></a>例
--------

出力の例を次に示します **! usbkd.isthisdumpasyncissue**します。

```dbgcmd
1: kd> !analyze -v
*** ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.isthisdumpasyncissue
This is *NOT* Async on Advance Issue because the EndPointData is NULL
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






