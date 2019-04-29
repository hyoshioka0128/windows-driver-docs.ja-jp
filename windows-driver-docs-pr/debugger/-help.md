---
title: ヘルプ
description: ヘルプの拡張機能では、拡張 DLL からエクスポートされた拡張機能のコマンドについて説明するヘルプ テキストが表示されます。
ms.assetid: 9d01856e-4906-43cb-a445-71cce011a973
keywords:
- Windows デバッグ ヘルプ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- help
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b22a2d256a9ae0ee36489dd2704c1fde5788cbe6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336516"
---
# <a name="help"></a>!help


**! ヘルプ**拡張機能が拡張 DLL からエクスポートされた拡張機能のコマンドについて説明するヘルプ テキストを表示します。

この拡張機能のコマンドとを混同しないでください、 [**でしょうか。(コマンドのヘルプ)** ](---command-help-.md)または[ **(Meta-Command ヘルプ) の .help** ](-help--meta-command-help-.md)コマンド。

```dbgcmd
![ExtensionDLL.]help [-v] [CommandName] 
```

## <a name="span-idddkhelpdbgspanspan-idddkhelpdbgspanparameters"></a><span id="ddk__help_dbg"></span><span id="DDK__HELP_DBG"></span>パラメーター


<span id="_______ExtensionDLL______"></span><span id="_______extensiondll______"></span><span id="_______EXTENSIONDLL______"></span> *ExtensionDLL*   
指定された拡張 DLL のヘルプを表示します。 .Dll ファイル名拡張子を除いた、拡張 DLL の名前を入力します。 DLL ファイルが拡張機能の検索パスでないかどうか (を使用して表示される[ **.chain (リスト デバッガー拡張)**](-chain--list-debugger-extensions-.md))、DLL ファイルへのパスが含まれます。 たとえば、uext.dll ヘルプを表示するには、次のように入力します **! uext.help**または **!** 。<em>パス</em>**\\winext\\uext.help**します。

省略した場合、 *ExtensionDLL*デバッガーは読み込まれた Dll の一覧で最初の拡張 DLL のヘルプ テキストを表示します。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
使用可能な最も詳細なヘルプ テキストが表示されます。 この機能は、すべての Dll ではサポートされていません。

<span id="_______CommandName______"></span><span id="_______commandname______"></span><span id="_______COMMANDNAME______"></span> *CommandName*   
指定されたコマンドのヘルプ テキストのみが表示されます。 すべての Dll またはすべてのコマンドは、この機能はサポートされていません。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、ほとんどの拡張 Dll でサポートされます。

<a name="remarks"></a>注釈
-------

いくつかの個々 のコマンドがまた表示ヘルプ テキストを使用する場合、 **/でしょうか。** または **-でしょうか。** コマンド名を持つパラメーター。

 

 





