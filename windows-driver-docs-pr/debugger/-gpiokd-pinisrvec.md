---
title: gpiokd.pinisrvec
description: Gpiokd.pinisrvec コマンドでは、指定した pin の割り込みサービス ルーチン (ISR) のベクター情報が表示されます。
ms.assetid: 83D4C072-92B2-4F61-A099-0BA4F8255BE8
keywords:
- デバッグ gpiokd.pinisrvec Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.pinisrvec
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4cf71c9760f57ff8ad90eaa1bc7886419c64330b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558968"
---
# <a name="gpiokdpinisrvec"></a>!gpiokd.pinisrvec


**! Gpiokd.pinisrvec**コマンドには、指定した pin の割り込みサービス ルーチン (ISR) ベクターの情報が表示されます。

```dbgcmd
!gpiokd.bankinfo PinAddress
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______PinAddress______"></span><span id="_______pinaddress______"></span><span id="_______PINADDRESS______"></span> *PinAddress*   
アドレス、 [ \_GPIO\_PIN\_情報\_エントリ](gpio-extensions.md#data-structures-used-by-the-gpio-commands)暗証番号 (pin) を表すデータ構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Gpiokd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[GPIO 拡張機能](gpio-extensions.md)

 

 






