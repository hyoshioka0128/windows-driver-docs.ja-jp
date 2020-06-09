---
title: usbkd. usbhcdpow
description: Usbkd-usbhcdpow コマンドは、USB ホストコントローラーまたはルートハブの電源状態の履歴を表示します。
ms.assetid: 49D803E3-0D65-48D4-98C5-BFE4DB2C2985
keywords:
- usbkd. usbhcdpow Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdpow
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 31e996f7ccb1dd4a8754ce96285746524158ca43
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534861"
---
# <a name="usbkdusbhcdpow"></a>!usbkd.usbhcdpow


**! Usbkd-usbhcdpow**コマンドは、USB ホストコントローラーまたはルートハブの電源状態の履歴を表示します。

```dbgcmd
!usbkd.usbhcdpow DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
次のいずれかのアドレス。

-   USB ホストコントローラーの機能デバイスオブジェクト (FDO) のデバイス拡張機能。
-   物理デバイスオブジェクト (PDO) の USB ルートハブのデバイス拡張機能。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

EHCI ホストコントローラーの FDO のデバイス拡張機能のアドレスを確認する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
     ...
```

上記の出力では、FDO のデバイス拡張機能のアドレスが、 [DML](debugger-markup-language-commands.md)コマンドの引数として表示されます **! ehci \_ info ffffe00001ca11a0**です。

次に、デバイス拡張機能のアドレスを **! usbhcdpow**コマンドに渡します。

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

ルートハブの PDO のデバイス拡張機能のアドレスを確認する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        ...
```

上記の出力には、コマンド **! devstack ffffe00002320050**の引数として表示されるルートハブの FDO のアドレスが表示されます。 [**! Devstack**](-devstack.md)コマンドを使用して、pdo のアドレスと pdo デバイス拡張機能を検索します。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

前の出力では、ルートハブの PDO のデバイス拡張機能のアドレスがであることがわかり `ffffe0000213c1a0` ます。

次に、デバイス拡張機能のアドレスを **! usbhcdpow**コマンドに渡します。

```dbgcmd
0: kd> !usbkd.usbhcdpow ffffe0000213c1a0

dt USBPORT!_FDO_EXTENSION ffffe0000213c5a0

## State History (latest at bottom)

##      EVENT                              STATE                              NEXT

...
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






