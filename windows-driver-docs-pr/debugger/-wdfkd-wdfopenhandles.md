---
title: wdfkd.wdfopenhandles
description: Wdfkd.wdfopenhandles 拡張機能では、指定した WDF デバイスで開いているすべてのハンドルに関する情報が表示されます。
ms.assetid: 9b62a80a-6f53-4581-98b7-8eb5f9f146c2
keywords:
- デバッグ wdfkd.wdfopenhandles Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfopenhandles
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0111d4dc776e69e36ef7daf0a93b63a55acd12cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536340"
---
# <a name="wdfkdwdfopenhandles"></a>! wdfkd.wdfopenhandles


**! Wdfkd.wdfopenhandles**拡張機能が、指定された WDF デバイスで開いているすべてのハンドルに関する情報を表示します。

```dbgcmd
!wdfkd.wdfopenhandles Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
Framework デバイス オブジェクト (WDFDEVICE) へのハンドル。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示する情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、「0x0」です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
ファイル オブジェクトのコンテキスト情報を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

 

 





