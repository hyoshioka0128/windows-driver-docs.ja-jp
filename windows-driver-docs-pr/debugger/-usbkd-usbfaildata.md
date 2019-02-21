---
title: usbkd.usbfaildata
description: Usbkd.usbfaildata コマンドでは、格納されている USB デバイスの障害データ (該当する場合) が表示されます。
ms.assetid: 08FD3F82-73E3-4616-92EB-D562ECAB8A96
keywords:
- デバッグ usbkd.usbfaildata Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbfaildata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 55fdb43933f08d4ae24f466a86e3fbc99a74d167
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550969"
---
# <a name="usbkdusbfaildata"></a>!usbkd.usbfaildata


**! Usbkd.usbfaildata**コマンドが格納されている USB デバイスの障害データ (該当する場合) を表示します。

```dbgcmd
!usbkd.usbfaildata PDO
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______PDO______"></span><span id="_______pdo______"></span> *PDO*   
USB ハブに接続されているデバイスの物理デバイス オブジェクト (PDO) のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

USB デバイスの PDO のアドレスを検索する 1 つの方法を次に示します。 入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

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

上記の出力で PDO のアドレスは、推奨されるコマンドの引数として表示されます。 **! devstack ffffe00007c882a0**します。

今すぐに PDO のアドレスを渡す **! usbkd.usbfaildata**します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






