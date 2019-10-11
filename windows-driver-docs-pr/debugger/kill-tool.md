---
title: Kill ツール
description: Kill tool (eseutil.exe) は、1つ以上のプロセスとそのすべてのスレッドを終了します。 このツールは、ローカルコンピューター上で実行されているプロセスでのみ機能します。
ms.assetid: e1733a74-2a31-436f-87b8-e704b27b6f04
keywords: kill Tool、Kill .exe、kill
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc5c790095a05b9491d863c41954aed3c3f0dd13
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038087"
---
# <a name="kill-tool"></a>Kill ツール

Kill tool (eseutil.exe) は、1つ以上のプロセスとそのすべてのスレッドを終了します。 このツールは、ローカルコンピューター上で実行されているプロセスでのみ機能します。

## <a name="span-idwhere_to_get_kill_toolspanspan-idwhere_to_get_kill_toolspanspan-idwhere_to_get_kill_toolspanwhere-to-get-kill-tool"></a><span id="Where_to_get_Kill_Tool"></span><span id="where_to_get_kill_tool"></span><span id="WHERE_TO_GET_KILL_TOOL"></span>Kill ツールの入手場所

[Windows 用デバッグツール](index.md)には、Kill が含まれています。

## <a name="span-idkill_tool_command-line_optionsspanspan-idkill_tool_command-line_optionsspanspan-idkill_tool_command-line_optionsspankill-tool-command-line-options"></a><span id="Kill_Tool_command-line_options"></span><span id="kill_tool_command-line_options"></span><span id="KILL_TOOL_COMMAND-LINE_OPTIONS"></span>Kill Tool のコマンドラインオプション

```console
kill [/f] { PID | Pattern* }
```

### <a name="span-idddk_kill_tool_commands_dtoolsspanspan-idddk_kill_tool_commands_dtoolsspanparameters"></a><span id="ddk_kill_tool_commands_dtools"></span><span id="DDK_KILL_TOOL_COMMANDS_DTOOLS"></span>パラメータ

<span id="________f______"></span><span id="________F______"></span> **/f**ユーザーに確認のメッセージを表示せずに、プロセスを強制的に終了します。 このオプションは、システムサービスなどの保護されたプロセスを終了するために必要です。

<span id="_______PID______"></span><span id="_______pid______"></span>*PID*終了するタスクのプロセス識別子 (PID) を指定します。

タスクの PID を検索するには、Microsoft Windows XP 以降または Windows 2000 の[tlist.exe](tlist.md)で TaskList を使用します。

<span id="_______Pattern_"></span><span id="_______pattern_"></span><span id="_______PATTERN_"></span><em>パターン</em> **\***  
タスクまたはウィンドウの名前のすべてまたは一部を指定します。 Kill tool は、プロセス名またはウィンドウ名がパターンに一致するすべてのプロセスを終了します。 アスタリスクは必須です。

多くのプロセス名またはウィンドウ名が誤って一致する可能性があるパターンを使用する前に、 **tlist.exe** *pattern*コマンドを使用してパターンをテストします。 詳細については、 [tlist.exe](tlist.md)を参照してください。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例

名前が "myapp" で始まるプロセスを終了するコマンドを次に示します。

```console
kill myapp*
```

プロセス ID (PID) が2520であるプロセスを終了するコマンドを次に示します。

```console
kill 2520
```

次のコマンドは、名前が "my @ no__t-0" で始まるプロセスを終了します。 確認のプロンプトは表示されません。 このプロセスがシステムサービスの場合でも、このコマンドは成功します。

```console
kill /f my*
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[Windows 用デバッグツールに含まれるツール](extra-tools.md)
