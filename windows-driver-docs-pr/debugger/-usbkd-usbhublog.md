---
title: usbkd. usbkd ブログ
description: Usbkd. usbkd blog コマンドを実行すると、USB ハブのデバッグログが表示されます。
ms.assetid: DFDF595E-3452-40C2-A6C7-94FB8954002C
keywords:
- usbkd. usbkd ブログ Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhublog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f70387f907ffec4f29e28a1ae96a06aa7c93344
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534695"
---
# <a name="usbkdusbhublog"></a>!usbkd.usbhublog


**! Usbkd ブログ**コマンドを実行すると、USB ハブのデバッグログが表示されます。

```dbgcmd
!usbkd.usbhublog DeviceExtension[, NumberOfEntries]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
USB ハブの機能デバイスオブジェクト (FDO) のデバイス拡張機能のアドレス。

<span id="_______NumberOfEntries______"></span><span id="_______numberofentries______"></span><span id="_______NUMBEROFENTRIES______"></span>*Numberofentries*   
表示するログエントリの数。 ログ全体を表示するには、このパラメーターを-1 に設定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

USB ハブの FDO のデバイス拡張機能のアドレスを確認する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
      ...
```

上記の出力には、推奨されるコマンドである**devstack ffffe00002320050**が表示されます。 次のコマンドを入力します。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

前の出力で、 `ffffe000023201a0` はハブの FDO のデバイス拡張機能のアドレスです。

次に、デバイス拡張機能のアドレスを **! usbのブログ**に渡します。 この例では、2番目の引数によって、表示が10個のログエントリに制限されます。

```dbgcmd
0: kd> !usbkd.usbhublog ffffe000023201a0, 10

LOG@: ffffe000023201a0 (usbhub!_DEVICE_EXTENSION_HUB)
>LOG mask = ff idx = ffffa333 (33)
*LOG: ffffe00002321ca0  LOGSTART: ffffe00002321640 *LOGEND: ffffe00002323620 # 20 
[ 000] ffffe00002321ca0 HDec 0000000000000000 ffffe000002904d0 0000000000000001 
[ 001] ffffe00002321cc0 HPCd 0000000000000000 0000000000000002 0000000000000004 
[ 002] ffffe00002321ce0 qwk- 0000000000000000 ffffe000021c11c0 0000000000000000 
[ 003] ffffe00002321d00 pq-- 0000000000000000 0000000000000002 0000000000000004 
[ 004] ffffe00002321d20 _6p4 0000000000000000 0000000000000000 0000000000000004 
[ 005] ffffe00002321d40 _6p1 0000000000000000 0000000000000003 0000000000000004 
[ 006] ffffe00002321d60 pq++ 0000000000000000 0000000000000003 0000000000000004 
[ 007] ffffe00002321d80 pq++ 0000000000000000 0000000000000006 0000000000000004 
[ 008] ffffe00002321da0 _6p0 0000000000000000 ffffe000021c11c0 0000000000000004 
[ 009] ffffe00002321dc0 pqDP 0000000000000000 ffffe000021c11d8 0000000000000006
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






