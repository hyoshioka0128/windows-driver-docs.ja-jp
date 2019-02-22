---
title: ツールを強制終了します。
description: Kill ツール、kill.exe、1 つまたは複数のプロセスとそのすべてのスレッドを終了します。 このツールは、ローカル コンピューターで実行されているプロセスでのみ機能します。
ms.assetid: e1733a74-2a31-436f-87b8-e704b27b6f04
keywords: ツール、Kill.exe、kill.exe を強制終了します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48c7683249757252908f23d8e58b5ca7cafad884
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530389"
---
# <a name="kill-tool"></a>ツールを強制終了します。


Kill ツール、kill.exe、1 つまたは複数のプロセスとそのすべてのスレッドを終了します。 このツールは、ローカル コンピューターで実行されているプロセスでのみ機能します。

## <a name="span-idwheretogetkilltoolspanspan-idwheretogetkilltoolspanspan-idwheretogetkilltoolspanwhere-to-get-kill-tool"></a><span id="Where_to_get_Kill_Tool"></span><span id="where_to_get_kill_tool"></span><span id="WHERE_TO_GET_KILL_TOOL"></span>強制終了のツールの入手先


含まれている Kill.exe[ツールを Windows のデバッグ](index.md)します。

## <a name="span-idkilltoolcommand-lineoptionsspanspan-idkilltoolcommand-lineoptionsspanspan-idkilltoolcommand-lineoptionsspankill-tool-command-line-options"></a><span id="Kill_Tool_command-line_options"></span><span id="kill_tool_command-line_options"></span><span id="KILL_TOOL_COMMAND-LINE_OPTIONS"></span>ツールのコマンド ライン オプションを強制終了します。


```console
kill [/f] { PID | Pattern* }
```

### <a name="span-idddkkilltoolcommandsdtoolsspanspan-idddkkilltoolcommandsdtoolsspanparameters"></a><span id="ddk_kill_tool_commands_dtools"></span><span id="DDK_KILL_TOOL_COMMANDS_DTOOLS"></span>パラメーター

<span id="________f______"></span><span id="________F______"></span> **/f**   
確認を求めることがなく、プロセスの終了を強制します。 このオプションは、システム サービスなど、保護されたプロセスを終了する必要があります。

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
終了するタスクのプロセス id (PID) を指定します。

タスクの PID を検索するには、TaskList Microsoft Windows XP 以降を使用または[TList](tlist.md) Windows 2000 でします。

<span id="_______Pattern_"></span><span id="_______pattern_"></span><span id="_______PATTERN_"></span> <em>パターン</em>**\\***  
タスクまたはウィンドウの名前の全部または一部を指定します。 Kill ツールには、プロセス名またはウィンドウ名を持つパターンに一致するすべてのプロセスが終了します。 アスタリスクが必要です。

意図せず多数のプロセスまたはウィンドウの名前に一致パターンを使用する前に、 **tlist** *パターン*パターンをテストするコマンド。 参照してください[TList](tlist.md)詳細についてはします。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


次のコマンドは、名前が"myapp。"で始まるプロセスを終了します。

```console
kill myapp*
```

次のコマンドでは、プロセス ID (PID) が 2520 プロセスは終了します。

```console
kill 2520
```

次のコマンドで名前が始まるプロセスを終了します"マイ\*"。 確認のプロンプトは表示されません。 このコマンドは、このプロセスがシステム サービスの場合でも成功します。

```console
kill /f my*
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Windows 用デバッグ ツールに含まれるツール](extra-tools.md)

 

 






