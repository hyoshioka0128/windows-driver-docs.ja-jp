---
title: bthkd.sdpnode
description: Bthkd.sdpnode コマンドでは、sdp ツリー内のノードに関する情報が表示されます。
ms.assetid: 3B5D1903-53C0-4FF5-8542-E419E555AFC1
keywords:
- デバッグ bthkd.sdpnode Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bthkd.sdpnode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0ad593186957459ae49dfa012180f206fecfb1e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578626"
---
# <a name="bthkdsdpnode"></a>!bthkd.sdpnode


**! Bthkd.sdpnode**コマンドが、sdp ツリー内のノードに関する情報を表示します。

```dbgsyntax
!bthkd.sdpnode addr [flags]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______addr______"></span><span id="_______ADDR______"></span> *addr*   
表示する sdp ツリー ノードのアドレス。

<span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
0x1 - recurse ノード

0x2 - 詳細

既定値は 0x0

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Bthkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[Bluetooth の拡張機能 (Bthkd.dll)](bluetooh-extensions--bthkd-dll-.md)

 

 






