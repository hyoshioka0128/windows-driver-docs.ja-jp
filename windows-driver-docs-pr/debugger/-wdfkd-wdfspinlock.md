---
title: wdfkd.wdfspinlock
description: Wdfkd.wdfspinlock 拡張機能には、フレームワークのスピン ロック オブジェクトに関する情報が表示されます。 この情報には、スピン ロックの取得の履歴と、ロックが保持されている時間の長さが含まれています。
ms.assetid: 73e74703-ed9b-460b-a798-41bb56942aa3
keywords:
- デバッグ wdfkd.wdfspinlock Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfspinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4f59ac337b4d830e36b8585afed03e343d23c005
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581861"
---
# <a name="wdfkdwdfspinlock"></a>!wdfkd.wdfspinlock


**! Wdfkd.wdfspinlock**拡張機能フレームワークのスピン ロック オブジェクトに関する情報を表示します。 この情報には、スピン ロックの取得の履歴と、ロックが保持されている時間の長さが含まれています。

```dbgcmd
!wdfkd.wdfspinlock Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
WDFSPINLOCK に型指定されたオブジェクトへのハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

 

 





