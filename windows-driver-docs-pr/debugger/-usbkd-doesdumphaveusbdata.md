---
title: doesdumphaveusbdata
description: Doesdumphaveusbdata コマンドは、バグチェック0xFE の結果として生成された、クラッシュダンプファイルに含まれている USB データの種類を確認します。
ms.assetid: 5E475E9F-BC8E-4185-9F63-5BAD49A83904
keywords:
- doesdumphaveusbdata Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.doesdumphaveusbdata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64b776789a9cbc1cb4cf119b28b3773b28343fb3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534875"
---
# <a name="usbkddoesdumphaveusbdata"></a>!usbkd.doesdumphaveusbdata


**Doesdumphaveusbdata**コマンドは、[**バグチェック 0xfe**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成された、クラッシュダンプファイルに含まれている USB データの種類を確認します。

```dbgcmd
!usbkd.doesdumphaveusbdata
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="remarks"></a>注釈
-------

このコマンドは、[**バグチェック 0xfe: バグコード \_ USB \_ ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプファイルをデバッグする場合にのみ使用します。

<a name="examples"></a>例
--------

次に、 **! doesdumphaveusbdata**の出力の例を示します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






