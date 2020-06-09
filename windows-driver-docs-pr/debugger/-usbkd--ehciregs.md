---
title: usbkd. _ehciregs
description: Usbkd. _ehciregs コマンドを実行すると、USB EHCI ホストコントローラーの操作およびルートハブポートの状態レジスタが表示されます。
ms.assetid: BFD58E6B-BC51-4F2F-B597-8C815826F931
keywords:
- usbkd. _ehciregs Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciregs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e60507e8ccba9eb8b9aa6e5579e284828d85c1c
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534089"
---
# <a name="usbkd_ehciregs"></a>! usbkd。 \_ehciregs


**! Usbkd。 \_ehciregs**コマンドは、USB EHCI ホストコントローラーの操作およびルートハブポートの状態の登録を表示します。

```dbgcmd
!usbkd._ehciregs StructAddr[, NumPorts]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbehci のアドレス** \_HC \_ OPERATIONAL \_ REGISTER**構造体。 Usbehci のアドレスを検索するには** \_HC \_ OPERATIONAL \_ REGISTER**構造体を使用して、 [**! usbkd. usbhcdlist**](-usbkd-usbhcdlist.md)を使用します。

<span id="_______NumPorts______"></span><span id="_______numports______"></span><span id="_______NUMPORTS______"></span>*Numports*   
表示するルートハブポートステータスレジスタの数。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

Usbehci のアドレスを取得する方法の1つを次に示し**ます。 \_HC \_ OPERATIONAL \_ REGISTER**構造体。 最初に「 [**! usbkd. usbhcdlist**](-usbkd-usbhcdlist.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usbhcdlist
MINIPORT List @ fffff80001e5bbd0

## List of EHCI controllers

!drvobj ffffe00001fd33a0 dt USBPORT!_USBPORT_MINIPORT_DRIVER ...
...
02. Xxxx Corporation PCI: VendorID Xxxx DeviceID Xxxx RevisionId 0002
    !devobj ffffe00001ca1050
    !ehci_info ffffe00001ca11a0
    Operational Registers ffffd000228bf020
```

前の出力で、 ` ffffd000228bf020` は** \_ HC \_ OPERATIONAL \_ REGISTER**構造体のアドレスです。

ここで、構造体のアドレスをに渡し**ます。 \_ehciregs**。 この例では、2番目の引数によって、表示が2つのルートハブポートの状態レジスタに限定されます。

```dbgcmd
0: kd> !usbkd._ehciregs ffffd000228bf020, 2
*(ehci)HC_OPERATIONAL_REGISTER ffffd000228bf020
    USBCMD 00010001
    .HostControllerRun: 1
    .HostControllerReset: 0
    .FrameListSize: 0
    .PeriodicScheduleEnable: 0
    .AsyncScheduleEnable: 0
    .IntOnAsyncAdvanceDoorbell: 0
    .HostControllerLightReset: 0
    .InterruptThreshold: 1
    .ParkModeEnable: 0
    .ParkModeCount: 0

    USBSTS 00002008
    .UsbInterrupt: 0
    .UsbError: 0
    .PortChangeDetect: 0
    .FrameListRollover: 1
    .HostSystemError: 0
    .IntOnAsyncAdvance: 0
    ----
    .HcHalted: 0
    .Reclimation: 1
    .PeriodicScheduleStatus: 0
    .AsyncScheduleStatus: 0

    USBINTR 0000003f
    .UsbInterrupt: 1
    .UsbError: 1
    .PortChangeDetect: 1
    .FrameListRollover: 1
    .HostSystemError: 1
    .IntOnAsyncAdvance: 1
    PeriodicListBase dec8e000
    AsyncListAddr dec91000
    PortSC[0] 00001000
        PortConnect x0
        PortConnectChange x0
        PortEnable x0
        PortEnableChange x0
        OvercurrentActive x0
        OvercurrentChange x0
        ForcePortResume x0
        PortSuspend x0
        PortReset x0
        HighSpeedDevice x0
        LineStatus x0
        PortPower x1
        PortOwnedByCC x0
        PortIndicator x0
        PortTestControl x0
        WakeOnConnect x0
        WakeOnDisconnect x0
        WakeOnOvercurrent x0
    PortSC[1] 00001000
        PortConnect x0
        PortConnectChange x0
        PortEnable x0
        PortEnableChange x0
        OvercurrentActive x0
        OvercurrentChange x0
        ForcePortResume x0
        PortSuspend x0
        PortReset x0
        HighSpeedDevice x0
        LineStatus x0
        PortPower x1
        PortOwnedByCC x0
        PortIndicator x0
        PortTestControl x0
        WakeOnConnect x0
        WakeOnDisconnect x0
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






