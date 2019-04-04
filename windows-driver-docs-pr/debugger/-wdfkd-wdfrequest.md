---
title: wdfkd.wdfrequest
description: Wdfkd.wdfrequest 拡張機能では、指定のフレームワークの要求オブジェクトと、要求オブジェクトに関連付けられている WDM I/O 要求パケット (IRP) に関する情報が表示されます。
ms.assetid: 8b99ec30-ac2b-421d-8b20-bfbd09d41dfb
keywords:
- デバッグ wdfkd.wdfrequest Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfrequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 784bb0cb42b3726094b018d7f2f6e737c285affa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578680"
---
# <a name="wdfkdwdfrequest"></a>!wdfkd.wdfrequest


**! Wdfkd.wdfrequest**拡張機能が、指定のフレームワークの要求オブジェクトと、要求オブジェクトに関連付けられている WDM I/O 要求パケット (IRP) に関する情報を表示します。

```dbgcmd
!wdfkd.wdfrequest Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
フレームワークの要求オブジェクトへのハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

 

 





