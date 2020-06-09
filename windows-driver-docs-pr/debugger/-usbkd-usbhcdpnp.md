---
title: usbkd. usbhcdpnp
description: Usbkd-usbhcdpnp コマンドは、USB ホストコントローラーまたはルートハブのプラグアンドプレイ (PnP) 状態の履歴を表示します。
ms.assetid: 1153F3C2-5878-4223-AA18-5AE6FA056851
keywords:
- usbkd. usbhcdpnp Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdpnp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f30706b958b3b6204e77bd9a0ce879b7a01033f8
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534863"
---
# <a name="usbkdusbhcdpnp"></a>!usbkd.usbhcdpnp


**! Usbkd-usbhcdpnp**コマンドを実行すると、USB ホストコントローラーまたはルートハブのプラグアンドプレイ (PnP) 状態の履歴が表示されます。

```dbgcmd
!usbkd.usbhcdpnp DeviceExtension
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

USB ホストコントローラーの FDO のデバイス拡張機能のアドレスを確認する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree

UHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe0000090c3d0
...
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
...
```

上記の出力では、FDO のデバイス拡張機能のアドレスが、 [DML](debugger-markup-language-commands.md)コマンド **! uhci \_ info ffffe00001c8f1a0**の引数として表示されます。

次に、デバイス拡張機能のアドレスを **! usbhcdpnp**コマンドに渡します。

```dbgcmd
0: kd> !usbkd.usbhcdpnp ffffe00001c8f1a0

## PNP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvFDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted          
[02] EvFDO_IRP_MN_QBR_RH            PnpStarted          PnpStarted
```

ルートハブの PDO のデバイス拡張機能のアドレスを確認する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
    RootHub !hub2_info ffffe00000d941a0 !devstack ffffe00000d94050
```

上記の出力には、コマンド **! devstack ffffe00000d94050**の引数として表示されるルートハブの FDO のアドレスが表示されます。 [**! Devstack**](-devstack.md)コマンドを使用して、pdo のアドレスと pdo デバイス拡張機能を検索します。

```dbgcmd
0: kd> !kdexts.devstack ffffe00000d94050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00000d94050  \Driver\usbhub     ffffe00000d941a0  0000006b
  ffffe00000ed4050  \Driver\usbuhci    ffffe00000ed41a0  USBPDO-2
```

前の出力では、ルートハブの PDO のデバイス拡張機能のアドレスがであることがわかり `ffffe00000ed41a0` ます。

次に、デバイス拡張機能のアドレスを **! usbhcdpnp**コマンドに渡します。

```dbgcmd
0: kd> !usbkd.usbhcdpnp ffffe00000ed41a0

## PNP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvPDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted          
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






