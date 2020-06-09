---
title: usbkd. isit dumpasyncissue
description: このコマンドは、0xFE クラッシュダンプファイルをチェックして、クラッシュの原因として、USB EHCI ホストコントローラーに関連付けられた非同期の事前の問題が発生していないかどうかを確認します。
ms.assetid: 1729E52F-F943-4062-94AC-7890C2E25EBF
keywords:
- usbkd. isit dumpasyncissue Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.isthisdumpasyncissue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1939efedae2a1a0fbbc3b3d368f3de228b6c2a5
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534051"
---
# <a name="usbkdisthisdumpasyncissue"></a>!usbkd.isthisdumpasyncissue


**! Usbkd. isthe dumpasyncissue**コマンドは、[**バグチェック 0xfe**](bug-check-0xfe--bugcode-usb-driver.md)によって生成されたクラッシュダンプファイルをチェックして、クラッシュの原因として、USB EHCI ホストコントローラーに関連付けられている非同期の事前問題があるかどうかを確認します。

```dbgcmd
!usbkd.isthisdumpasyncissue
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="remarks"></a>注釈
-------

このコマンドは、[**バグチェック 0xfe: バグコード \_ USB \_ ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプファイルをデバッグする場合にのみ使用します。

<a name="examples"></a>例
--------

次に、 **! usbkd**の出力例を示します。

```dbgcmd
1: kd> !analyze -v
*** ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.isthisdumpasyncissue
This is *NOT* Async on Advance Issue because the EndPointData is NULL
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






