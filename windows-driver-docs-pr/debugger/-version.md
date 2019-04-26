---
title: version
description: 拡張機能のバージョンでは、拡張 DLL のバージョン情報が表示されます。この拡張機能のコマンドは、バージョン (デバッガーのバージョンの表示) コマンドと混同しないでください。
ms.assetid: b6ca4b8c-d673-40c5-890f-3b92fbb99fae
keywords:
- Windows のデバッグ バージョン
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- version
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2353c12fe18e72756c46d75f9ea12f3bab8ae788
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341777"
---
# <a name="version"></a>!version


**! バージョン**拡張機能が拡張 DLL のバージョン情報が表示されます。

この拡張機能のコマンドと混同しないで、 [**バージョン (デバッガーのバージョンの表示)** ](version--show-debugger-version-.md)コマンド。

```dbgcmd
![ExtensionDLL.]version
```

## <a name="span-idddkversiondbgspanspan-idddkversiondbgspanparameters"></a><span id="ddk__version_dbg"></span><span id="DDK__VERSION_DBG"></span>パラメーター


<span id="_______ExtensionDLL______"></span><span id="_______extensiondll______"></span><span id="_______EXTENSIONDLL______"></span> *ExtensionDLL*   
拡張 DLL のバージョン番号が表示されることを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、ほとんどの拡張 Dll で使用できます。

<a name="remarks"></a>注釈
-------

拡張 DLL のバージョンがデバッガーのバージョンが一致しない場合は、エラー メッセージが表示されます。

この拡張機能のコマンドは、Windows XP と Windows の以降のバージョンでは機能しません。 バージョン情報を表示するには、使用、 [**バージョン (デバッガーのバージョンの表示)** ](version--show-debugger-version-.md)コマンド。

この拡張機能の元の目的は、DLL のバージョンでは、多くの拡張機能の不正確な結果は結果が一致しないのために、対象のバージョンが一致することを確認するでした。 新しい Dll は、この拡張機能は廃止されていますので、Windows のバージョンを 1 つだけの操作に制限がなくなりました。

 

 





