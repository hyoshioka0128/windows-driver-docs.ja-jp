---
title: usbkd.usbhubpd
description: Usbkd.usbhubpd コマンドでは、USB ポートに関する情報が表示されます。
ms.assetid: 41D5E65D-76C2-45E0-9AC7-C2B50D806935
keywords:
- デバッグ usbkd.usbhubpd Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubpd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cdae55164518d2eebca7536d038f55a9d32fc61d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340608"
---
# <a name="usbkdusbhubpd"></a>!usbkd.usbhubpd


**! Usbkd.usbhubpd**コマンドは、USB ポートに関する情報を表示します。

```dbgcmd
!usbkd.usbhubpd StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**usbhub!\_ハブ\_ポート\_データ**構造体。 これらの構造体のアドレスを取得する[ **! usbhubext**](-usbkd-usbhubext.md)します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

以下のアドレスを検索する 1 つの方法を示します、 **usbhub!\_ハブ\_ポート\_データ**します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        ...
```

上記の出力で推奨されるコマンドを確認できます **! devstack ffffe00002320050**します。 次のコマンドを入力します。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

上記の出力で確認できます、ハブの FDO のデバイスの拡張機能のアドレスが`ffffe000023201a0`します。

デバイスの拡張機能のアドレスを渡す、 [ **! usbhubext** ](-usbkd-usbhubext.md)コマンド。

```dbgcmd
0: kd> !usbkd.usbhubext ffffe000023201a0

FDO ffffe00002320050 PDO ffffe0000213c050 HubNumber# 3
dt USBHUB!_DEVICE_EXTENSION_HUB ffffe000023201a0
!usbhublog ffffe000023201a0
RemoveLock ffffe00002320668
FdoFlags ffffe00002320ba0

CurrentPowerIrp: System (0000000000000000) Device (0000000000000000)
...
## PORT DATA

PortData 1: !port2_info ffffe000021bf000 Port State = PS_WAIT_CONNECT PortChangeLock: 0, Pcq_State: Pcq_Run_Idle             
     PDO 0000000000000000 
....
```

上記の出力で`ffffe000021bf000`のアドレスを**\_ハブ\_ポート\_データ**構造体。 このアドレスを渡す **! usbhubpd**します。

```dbgcmd
0: kd> !usbkd.usbhubpd ffffe000021bf000
PortNumber: 1
Parent Hub FDO ffffe00002320050
Device PDO <NULL>
dt USBHUB!_HUB_PORT_DATA ffffe000021bf000
dt USBHUB!_PORTDATA_FLAGS ffffe000021bf968

PortChangelist: !usblist ffffe000021bf1c8, CL [Empty]

## Port Indicators Log (latest at bottom)

##     Event           State                Next

    [EMPTY]

## Port Change Queue History (latest at bottom)

##     Event                State                    Next                     PcqEv_Suspend PcqEv_Resume  PcqEv_ChDone  Tag 

01. PCE_Resume           Pcq_Stop                 Pcq_Pause                              PcqEv_Reset   PcqEv_Reset   REQUEST_RESUME     
...          Pcq_Run_wBusy            Pcq_Run_Idle                                                                            

## Port Status History (latest at bottom)

##     Current State          Change Eve nt        PDO              CEOSP H/W Port REG Frame Inserted

01. PS_WAIT_CONNECT        REQUEST_PAUSE       0000000000000000 00000 100  Age:000 512498
...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






