---
title: 実行プロセスの分析
description: 記録および分析の実行中のプロセスでは、ヒープ メモリの割り当てには、次のコマンドを使用します。 この分析は、スタック トレースについて説明します。
ms.assetid: 65a8b510-f5f1-4622-87ff-b44d5855787d
keywords:
- デバッグ実行プロセスの Windows を分析します。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Analyze a Running Process
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0abc7873df21e5fa570ddf7395257d21cf141dd3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354999"
---
# <a name="analyze-a-running-process"></a>実行プロセスの分析


記録および分析の実行中のプロセスでは、ヒープ メモリの割り当てには、次のコマンドを使用します。 この分析は、スタック トレースについて説明します。

```dbgcmd
umdh -p:PID [-f:LogFile] [-v[:MsgFile]] | [-g] | [-h]
```

## <a name="span-idddkanalyzearunningprocessdtoolsspanspan-idddkanalyzearunningprocessdtoolsspanparameters"></a><span id="ddk_analyze_a_running_process_dtools"></span><span id="DDK_ANALYZE_A_RUNNING_PROCESS_DTOOLS"></span>パラメーター


<span id="_______-p_PID______"></span><span id="_______-p_pid______"></span><span id="_______-P_PID______"></span> **-p:**<em>PID</em>   
分析するプロセスを指定します。 *PID*プロセスのプロセス ID です。 このパラメーターは必須です。

実行中のプロセスの PID を検索、タスク マネージャー、Tasklist、または[TList](tlist.md)します。

<span id="_______-f_LogFile______"></span><span id="_______-f_logfile______"></span><span id="_______-F_LOGFILE______"></span> **-f:**<em>LogFile</em>   
テキスト ファイルには、ログの内容を保存します。 既定では、UMDH は、stdout (コマンド ウィンドウ) にログを書き込みます。

*LogFile* (省略可能) のパスを指定し、ファイルの名前。 既存のファイルを指定する場合、UMDH は、ファイルを上書きします。

**注**   UMDH が管理者モード、または"protected"パスへの書き込み試行で開始されていない場合、アクセスが拒否されます。

 

<span id="_______-v__MsgFile_"></span><span id="_______-v__msgfile_"></span><span id="_______-V__MSGFILE_"></span> **-v\[:**<em>MsgFile</em>**\]**  
詳細モード。 生成情報の詳細とエラー メッセージ。 既定では、UMDH はこれらのメッセージを stderr に書き込みます。

*Msgfile が正しくありません*(省略可能) のパスを指定し、テキスト ファイルの名前。 この変数を使用すると、UMDH では、代わりに指定したファイルに詳細メッセージを stderr に書き込みます。 既存のファイルを指定する場合、UMDH は、ファイルを上書きします。

<span id="_______-g"></span><span id="_______-G"></span> **-g**  
プロセス (「ガベージ コレクション」) で参照されていないヒープ ブロックを記録します。

<span id="_______-h"></span><span id="_______-H"></span> **-h**  
ヘルプを表示します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Windows 2000、UMDH が、スタック トレースのデータベースの検索エラーを報告し、有効にした場合に、**ユーザー モードのスタック トレースのデータベースの作成**オプション[GFlags](gflags.md)、シンボル ファイルの競合がある可能性があります。 同じディレクトリにアプリケーションの DBG と PDB シンボル ファイルのコピーが問題を解決するには、もう一度やり直してください。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```dbgcmd
umdh -?
umdh -p:2230
umdh -p:2230  -f:dump_allocations.txt
umdh -p:2230 -f:c:\Log1.txt -v:c:\Msg1.txt
umdh -p:2230 -g -f:garbage.txt
```

 

 





