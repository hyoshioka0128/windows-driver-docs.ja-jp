---
title: usbkd.usbhcdpnp
description: Usbkd.usbhcdpnp コマンドは、USB ホスト コント ローラーまたはルート ハブのプラグ アンド プレイ (PnP) 状態の履歴を表示します。
ms.assetid: 1153F3C2-5878-4223-AA18-5AE6FA056851
keywords:
- usbkd.usbhcdpnp Windows Debugging
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdpnp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3a2ad2c4287a694f2ee39b5b1fd1b2df809a65e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527825"
---
# <a name="usbkdusbhcdpnp"></a>!usbkd.usbhcdpnp


**! Usbkd.usbhcdpnp**コマンドは、USB ホスト コント ローラーまたはルート ハブのプラグ アンド プレイ (PnP) 状態の履歴を表示します。

```dbgcmd
!usbkd.usbhcdpnp DeviceExtension
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

FDO の USB ホスト コント ローラーのデバイスの拡張機能のアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree

UHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe0000090c3d0
...
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! uhci\_情報 ffffe00001c8f1a0**します。

今すぐに、デバイスの拡張機能のアドレスを渡す、 **! usbhcdpnp**コマンド。

```dbgcmd
0: kd> !usbkd.usbhcdpnp ffffe00001c8f1a0

## PNP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvFDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted          
[02] EvFDO_IRP_MN_QBR_RH            PnpStarted          PnpStarted
```

ルート ハブの PDO のデバイスの拡張機能のアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
    RootHub !hub2_info ffffe00000d941a0 !devstack ffffe00000d94050
```

上記の出力で、コマンドの引数として表示されるルート ハブの FDO のアドレスを確認できます **! devstack ffffe00000d94050**します。 使用して、 [ **! devstack** ](-devstack.md)は PDO とデバイスの PDO 拡張機能のアドレスを検索するコマンド。

```dbgcmd
0: kd> !kdexts.devstack ffffe00000d94050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00000d94050  \Driver\usbhub     ffffe00000d941a0  0000006b
  ffffe00000ed4050  \Driver\usbuhci    ffffe00000ed41a0  USBPDO-2
```

上記の出力で確認できます、pdo ルート ハブのデバイスの拡張機能のアドレスが`ffffe00000ed41a0`します。

今すぐに、デバイスの拡張機能のアドレスを渡す、 **! usbhcdpnp**コマンド。

```dbgcmd
0: kd> !usbkd.usbhcdpnp ffffe00000ed41a0

## PNP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvPDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted          
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






