---
title: usbkd.usbchain
description: Usbkd.usbchain コマンドでは、指定の PDO から開始し、ルート ハブに戻ると、USB デバイス チェーンが表示されます。
ms.assetid: 0D69E29E-3886-436F-B5EE-E4F297D9CE36
keywords:
- デバッグ usbkd.usbchain Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbchain
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73c13d57af32bc852b650a829e9a5148b02adc2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334102"
---
# <a name="usbkdusbchain"></a>!usbkd.usbchain


**! Usbkd.usbchain**コマンドは、指定の PDO から開始し、ルート ハブに戻ると、USB デバイス チェーンを表示します。

```dbgcmd
!usbkd.usbchain PDO
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______PDO______"></span><span id="_______pdo______"></span> *PDO*   
USB ハブに接続されているデバイスの物理デバイス オブジェクト (PDO) のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

USB デバイスの PDO のアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
 kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        Port 1: !port2_info ffffe000021bf000 
        Port 2: !port2_info ffffe000021bfb40 
        Port 3: !port2_info ffffe000021c0680 !devstack ffffe00007c882a0
...
```

上記の出力では、PDO のアドレスは、推奨されるコマンドの引数 **! devstack ffffe00007c882a0**します。 PDO のアドレスを渡す **! usbkd.usbchain**します。

```dbgcmd
0: kd> !usbkd.usbchain ffffe00007c882a0

usbchain
*****************************************************************************
HUB PDO ffffe00007c882a0 on port 3 !usbhubext ffffe00007c883f0 ArmedForWake = 0
VID Xxxx PID Xxxx REV 0100  Xxxx Corporation
    HUB #3 FDO ffffe00002320050 , !usbhubext ffffe000023201a0  HWC_ARM=0
    ROOT HUB PDO(ext) @ffffe0000213c1a0
        ROOT HUB FDO @ffffe00001ca1050, !usbhcdext ffffe00001ca11a0 PCI Vendor:Device:...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






