---
title: usbkd.usbhublog
description: Usbkd.usbhublog コマンドは、USB ハブのデバッグ ログを表示します。
ms.assetid: DFDF595E-3452-40C2-A6C7-94FB8954002C
keywords:
- デバッグ usbkd.usbhublog Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhublog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75a1c337e4e50da85b10860b05d113f122845497
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340618"
---
# <a name="usbkdusbhublog"></a>!usbkd.usbhublog


**! Usbkd.usbhublog**コマンドは、USB ハブのデバッグ ログを表示します。

```dbgcmd
!usbkd.usbhublog DeviceExtension[, NumberOfEntries]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
USB ハブの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能のアドレス。

<span id="_______NumberOfEntries______"></span><span id="_______numberofentries______"></span><span id="_______NUMBEROFENTRIES______"></span> *NumberOfEntries*   
表示するログ エントリの数。 全体のログを表示するには、このパラメーターを-1 に設定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

USB ハブの FDO のデバイスの拡張機能のアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
      ...
```

上記の出力で推奨されるコマンドを確認できます **! devstack ffffe00002320050**します。 次のコマンドを入力します。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

上記の出力で`ffffe000023201a0`ハブの FDO のデバイスの拡張機能のアドレスになります。

今すぐに、デバイスの拡張機能のアドレスを渡す **! usbhublog**します。 この例では、2 番目の引数は、10 個のログ エントリを表示を制限します。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






