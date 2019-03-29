---
title: usbkd._ehciregs
description: Usbkd._ehciregs コマンドは、運用が表示され、USB EHCI ホスト コント ローラーのルート ハブのポートの状態を登録します。
ms.assetid: BFD58E6B-BC51-4F2F-B597-8C815826F931
keywords:
- Windows デバッグ usbkd._ehciregs
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciregs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b81f63e35fd2c56f7c45fe2b252add571f01c3a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571593"
---
# <a name="usbkdehciregs"></a>! usbkd します。\_ehciregs


**! Usbkd\_ 。ehciregs**コマンドは、運用上を表示し、ハブのポート ステータス レジスタ USB EHCI ホスト コント ローラーのルートします。

```dbgcmd
!usbkd._ehciregs StructAddr[, NumPorts]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**usbehci!\_HC\_運用\_登録**構造体。 アドレスを検索する、 **usbehci!\_HC\_運用\_登録**構造体を使用して[ **! usbkd.usbhcdlist**](-usbkd-usbhcdlist.md)します。

<span id="_______NumPorts______"></span><span id="_______numports______"></span><span id="_______NUMPORTS______"></span> *NumPorts*   
表示するルート ハブのポートの状態の数を登録します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>使用例
--------

以下のアドレスを取得する 1 つの方法を示します、 **usbehci!\_HC\_運用\_登録**構造体。 最初に入力[ **! usbkd.usbhcdlist**](-usbkd-usbhcdlist.md)します。

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

上記の出力で` ffffd000228bf020`のアドレスを **\_HC\_運用\_登録**構造体。

今すぐに構造体のアドレスを渡す **!\_ehciregs**します。 この例では、2 番目の引数は、2 つのルート ハブのポートの状態をレジスタに表示を制限します。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






