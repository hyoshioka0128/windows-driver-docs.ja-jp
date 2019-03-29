---
title: usbkd._ehciqh
description: Usbkd._ehciqh コマンドは、usbehci _HCD_QUEUEHEAD_DESCRIPTOR 構造から情報を表示します。
ms.assetid: 52A1CF03-3B1D-4CC6-A4DD-3E73A7AB2F00
keywords:
- usbkd._ehciqh Windows Debugging
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciqh
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d43bef72e1d3aaa8b1e71d2ac77e6851a1bab6fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582200"
---
# <a name="usbkdehciqh"></a>!usbkd.\_ehciqh


**! Usbkd\_ 。ehciqh**コマンドからの情報を表示、 **usbehci!\_HCD\_QUEUEHEAD\_記述子**構造体。 非同期のエンドポイント (つまり、コントロールと一括エンドポイント) に関する情報を表示するのにには、このコマンドを使用します。

```dbgcmd
!usbkd._ehciqh StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**usbehci!\_HCD\_QUEUEHEAD\_記述子**構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






