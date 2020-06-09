---
title: usbkd. usbkd
description: Usbkd. usbkd コマンドは、指定された PDO から開始し、ルートハブに戻る USB デバイスチェーンを表示します。
ms.assetid: 0D69E29E-3886-436F-B5EE-E4F297D9CE36
keywords:
- usbkd. usbkd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbchain
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f5d57b852e76e5261eb7bb35f4737ef10ab7472c
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534041"
---
# <a name="usbkdusbchain"></a>!usbkd.usbchain


**! Usbkd. usbkd**コマンドは、指定された PDO から開始し、ルートハブに戻る USB デバイスチェーンを表示します。

```dbgcmd
!usbkd.usbchain PDO
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______PDO______"></span><span id="_______pdo______"></span>*PDO*   
USB ハブに接続されているデバイスの物理デバイスオブジェクト (PDO) のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

USB デバイスの PDO のアドレスを検索する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

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

上記の出力では、PDO のアドレスは、推奨されるコマンドの引数である **! devstack ffffe00007c882a0**です。 PDO のアドレスを **! usbkd**に渡します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






