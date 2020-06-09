---
title: usbkd. _ehciframe
description: FrameListBaseAddress コマンドは、フレーム番号によってインデックス付けされた EHCI ミニポート定期リストエントリチェーンを表示し _ehciframe ます。
ms.assetid: 6359FC98-F070-410E-AFE7-C2C67A4F7C98
keywords:
- usbkd. _ehciframe Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciframe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7052fd160a57c80e347eadc4931b2736f81a20a3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534883"
---
# <a name="usbkd_ehciframe"></a>! usbkd。 \_ehciframe


**! Usbkd。 \_ehciframe**コマンドは、フレーム番号によってインデックス付けされた EHCI ミニポート FrameListBaseAddress 定期リストエントリチェーンを表示します。

```dbgcmd
!usbkd._ehciframe StructAddr, FrameNumber
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbehci のアドレス** \_デバイスの \_ データ**構造。

<span id="_______FrameNumber______"></span><span id="_______framenumber______"></span><span id="_______FRAMENUMBER______"></span>*FrameNumber*   
0 ~ 1023 の範囲のフレーム番号。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






