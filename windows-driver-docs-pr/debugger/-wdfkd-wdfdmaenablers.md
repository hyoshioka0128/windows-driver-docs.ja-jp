---
title: wdfkd.wdfdmaenablers
description: Wdfkd.wdfdmaenablers 拡張機能は、指定したデバイス オブジェクトに関連付けられたすべての WDF ダイレクト メモリ アクセス (DMA) オブジェクトを表示します。
ms.assetid: 31b185e7-74d3-4329-b389-37279e5aa75c
keywords:
- デバッグ wdfkd.wdfdmaenablers Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdmaenablers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e021324d3d2ea7cc911331e73124920d9c57bfae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550971"
---
# <a name="wdfkdwdfdmaenablers"></a>!wdfkd.wdfdmaenablers


**! Wdfkd.wdfdmaenablers**拡張機能は、指定したデバイス オブジェクトに関連付けられたすべての WDF ダイレクト メモリ アクセス (DMA) オブジェクトを表示します。 また、関連付けられているトランザクションと共通のバッファー オブジェクトも表示されます。

```dbgcmd
!wdfkd.wdfdmaenablers Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
Framework デバイス オブジェクト (WDFDEVICE) へのハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

 

 





