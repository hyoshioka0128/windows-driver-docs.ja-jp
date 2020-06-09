---
title: usbkd. usbportmddevext
description: 結果のバグチェック0xFE として生成されたクラッシュダンプに存在する場合は、usbkd. usbportmddevext コマンドによって、usbkd _DEVICE_EXTENSION 構造が表示されます。
ms.assetid: 07DE5D4A-E909-4D9B-B906-B74C9CC8AE49
keywords:
- usbkd. usbportmddevext Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbportmddevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cc8d97c71f89d97501cafe1aba791587da82af51
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534683"
---
# <a name="usbkdusbportmddevext"></a>!usbkd.usbportmddevext


**! Usbkd. usbportmddevext**コマンドを実行すると、 **usbkd \_ が表示されます。\_** [**バグチェック 0xfe**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプに1つが存在する場合は、デバイス拡張構造。

```dbgcmd
!usbkd.usbportmddevext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="remarks"></a>注釈
-------

このコマンドは、[**バグチェック 0xfe: バグコード \_ USB \_ ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプファイルをデバッグする場合にのみ使用します。

<a name="examples"></a>例
--------

次に、 **! usbportmddevext**の出力例を示します。

```dbgcmd
1: kd> !analyze -v
*** ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.usbportmddevext
USBPORT.SYS DEVICE_EXTENSION DATA: 
Hcd FDO Extension:
Sig:4f444648 HFDO
CurrentPnpFunc: 0x00000008
PnpFuncHistoryIdx: 0x0000000d
CurrentPowerFunc: 0x00000000
PowerFuncHistoryIdx: 0x00000000
PnpLogIdx: 0x00000002
IoRequestCount: 0x00000007
IoRequestAsyncCallbackCount: 0xffffffff
IoRequestAllow: 0x00000000
Pnp Func History (idx 13)
...
[02] pnp 13 (0d) IRP_MN_FILTER_RESOURCE_REQUIREMENTS
[...
Power Func History (idx 0)
[01] pnp 255 (ff) ??? (x0) PowerDeviceUnspecified
...
    **Power and Wake -----------------------------------------------
    selective suspend:on (1)
    PowerFlags (00000080):
*---FDO---*
PMDebug: 0x00000000
MinAllocedBw: 0x00000000
MaxAllocedBw: 0x00000000
## ...

## XDPC HISTORY_UsbHcIntDpc

State History (idx 2)
EVENT, STATE, NEXT 
Log[3] @ 000000d9e7c615cc  
Ev_Xdpc_Worker       XDPC_DpcQueued          XDPC_Running            
## ...        

## XDPC HISTORY_UsbDoneDpc

State History (idx 0)
EVENT, STATE, NEXT 
Log[1] @ 000000d9e7c61774  
Ev_Xdpc_Worker       XDPC_DpcQueued          XDPC_Running            
## ...          

## XDPC HISTORY_UsbMapDpc

State History (idx 3)
EVENT, STATE, NEXT 
Log[4] @ 000000d9e7c6196c  
## ...         

## XDPC HISTORY_UsbIocDpc

State History (idx 0)
EVENT, STATE, NEXT 
Log[1] @ 000000d9e7c61b04  
Ev_Xdpc_Worker       XDPC_DpcQueued          XDPC_Running            
...           
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






