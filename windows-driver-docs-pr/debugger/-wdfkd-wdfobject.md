---
title: wdfkd.wdfobject
description: Wdfkd.wdfobject 拡張機能では、指定のフレームワーク オブジェクトに関する情報が表示されます。
ms.assetid: fee1b924-5437-4d15-b39c-4d0f6eba0a90
keywords:
- デバッグ wdfkd.wdfobject Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfobject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 138b2a052bbc932c66eee278cb7683494cde99ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574689"
---
# <a name="wdfkdwdfobject"></a>!wdfkd.wdfobject


**! Wdfkd.wdfobject**拡張機能は、指定のフレームワーク オブジェクトに関する情報を表示します。

```dbgcmd
!wdfkd.wdfobject FrameworkObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______FrameworkObject______"></span><span id="_______frameworkobject______"></span><span id="_______FRAMEWORKOBJECT______"></span> *FrameworkObject*   
Framework のオブジェクトへのポインター。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>コメント
-------

ドライバーのカーネル モード ドライバー フレームワーク (KMDF) 検証を有効にし、パブリック ハンドルの種類がから表示を追跡するためにマークされました、 **! wdfkd.wdfobject**拡張機能には、タグの追跡ツール (つまり、追跡オブジェクト) が含まれています。次の例では。

```dbgcmd
kd> !wdfobject 0x83584e38 

The type for object 0x83584e38 is FxDevice
State: FxObjectStateCreated (0x1)

!wdfhandle 0x7ca7b1c0

dt FxDevice 0x83584e38

    context:  dt 0x83584ff8 ROOT_CONTEXT (size is 0x1 bytes)
     <no associated attribute callbacks>

Object debug extension 83584e20
   !wdftagtracker 0x83722d80
   Verifier lock 0x831cefa8

   State history:
    [0] FxObjectStateCreated (0x1)
```

 

 





