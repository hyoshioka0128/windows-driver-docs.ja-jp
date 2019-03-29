---
title: wdfkd.wdfusbpipe
description: Wdfkd.wdfusbpipe 拡張機能には、カーネル モード ドライバー フレームワーク (KMDF) USB パイプ オブジェクトの I/O のターゲットに関する情報が表示されます。
ms.assetid: 6ae335c4-ac86-4f8c-b22d-cedad72e9cab
keywords:
- デバッグ wdfkd.wdfusbpipe Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfusbpipe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c93927292422ba96e9b22c827551d2aa0cac0662
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574711"
---
# <a name="wdfkdwdfusbpipe"></a>!wdfkd.wdfusbpipe


**! Wdfkd.wdfusbpipe**拡張機能は、カーネル モード ドライバー フレームワーク (KMDF) USB パイプ オブジェクトの I/O のターゲットに関する情報を表示します。

```dbgcmd
!wdfkd.wdfusbpipe Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
WDFUSBPIPE に型指定された USB パイプ オブジェクトへのハンドル。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
任意。 返される情報の種類を変更する 16 進値。 既定値は、「0x0」です。 フラグは、次のビットの任意の組み合わせを指定できます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
表示は、I/O ターゲットのプロパティが含まれます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

 

 





