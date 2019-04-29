---
title: usbkd._ehciframe
description: Usbkd._ehciframe コマンドでは、フレーム番号によって、EHCI ミニポート FrameListBaseAddress 定期的なリストのエントリのチェーンのインデックスが表示されます。
ms.assetid: 6359FC98-F070-410E-AFE7-C2C67A4F7C98
keywords:
- Windows デバッグ usbkd._ehciframe
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciframe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 72e79141fb1dd6b34cafe0eb666eea078ac33f35
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335595"
---
# <a name="usbkdehciframe"></a>!usbkd.\_ehciframe


**! Usbkd\_ 。ehciframe**コマンドは、フレーム番号によって EHCI ミニポート FrameListBaseAddress 定期的なリストのエントリのチェーンのインデックスを表示します。

```dbgcmd
!usbkd._ehciframe StructAddr, FrameNumber
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
アドレスを**usbehci!\_デバイス\_データ**構造体。

<span id="_______FrameNumber______"></span><span id="_______framenumber______"></span><span id="_______FRAMENUMBER______"></span> *FrameNumber*   
範囲 0 ~ 1023 のフレーム数。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






