---
title: usbkd. hub2_info_from_fdo
description: Hub2_info_from_fdo コマンドは、USB ハブに関する情報を表示します。
ms.assetid: BB40AEDD-9FDF-43BE-A741-56D06BE2965C
keywords:
- usbkd. hub2_info_from_fdo Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.hub2_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b116a63061d2613dea641e81786560e7df1be77
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534873"
---
# <a name="usbkdhub2_info_from_fdo"></a>! usbkd. hub2 \_ info \_ from \_ fdo


**Hub2 \_ info \_ from \_ FDO**コマンドは、USB ハブに関する情報を表示します。

```dbgcmd
!usbkd.hub2_info_from_fdo FDO
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______FDO______"></span><span id="_______fdo______"></span>*FDO*   
USB ハブの機能デバイスオブジェクト (FDO) のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

USB ハブの FDO のアドレスを検索する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
```

上記の出力では、ハブの FDO のアドレスが、提案されたコマンド **! devstack ffffe00002320050**の引数として表示されます。

ここで、FDO のアドレスを FDO コマンド** \_ \_ から \_ ! hub2 info**に渡します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






