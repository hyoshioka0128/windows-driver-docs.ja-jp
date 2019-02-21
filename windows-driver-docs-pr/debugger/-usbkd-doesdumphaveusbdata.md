---
title: usbkd.doesdumphaveusbdata
description: Usbkd.doesdumphaveusbdata コマンドが生成されたクラッシュ ダンプ ファイルの USB データの種類を表示するためのバグ チェック 0 xfe。
ms.assetid: 5E475E9F-BC8E-4185-9F63-5BAD49A83904
keywords:
- デバッグ usbkd.doesdumphaveusbdata Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.doesdumphaveusbdata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e666bb7e3be9ac273da4b03f0bd974450217a37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558587"
---
# <a name="usbkddoesdumphaveusbdata"></a>!usbkd.doesdumphaveusbdata


**! Usbkd.doesdumphaveusbdata**コマンド ファイルをクラッシュ ダンプで USB のデータの種類を確認するためのチェックがの結果として生成された[**バグ チェック 0 xfe**](bug-check-0xfe--bugcode-usb-driver.md)します。

```dbgcmd
!usbkd.doesdumphaveusbdata
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>注釈
-------

結果として生成されたクラッシュ ダンプ ファイルをデバッグしている場合にのみ、このコマンドを使用して[ **0 xfe のバグ チェック。BUGCODE\_USB\_ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)します。

<a name="examples"></a>例
--------

出力の例を次に示します **! doesdumphaveusbdata**

```dbgcmd
1: kd> !analyze -v
*** ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.doesdumphaveusbdata

Retrieving crashdump information Please Wait...

Checking for GuidUsbHubPortArrayData information...
There is no data for this GUID in the mini dump.
No data to print  

Checking for GuidUsbHubExt information...
There is no data for this GUID in the mini dump.
No data to print  

Checking for GuidUsbPortLog information...
GuidUsbPortLog Exists with PORT Log Size = 8000 

Checking for GuidUsbPortContextData information...
GuidUsbPortContextData Exists with Data Length = 4c8 

Checking for GuidUsbPortExt information...
GuidUsbPortExt Exists (DEVICE_EXTENSION + DeviceDataSize ) = 2250
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






