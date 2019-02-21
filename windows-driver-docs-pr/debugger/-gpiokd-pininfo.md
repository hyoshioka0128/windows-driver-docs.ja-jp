---
title: gpiokd.pininfo
description: Gpiokd.pininfo コマンドでは、指定した GPIO pin 情報を表示します。
ms.assetid: 67A8F87A-E1E4-42AC-B626-66C2CB177A61
keywords:
- デバッグ gpiokd.pininfo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.pininfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bccd5b8afe75e43404f04cbdffbb6c1ce15a7979
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536035"
---
# <a name="gpiokdpininfo"></a>!gpiokd.pininfo


**! Gpiokd.pininfo**コマンドは、指定した GPIO ピンに関する情報を表示します。

```dbgcmd
!gpiokd.pininfo PinAddress
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______PinAddress______"></span><span id="_______pinaddress______"></span><span id="_______PINADDRESS______"></span> *PinAddress*   
アドレス、 [ \_GPIO\_PIN\_情報\_エントリ](gpio-extensions.md#data-structures-used-by-the-gpio-commands)暗証番号 (pin) を表すデータ構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Gpiokd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[GPIO 拡張機能](gpio-extensions.md)

 

 






