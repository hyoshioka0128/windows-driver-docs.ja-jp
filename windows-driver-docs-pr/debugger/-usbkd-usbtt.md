---
title: usbkd.usbtt
description: Usbkd.usbtt コマンドは、し、USBPORT _TRANSACTION_TRANSLATOR 構造から情報を表示します。
ms.assetid: 4D599BCE-C6C3-42B3-BDCE-EE9E47FA6AB7
keywords:
- デバッグ usbkd.usbtt Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbtt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea628704feacbb584d83a36bd7355cf1587fe2cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327979"
---
# <a name="usbkdusbtt"></a>!usbkd.usbtt


**! Usbkd.usbtt**コマンドからの情報を表示、**し、USBPORT!\_トランザクション\_TRANSLATOR**構造体。

```dbgcmd
!usbkd.usbtt StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**し、usbport!\_トランザクション\_TRANSLATOR**構造体。 USB ホスト コント ローラーに対するトランザクション変換プログラムの一覧を取得する、 [ **! usbkd.usbhcdext** ](-usbkd-usbhcdext.md)コマンド。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

以下のアドレスを検索する 1 つの方法を示します、**し、usbport!\_トランザクション\_TRANSLATOR**構造体。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! ehci\_情報 ffffe00001ca11a0**します。

DML コマンドをクリックするか、デバイスの拡張機能のアドレスを渡す[ **! usbhcdext** ](https://msdn.microsoft.com/library/windows/hardware/dn367072)のアドレスを取得する`GlobalTtListHead`します。 そのアドレスを渡す[ **! usbkd.usblist**](-usbkd-usblist.md)のアドレスが表示されます**\_トランザクション\_TRANSLATOR**構造体。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






