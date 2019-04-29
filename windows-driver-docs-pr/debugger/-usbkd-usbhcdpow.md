---
title: usbkd.usbhcdpow
description: Usbkd.usbhcdpow コマンドは、ルート ハブまたは USB ホスト コント ローラーの電源状態の履歴を表示します。
ms.assetid: 49D803E3-0D65-48D4-98C5-BFE4DB2C2985
keywords:
- デバッグ usbkd.usbhcdpow Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdpow
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 29b6d960aa7e9a448bb44c68fb104d9962205766
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335573"
---
# <a name="usbkdusbhcdpow"></a>!usbkd.usbhcdpow


**! Usbkd.usbhcdpow**コマンドは、USB ホスト コント ローラーまたはルート ハブの電源状態の履歴を表示します。

```dbgcmd
!usbkd.usbhcdpow DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
次のいずれかのアドレス:

-   USB ホスト コント ローラーの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能。
-   物理デバイス オブジェクト (PDO) USB ルート ハブにデバイスの拡張機能。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

EHCI ホスト コント ローラーの FDO のデバイスの拡張機能のアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
     ...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! ehci\_情報 ffffe00001ca11a0**します。

今すぐに、デバイスの拡張機能のアドレスを渡す、 **! usbhcdpow**コマンド。

```dbgcmd
0: kd> !usbkd.usbhcdpow ffffe00001ca11a0

dt USBPORT!_FDO_EXTENSION ffffe00001ca15a0

## State History (latest at bottom)

##      EVENT                              STATE                              NEXT

[00] FdoPwrEv_D0_DoSetD0_2              FdoPwr_D0_WaitWorker2              FdoPwr_D0_WaitSyncUsb2               dt:0 ms
[01] FdoPwrEv_SyncUsb2_DoChirp          FdoPwr_D0_WaitSyncUsb2             FdoPwr_D0_WaitSyncUsb2               dt:0 ms
[02] FdoPwrEv_Rh_SetPowerSys            FdoPwr_D0_WaitSyncUsb2             FdoPwr_D0_WaitSyncUsb2               dt:0 ms
[03] FdoPwrEv_Rh_SetD0                  FdoPwr_D0_WaitSyncUsb2             FdoPwr_D0_WaitSyncUsb2               dt:0 ms
[04] FdoPwrEv_SyncUsb2_Complete         FdoPwr_D0_WaitSyncUsb2             FdoPwr_WaitSx                        dt:50 ms
[05] FdoPwrEv_Rh_Wake                   FdoPwr_WaitSx                      FdoPwr_WaitSx                        dt:3412 ms
[06] FdoPwrEv_Rh_Wake                   FdoPwr_WaitSx                      FdoPwr_WaitSx                        dt:283872 ms
[07] FdoPwrEv_Rh_Wake                   FdoPwr_WaitSx                      FdoPwr_WaitSx                        dt:25481267 ms
```

ルート ハブの PDO のデバイスの拡張機能のアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        ...
```

上記の出力で、コマンドの引数として表示されるルート ハブの FDO のアドレスを確認できます **! devstack ffffe00002320050**します。 使用して、 [ **! devstack** ](-devstack.md)は PDO とデバイスの PDO 拡張機能のアドレスを検索するコマンド。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

上記の出力で確認できます、pdo ルート ハブのデバイスの拡張機能のアドレスが`ffffe0000213c1a0`します。

今すぐに、デバイスの拡張機能のアドレスを渡す、 **! usbhcdpow**コマンド。

```dbgcmd
0: kd> !usbkd.usbhcdpow ffffe0000213c1a0

dt USBPORT!_FDO_EXTENSION ffffe0000213c5a0

## State History (latest at bottom)

##      EVENT                              STATE                              NEXT

...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






