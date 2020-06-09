---
title: usbkd. usbbpd
description: Usbkd. usbbpbpd コマンドを実行すると、USB ポートに関する情報が表示されます。
ms.assetid: 41D5E65D-76C2-45E0-9AC7-C2B50D806935
keywords:
- usbkd. usbbpbpd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubpd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5f99c9bfe75c260e269f4cac5a5e9be43114d74b
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533991"
---
# <a name="usbkdusbhubpd"></a>!usbkd.usbhubpd


**! Usbkd. usbbpbpd**コマンドを実行すると、USB ポートに関する情報が表示されます。

```dbgcmd
!usbkd.usbhubpd StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbhub のアドレス** \_ハブ \_ ポートの \_ データ**構造。 これらの構造体のアドレスを取得するには、 [**! usbhubext**](-usbkd-usbhubext.md)を使用します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

Usbhub のアドレスを検索する方法の1つを次に示し**ます。 \_ハブ \_ ポート \_ データ**。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        ...
```

上記の出力には、推奨されるコマンドである**devstack ffffe00002320050**が表示されます。 次のコマンドを入力します。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

前の出力では、ハブの FDO のデバイス拡張機能のアドレスがであることがわかり `ffffe000023201a0` ます。

デバイス拡張機能のアドレスを[**! usbhubext**](-usbkd-usbhubext.md)コマンドに渡します。

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

前の出力で、 `ffffe000021bf000` は** \_ ハブ \_ ポート \_ データ**構造のアドレスです。 このアドレスを **! usbhubpd**に渡します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






