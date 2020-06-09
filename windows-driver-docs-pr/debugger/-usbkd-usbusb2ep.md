---
title: usbusb2ep
description: Usbusb2ep コマンドは、usbkd _USB2_EP 構造の情報を表示します。
ms.assetid: 0298D7A2-C121-4B09-8542-CCD10323D573
keywords:
- usbusb2ep Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbusb2ep
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7d05a661eebec928addc75f5ac71f666db2c61a9
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533979"
---
# <a name="usbkdusbusb2ep"></a>!usbkd.usbusb2ep


**Usbusb2ep**コマンドは、 **usbkd \_ から情報を表示します。USB2 \_ EP**構造体。

```dbgcmd
!usbkd.usbusb2ep StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
**Usbport のアドレス。 \_USB2 \_ EP**構造体。 Usbport のアドレスを取得するには** \_USB2 \_ EP**構造体を使用して、 [**! usbkd. usb2**](-usbkd-usb2.md)を使用します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






