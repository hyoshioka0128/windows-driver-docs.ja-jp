---
title: wdfkd.wdfwmi
description: Wdfkd.wdfwmi 拡張機能には、指定のフレームワークのデバイス オブジェクトの Microsoft Windows Management Instrumentation (WMI) の情報が表示されます。
ms.assetid: fd521be8-3c7a-415b-8044-c9fb25188cbc
keywords:
- デバッグ wdfkd.wdfwmi Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfwmi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e38c0934364eac907830fe1dacfcba2b599a4894
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574527"
---
# <a name="wdfkdwdfwmi"></a>!wdfkd.wdfwmi


**! Wdfkd.wdfwmi**拡張機能には、指定のフレームワークのデバイス オブジェクトの Microsoft Windows Management Instrumentation (WMI) の情報が表示されます。 この情報には、すべての WMI プロバイダー オブジェクトと、関連付けられた WMI インスタンス オブジェクトが含まれています。

```dbgcmd
!wdfkd.wdfwmi Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
Framework デバイス オブジェクトへのハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>コメント
-------

出力、 **! wdfkd.wdfwmi**拡張機能には、WMI の登録、プロバイダー、およびインスタンスに関する情報が含まれます。

 

 





