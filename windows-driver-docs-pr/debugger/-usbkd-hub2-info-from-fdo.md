---
title: usbkd.hub2_info_from_fdo
description: Usbkd.hub2_info_from_fdo コマンドでは、USB ハブに関する情報が表示されます。
ms.assetid: BB40AEDD-9FDF-43BE-A741-56D06BE2965C
keywords:
- デバッグ usbkd.hub2_info_from_fdo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.hub2_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 84912ddbe4cc9f21afcfd7489a4cae979e2e88d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539382"
---
# <a name="usbkdhub2infofromfdo"></a>!usbkd.hub2\_info\_from\_fdo


**! Usbkd.hub2\_情報\_から\_fdo**コマンドは、USB ハブに関する情報を表示します。

```dbgcmd
!usbkd.hub2_info_from_fdo FDO
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______FDO______"></span><span id="_______fdo______"></span> *FDO*   
USB ハブの機能のデバイス オブジェクト (FDO) のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

USB ハブに対する、FDO のアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
```

上記の出力で、ハブの FDO のアドレスは、推奨されるコマンドの引数として表示されます。 **! devstack ffffe00002320050**します。

今すぐに FDO のアドレスを渡す、 **! ハブ 2\_情報\_から\_fdo**コマンド。

```dbgcmd
0: kd> !usbkd.hub2_info_from_fdo ffffe00002320050
usbhubext
*****************************************************************************

FDO ffffe00002320050 PDO ffffe0000213c050 HubNumber# 3
dt USBHUB!_DEVICE_EXTENSION_HUB ffffe000023201a0
!usbhublog ffffe000023201a0
RemoveLock ffffe00002320668
FdoFlags ffffe00002320ba0

CurrentPowerIrp: System (0000000000000000) Device (0000000000000000)

ObjReferenceList: !usblist ffffe00002320b70, RL 
ExceptionList: !usblist ffffe00002321498, EL [Empty]
DmTimerListHead: !usblist ffffe00002321040, TL [Empty]
PdoRemovedListHead: !usblist ffffe00002321478, PL [Empty]
PdoPresentListHead: !usblist ffffe00002321468, PL 
WorkItemListHead: !usblist ffffe00002320c80, WI [Empty]
SshBusyListHead: !usblist ffffe00002320dc0, BL 


## PnP FUNC HISTORY (latest at bottom)

01. IRP_MN_QUERY_DEVICE_RELATIONS
...

## POWER FUNC HISTORY (latest at bottom)

01. IRP_MN_QUERY_POWER    - PowerSystemHibernate
...

## HARD RESET STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. HRE_Pause                       HReset_WaitReady                        HReset_Paused                           
...

## PNP STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. Ev_SYSTEM_POWER                 FDO_WaitPnpStop                         FDO_WaitPnpStop                         
...

## POWER STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. Ev_SET_POWER_S0                 FdoSx_Dx                                FdoWaitS0IoComplete_Dx                  
...

## BUS STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. BE_BusSuspend                   BS_BusPause                             BS_BusSuspend                           
...

SSH_EnabledStatus: [SSH_ENABLED_VIA_POWER_POLICY]

## SSH STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. SSH_Event_ResumeHubComplete     SSH_State_HubPendingResume              SSH_State_HubActive                     
...

## PORT DATA

PortData 1: !port2_info ffffe000021bf000 Port State = PS_WAIT_CONNECT PortChangeLock: 0, Pcq_State: Pcq_Run_Idle             
     PDO 0000000000000000 
...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






