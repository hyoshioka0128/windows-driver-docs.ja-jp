---
title: usbkd. usbfaildata
description: Usbkd. usbfaildata コマンドは、USB デバイス用に格納されているエラーデータ (存在する場合) を表示します。
ms.assetid: 08FD3F82-73E3-4616-92EB-D562ECAB8A96
keywords:
- usbkd. usbfaildata Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbfaildata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 743172ae48fef183451ef390d2e3d8d276a6739e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534025"
---
# <a name="usbkdusbfaildata"></a>!usbkd.usbfaildata


**! Usbkd. usbfaildata**コマンドは、USB デバイス用に保存されているエラーデータ (存在する場合) を表示します。

```dbgcmd
!usbkd.usbfaildata PDO
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______PDO______"></span><span id="_______pdo______"></span>*PDO*   
USB ハブに接続されているデバイスの物理デバイスオブジェクト (PDO) のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

USB デバイスの PDO のアドレスを検索する方法の1つを次に示します。 「 [**! Usbkd**](-usbkd-usb2tree.md)」と入力します。

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

上記の出力では、PDO のアドレスは、推奨されるコマンドの引数として、 **devstack ffffe00007c882a0**として表示されます。

次に、PDO のアドレスを **! usbkd. usbfaildata**に渡します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






