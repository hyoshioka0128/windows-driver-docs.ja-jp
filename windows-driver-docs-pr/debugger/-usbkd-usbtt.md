---
title: usbkd. usbkd
description: Usbkd. usbkd コマンドを実行すると、USBKD _TRANSACTION_TRANSLATOR 構造の情報が表示されます。
ms.assetid: 4D599BCE-C6C3-42B3-BDCE-EE9E47FA6AB7
keywords:
- usbkd. usbkd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbtt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2776a62be158c465832e698b18744733aa67fb56
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534677"
---
# <a name="usbkdusbtt"></a>!usbkd.usbtt


**! Usbkd. usbkd**コマンドを実行すると、 **usbkd \_ から情報が表示されます。トランザクション \_ 変換**の構造。

```dbgcmd
!usbkd.usbtt StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
**Usbport のアドレス。 \_トランザクション \_ 変換**の構造。 USB ホストコントローラーのトランザクショントランスレーターの一覧を取得するには、 [**usbhcdext**](-usbkd-usbhcdext.md)コマンドを使用します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

Usbport のアドレスを確認する方法の1つを次に示し**ます。 \_トランザクション \_ 変換**の構造。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

上記の出力では、FDO のデバイス拡張機能のアドレスが、 [DML](debugger-markup-language-commands.md)コマンドの引数として表示されます **! ehci \_ info ffffe00001ca11a0**です。

DML コマンドをクリックするか、デバイス拡張機能のアドレスを[**! usbhcdext**](-usbkd-usbhcdext.md)に渡して、のアドレスを取得 `GlobalTtListHead` します。 このアドレスを[**! usbkd. usbkd**](-usbkd-usblist.md)に渡します。このリストには、 ** \_ トランザクション \_ トランスレーター**構造体のアドレスが表示されます。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






