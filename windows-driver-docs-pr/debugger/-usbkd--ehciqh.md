---
title: usbkd. _ehciqh
description: Usbehci コマンドを実行 _ehciqh すると、_HCD_QUEUEHEAD_DESCRIPTOR 構造の情報が表示されます。
ms.assetid: 52A1CF03-3B1D-4CC6-A4DD-3E73A7AB2F00
keywords:
- usbkd. _ehciqh Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciqh
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d8ca31c3ceca5482e3806af9433c8e33b577253b
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534881"
---
# <a name="usbkd_ehciqh"></a>! usbkd。 \_ehciqh


**! Usbkd。 \_ehciqh**コマンドを実行すると、usbehci からの情報が表示され**ます。 \_HCD \_ queuehead \_ 記述子**構造体。 このコマンドを使用して、非同期エンドポイント (つまり、コントロールと一括エンドポイント) に関する情報を表示します。

```dbgcmd
!usbkd._ehciqh StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbehci のアドレス** \_HCD \_ queuehead \_ 記述子**構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






