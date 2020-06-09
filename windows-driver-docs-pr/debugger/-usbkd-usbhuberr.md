---
title: usbkd. usbkd
description: Usbkd. usbkd [r] コマンドを実行すると、USB ハブのエラーレコードが表示されます。
ms.assetid: 5BB87FA2-0531-400C-95B3-325EE4DDB649
keywords:
- usbkd. usbkd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhuberr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be0b24214a99f780b30b355fa51ffac7388b30a9
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534857"
---
# <a name="usbkdusbhuberr"></a>!usbkd.usbhuberr


**! Usbkd. usbkd r**コマンドを実行すると、USB ハブのエラーレコードが表示されます。

```dbgcmd
!usbkd.usbhuberr StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbhub のアドレス** \_ハブ \_ 例外 \_ レコード**の構造。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

Usbhub のアドレスを検索する方法の1つを次に示し**ます。 \_ハブ \_ 例外 \_ レコード**。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
      ...
```

上記の出力には、推奨されるコマンドである**devstack ffffe00002320050**が表示されます。 次のコマンドを入力します。

```dbgcmd
0: kd> !kdexts.devstack ffffe000011f7050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe000011f7050  \Driver\usbhub     ffffe000011f71a0  0000006f
  ffffe00000a21050  \Driver\usbehci    ffffe00000a211a0  USBPDO-8
...
```

前の出力で、 `ffffe000011f71a0` はハブの機能デバイスオブジェクト (FDO) のデバイス拡張機能のアドレスです。 デバイス拡張機能のアドレスを[**! usbhubext**](-usbkd-usbhubext.md)に渡します。

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

前の出力で、 `ffffe000011f8498` は例外リストのアドレスです。 例外リストが空でない場合は、 ** \_ ハブ \_ 例外 \_ レコード**構造のアドレスが含まれます。


## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






