---
title: usbkd. usbdstatus
description: USBD ステータスコードの名前は、usbkd. usbdstatus コマンドによって表示されます。
ms.assetid: 9983433E-1D17-47C6-972B-0A02B228A6AE
keywords:
- usbkd. usbdstatus Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbdstatus
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 412702d596f5d34d996eb6d9289b4b4e0d486c69
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534031"
---
# <a name="usbkdusbdstatus"></a>!usbkd.usbdstatus


**! Usbkd. usbdstatus**コマンドを実行すると、USBD 状態コードの名前が表示されます。

```dbgcmd
!usbkd.usbdstatus StatusCode
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StatusCode______"></span><span id="_______statuscode______"></span><span id="_______STATUSCODE______"></span>*StatusCode*   
USBD ステータスコードの16進数の値。 これらのコードは、usb .h で定義されています。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

次に、 **! usbdstatus**の出力例を示します。

```dbgcmd
1: kd> !usbkd.usbdstatus 0xC0000008

USBD_STATUS_DATA_OVERRUN (0xC0000008)
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






