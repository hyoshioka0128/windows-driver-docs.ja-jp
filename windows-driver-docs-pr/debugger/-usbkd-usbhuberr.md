---
title: usbkd.usbhuberr
description: Usbkd.usbhuberr コマンドは、USB ハブ エラー レコードを表示します。
ms.assetid: 5BB87FA2-0531-400C-95B3-325EE4DDB649
keywords:
- デバッグ usbkd.usbhuberr Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhuberr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b1593b60ec2a846d5ea8703211ba5faaf9881921
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334063"
---
# <a name="usbkdusbhuberr"></a>!usbkd.usbhuberr


**! Usbkd.usbhuberr**コマンドは、USB ハブ エラー レコードを表示します。

```dbgcmd
!usbkd.usbhuberr StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**usbhub!\_ハブ\_例外\_レコード**構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

以下のアドレスを検索する 1 つの方法を示します、 **usbhub!\_ハブ\_例外\_レコード**します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
      ...
```

上記の出力で推奨されるコマンドを確認できます **! devstack ffffe00002320050**します。 次のコマンドを入力します。

```dbgcmd
0: kd> !kdexts.devstack ffffe000011f7050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe000011f7050  \Driver\usbhub     ffffe000011f71a0  0000006f
  ffffe00000a21050  \Driver\usbehci    ffffe00000a211a0  USBPDO-8
...
```

上記の出力で`ffffe000011f71a0`はハブの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能のアドレスです。 デバイスの拡張機能のアドレスを渡す[ **! usbkd.usbhubext**](-usbkd-usbhubext.md)します。

```dbgcmd
0: kd> !usbkd.usbhubext ffffe000011f71a0

FDO ffffe000011f7050 PDO ffffe00000a21050 HubNumber# 7
dt USBHUB!_DEVICE_EXTENSION_HUB ffffe000011f71a0
!usbhublog ffffe000011f71a0
RemoveLock ffffe000011f7668
FdoFlags ffffe000011f7ba0

CurrentPowerIrp: System (0000000000000000) Device (0000000000000000)

ObjReferenceList: !usblist ffffe000011f7b70, RL 
ExceptionList: !usblist ffffe000011f8498, EL [Empty]
...
```

上記の出力で`ffffe000011f8498`例外の一覧のアドレスです。 例外の一覧が空でない場合のアドレスが含まれます **\_ハブ\_例外\_レコード**構造体。


## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






