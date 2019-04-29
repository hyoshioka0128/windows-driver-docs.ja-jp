---
title: .browse (ブラウザーにコマンドを表示)
description: .Browse コマンドは、新しいコマンドのブラウザー ウィンドウで、指定したコマンドの出力を表示します。
ms.assetid: 37822DDE-8AA8-4DB9-8213-08E73110ACE5
keywords:
- .browse (ブラウザーで表示コマンド) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .browse (Display Command in Browser)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dd1afe2fce86ecf029de4a78347922cf33ce820e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334671"
---
# <a name="browse-display-command-in-browser"></a>.browse (ブラウザーにコマンドを表示)


**.Browse**コマンドでは、指定したコマンドの出力を表示、新しい[コマンド ブラウザー ウィンドウ](command-browser-window.md)します。

```dbgcmd
.browse Command
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*コマンド*  
新しいコマンドのブラウザー ウィンドウに表示および実行するコマンドです。

<a name="remarks"></a>注釈
-------

次の例では、 **.browse**コマンドの出力を表示する、 [ **.chain/D** ](-chain--list-debugger-extensions-.md)コマンド ブラウザーのウィンドウでコマンド。

```dbgcmd
.browse .chain /D
```

 

 





