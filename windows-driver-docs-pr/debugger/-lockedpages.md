---
title: lockedpages
description: Lockedpages 拡張機能では、指定されたプロセスのドライバーがロックされているページが表示されます。
ms.assetid: a3f70b5f-350c-482f-a172-3abb2b22f408
keywords:
- ドライバーがロックされているページ
- Windows デバッグ lockedpages
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lockedpages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3716e6cfe9eae4d17759c226a1c5147cb2affb4d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336167"
---
# <a name="lockedpages"></a>!lockedpages


**! Lockedpages**拡張機能が指定されたプロセスのドライバーがロックされているページが表示されます。

構文

```dbgcmd
!lockedpages [Process]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *プロセス*   
プロセスを指定します。 場合*プロセス*は省略すると、現在のプロセスが使用されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

<a name="remarks"></a>注釈
-------

任意の時点での実行を停止するには、CTRL + BREAK (WinDbg) で、または (KD) では、CTRL + C キーを押します。

 

 





