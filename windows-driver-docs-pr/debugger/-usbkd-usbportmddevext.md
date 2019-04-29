---
title: usbkd.usbportmddevext
description: 場合 1 つし、usbport _DEVICE_EXTENSION 構造体はされたクラッシュ ダンプに存在する usbkd.usbportmddevext コマンドの表示は、0 xfe のバグ チェックでは、結果として生成します。
ms.assetid: 07DE5D4A-E909-4D9B-B906-B74C9CC8AE49
keywords:
- デバッグ usbkd.usbportmddevext Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbportmddevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fd1a1006d7cc08652a696506e38b191368ab2726
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327983"
---
# <a name="usbkdusbportmddevext"></a>!usbkd.usbportmddevext


**! Usbkd.usbportmddevext**コマンドが表示されます、**し、usbport!\_デバイス\_拡張子**、結果として生成されたクラッシュ ダンプに存在する場合に構造体[**バグ チェック 0 xfe**](bug-check-0xfe--bugcode-usb-driver.md)します。

```dbgcmd
!usbkd.usbportmddevext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>注釈
-------

結果として生成されたクラッシュ ダンプ ファイルをデバッグしている場合にのみ、このコマンドを使用して[ **0 xfe のバグ チェック。BUGCODE\_USB\_ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)します。

<a name="examples"></a>例
--------

出力の例を次に示します **! usbportmddevext**します。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






