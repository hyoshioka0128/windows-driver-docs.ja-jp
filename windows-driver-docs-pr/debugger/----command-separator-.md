---
title: ;(コマンドの区切り記号)
description: セミコロン (;) 文字が 1 行に複数のコマンドを使用します。
ms.assetid: efa59a34-1d1d-4df4-bbb9-b8066c6f3b3c
keywords:
- ;(コマンドの区切り記号)Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ; (Command Separator)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b23f6eda8fb784bdd47231e454ae124c3e3039e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334864"
---
# <a name="-command-separator"></a>;(コマンドの区切り記号)


セミコロン ( **;** ) 文字が 1 行に複数のコマンドを使用します。

```dbgcmd
    Command1 ; Command2 [; Command3 ...] 
```

## <a name="span-idddktokencommandseparatordbgspanspan-idddktokencommandseparatordbgspanparameters"></a><span id="ddk_token_command_separator_dbg"></span><span id="DDK_TOKEN_COMMAND_SEPARATOR_DBG"></span>パラメーター


<span id="_______Command1__Command2__..."></span><span id="_______command1__command2__..."></span><span id="_______COMMAND1__COMMAND2__..."></span> *Command1*、 *Command2*、.  
実行されるコマンド。

<a name="remarks"></a>注釈
-------

コマンドが、右側に左から順番に実行されます。 1 行にすべてのコマンドは、特に明記しない限り、現在のスレッドを参照してください。 コマンドにより、スレッドの実行、デバッグ イベントをそのスレッドを停止するまでに、行の残りのコマンドが延期されます。

ごく少数のコマンドは、セミコロンで後にことはできません、引数としての行の残りの部分全体を自動的に受け取るためです。 以下の[ **(設定の別名) として**](as--as--set-alias-.md)、 [  **$ &lt; (スクリプト ファイルを実行)**](-----------------------a---run-script-file-.md)、  **$ &gt; &lt; (スクリプト ファイルを実行)**、任意のコマンドが始まると、 [  **\* (コメント行の指定子)** ](----comment-line-specifier-.md)トークンです。

次に例を示します。 123 のソース行の現在のプログラムを実行します。 これには、の値を出力**カウンター**、し、実行を再開します。

```console
0:000> g `:123`; ? poi(counter); g 
```

 

 





