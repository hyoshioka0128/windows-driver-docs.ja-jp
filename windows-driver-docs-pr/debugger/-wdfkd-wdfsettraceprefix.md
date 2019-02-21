---
title: wdfkd.wdfsettraceprefix
description: Wdfkd.wdfsettraceprefix 拡張機能は、トレースのプレフィックスの書式指定文字列を設定します。
ms.assetid: dec47b55-4b6a-4ff5-8622-4a377a1903b8
keywords:
- デバッグ wdfkd.wdfsettraceprefix Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfsettraceprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ecafdceebd73e3ba57857389da8de38bf209148c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530092"
---
# <a name="wdfkdwdfsettraceprefix"></a>!wdfkd.wdfsettraceprefix


**! Wdfkd.wdfsettraceprefix**拡張機能は、トレースのプレフィックスの書式指定文字列を設定します。

```dbgcmd
!wdfkd.wdfsettraceprefix String
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *文字列*   
トレースのプレフィックス文字列。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

トレースのプレフィックス文字列の先頭は、カーネル モード ドライバー フレームワーク (KMDF) のエラー ログ内の各トレース メッセージに追加されます。 トレース\_形式\_プレフィックス環境変数は、トレースのプレフィックス文字列も制御します。

トレースのプレフィックス文字列の形式は、Microsoft Windows のトレース ツールによって定義されます。 この文字列とそれをカスタマイズする方法の詳細形式の詳細については、Windows Driver Kit (WDK) のドライバーの開発ツールのセクションでは「トレース メッセージのプレフィックス」トピックを参照してください。

 

 





