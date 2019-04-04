---
title: wdfkd.wdfusbinterface
description: Wdfkd.wdfusbinterface 拡張機能では、可能であり、現在の設定を含む、指定のカーネル モード ドライバー フレームワーク (KMDF) USB インターフェイス オブジェクトに関する情報が表示されます。
ms.assetid: 2c0788aa-adb0-4a51-9937-32c8d9e0c240
keywords:
- デバッグ wdfkd.wdfusbinterface Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfusbinterface
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 048d1627bfc40b613da7b859c06b56543a548747
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571330"
---
# <a name="wdfkdwdfusbinterface"></a>!wdfkd.wdfusbinterface


**! Wdfkd.wdfusbinterface**拡張機能には、可能であり、現在の設定を含む、指定のカーネル モード ドライバー フレームワーク (KMDF) USB インターフェイス オブジェクトに関する情報が表示されます。

```dbgcmd
!wdfkd.wdfusbinterface Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
USB の WDFUSBINTERFACE に型指定されたインターフェイス オブジェクトへのハンドル。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
任意。 返される情報の種類を変更する 16 進値。 既定値は、「0x0」です。 フラグは、次のビットの任意の組み合わせを指定できます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
表示は、各 KMDF の USB パイプ オブジェクトの I/O ターゲットのプロパティが含まれます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

 

 





