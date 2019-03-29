---
title: usbkd.usbhubs
description: Usbkd.usbhubs コマンドでは、USB ハブに関する情報が表示されます。
ms.assetid: 88642A67-5105-45A4-8374-7E4D01FFAEB6
keywords:
- デバッグ usbkd.usbhubs Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a6dedc4cfee0966fa678e68f89c0c18c59c2fda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572642"
---
# <a name="usbkdusbhubs"></a>!usbkd.usbhubs


**! Usbkd.usbhubs**コマンドは、USB ハブに関する情報を表示します。

```dbgcmd
!usbkd.usbhubs a[v]
!usbkd.usbhubs x[v]
!usbkd.usbhubs r[v]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_____________a"></span><span id="_____________A"></span> **A**  
すべてのハブを表示します。

<span id="_____________r"></span><span id="_____________R"></span> **R**  
ルート ハブに表示されます。

<span id="_____________x"></span><span id="_____________X"></span> **X**  
外部ハブを表示します。

<span id="_____________v"></span><span id="_____________V"></span> **v**  
出力は、冗長です。 たとえば、 **! usbhubs rv**すべてのルート ハブに関する詳細な出力が表示されます。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>使用例
--------

詳細な出力の例を次に示します、 **! usbhubs**コマンド。

```dbgcmd
0: kd> !usbkd.usbhubs rv

args 'rv'
level: r v
ROOT HUBS
*LIST -- Root Hub List @ fffff8000217f440
*flink, blink ffffe000023215c0,ffffe000011f85c0
----------

[0] entry @: ffffe000023201a0
    !DevObj ffffe00002320050 !usbhubext ffffe000023201a0 
On Host Controller (0x8086, 0x293c) 
        Stat_AsyncResumeStartAt: 2437ee39d29bd498
        Stat_AsyncResumeCompleteAt: 24413c77d29bd498
        Stat_AsyncResume: 0x3c(60) ms
        Stat_SyncResumeStartAt: 2437ee39d29bd498
        Stat_SyncResumeCompleteAt: 2437ee39d29bd498
        Stat_SyncResume: 0x0(0) ms
Trap Regs: Event, Port, Event (ffffe000023204d0) 
    Enable: 0 Port: 0 Event 00000000
Hub Number: # 3
Number Of Ports: 4
dt usbhub!_USBHUB_FDO_FLAGS ffffe00002320ba0
>Is Root
>Power Switching: 
     No Power Switching 
>Overcurrent: 
     Global Overcurrent 
>PortIndicators: 
     No PortIndicators present
>AllowWakeOnConnect: 
     DO NOT WakeOnConnect
>CURRENT Hub Wake on Connectstate: 
     HWC_DISARM:- do not wake system on connect/disconnect event
>CURRENT Bus Wake state: 
     BUS_DISARM:- bus not armed for wake by this hub
>CURRENT Wake Detect state (WW Irp): 
     HUB_DISARM:- no ww irp pending (HUB_WAKESTATE_DISARMED)
Milliamps/Port : 500ma
Power caps (0 = not reported)
     PortPower_Registry : 0
     PortPower_DeviceStatus : 500
     PortPower_CfgDescriptor : 500
##      PortPower_HubStatus : 500

----------

[1] entry @: ffffe000008b91a0
    !DevObj ffffe000008b9050 !usbhubext ffffe000008b91a0 
On Host Controller (0x8086, 0x2937) 
...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






