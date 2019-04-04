---
title: CDB を使用してユーザー モード プロセスのデバッグ
description: CDB を使用して、実行中のプロセスにアタッチするまたは生成し、新しいプロセスにアタッチすることができます。
ms.assetid: 0C56F6B5-0FBC-45C9-8AB7-218C00F90521
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb91baee79002457419a060312d1dd06b1136db2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553653"
---
# <a name="span-iddebuggerdebuggingauser-modeprocessusingcdbspandebugging-a-user-mode-process-using-cdb"></a><span id="debugger.debugging_a_user-mode_process_using_cdb"></span>CDB を使用してユーザー モード プロセスのデバッグ


CDB を使用して、実行中のプロセスにアタッチするまたは生成し、新しいプロセスにアタッチすることができます。

## <a name="span-idattachingtoarunningprocessspanspan-idattachingtoarunningprocessspanspan-idattachingtoarunningprocessspanattaching-to-a-running-process"></a><span id="Attaching_to_a_Running_Process"></span><span id="attaching_to_a_running_process"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS"></span>実行中のプロセスへのアタッチ


### <a name="span-idcommandprompt1spanspan-idcommandprompt1spancommand-prompt"></a><span id="command_prompt1"></span><span id="COMMAND_PROMPT1"></span>コマンド プロンプト

コマンド プロンプト ウィンドウを実行中のプロセスにアタッチできます CDB を起動するときに。 次のコマンドのいずれかを使用します。

-   **cdb -p** *ProcessID*
-   **cdb -pn** *ProcessName*

場所*ProcessID*が実行中のプロセスのプロセス ID または*ProcessName*実行中のプロセスの名前を指定します。

コマンドライン構文の詳細については、[ **CDB コマンド ライン オプション**](cdb-command-line-options.md)を参照してください。

### <a name="span-idcdbcommandwindow1spanspan-idcdbcommandwindow1spancdb-command-window"></a><span id="cdb_command_window1"></span><span id="CDB_COMMAND_WINDOW1"></span>CDB コマンド ウィンドウ

使用して実行中のプロセスにアタッチすることができる場合、デバッガーが 1 つまたは複数のプロセスをデバッグは既に、 [ **.attach (プロセスにアタッチ)** ](-attach--attach-to-process-.md)コマンド。

常に、デバッガーは同時に、複数のターゲット プロセスを開始し、いくつかのスレッドの固定または中断しない限り、します。

場合、 [ **.attach** ](-attach--attach-to-process-.md)コマンドが成功すると、デバッガーが、指定されたプロセスに、次回のデバッガー実行コマンドの発行をアタッチします。 行でこのコマンド何回かを使用する場合実行を何度でも、このコマンドを使用すると、デバッガーによって要求される必要があります。

## <a name="span-idattachingtoarunningprocessnoninvasivelyspanspan-idattachingtoarunningprocessnoninvasivelyspanspan-idattachingtoarunningprocessnoninvasivelyspanattaching-to-a-running-process-noninvasively"></a><span id="Attaching_to_a_Running_Process_Noninvasively"></span><span id="attaching_to_a_running_process_noninvasively"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_NONINVASIVELY"></span>Noninvasively 実行中のプロセスにアタッチ


実行中のプロセスをデバッグし、わずかに干渉するかどうか、その実行には、プロセスをデバッグする必要があります[noninvasively](noninvasive-debugging--user-mode-.md)します。

### <a name="span-idcommandprompt2spanspan-idcommandprompt2spancommand-prompt"></a><span id="command_prompt2"></span><span id="COMMAND_PROMPT2"></span>コマンド プロンプト

Noninvasively CDB コマンドラインから実行中のプロセスをデバッグするには、指定、 **-pv**オプション、 **-p**オプション、および、次の構文で、プロセス ID。

**cdb -pv -p** *ProcessID*

または、noninvasively プロセス名を指定して実行中のプロセスをデバッグするには次の構文を代わりに使用します。

**cdb -pv -pn** *ProcessName*

いくつかその他の便利なコマンド ライン オプションがあります。 コマンドライン構文の詳細については、[ **CDB コマンド ライン オプション**](cdb-command-line-options.md)を参照してください。

### <a name="span-idcdbcommandwindow2spanspan-idcdbcommandwindow2spancdb-command-window"></a><span id="cdb_command_window2"></span><span id="CDB_COMMAND_WINDOW2"></span>CDB コマンド ウィンドウ

Noninvasively を入力して実行中のプロセスをデバッグすることができます、デバッガーが既にアクティブである場合、 [ **.attach v (プロセスにアタッチ)** ](-attach--attach-to-process-.md)コマンド。

使用することができます、 **.attach**かどうか、デバッガーは、1 つまたは複数のプロセスの invasively デバッグ既にコマンドします。

場合、 **.attach v**コマンドが成功すると、デバッガーは、次回のデバッガー実行コマンドを発行する、指定されたプロセスをデバッグします。 待合室デバッグ中に実行が許可されていないため、デバッガーが、一度に 1 つ以上のプロセスをデバッグできません noninvasively。 この制限を使用することを意味も、 **.attach v**コマンドことは、既存の干渉のデバッグ セッションあまり役に立ちません。

## <a name="span-idspawninganewprocessspanspan-idspawninganewprocessspanspan-idspawninganewprocessspanspawning-a-new-process"></a><span id="Spawning_a_New_Process"></span><span id="spawning_a_new_process"></span><span id="SPAWNING_A_NEW_PROCESS"></span>新しいプロセスを作成


CDB では、ユーザー モード アプリケーションを起動でき、その後、アプリケーションをデバッグすることができます。 アプリケーションは、名前によって指定されます。 (元のターゲット プロセスを開始した追加のプロセス) の子プロセスにデバッガーも自動的にアタッチすることができます。

デバッガーが (子プロセスとも呼ばれます) を作成するプロセスにデバッガーが作成していないプロセスよりも若干異なる方法で動作します。

標準ヒープ API を使用する代わりには、デバッガーが作成するプロセスは、特別なデバッグ ヒープを使用します。 使用して、デバッグ ヒープではなく標準ヒープを使用する子プロセスを強制することができます、\_いいえ\_デバッグ\_ヒープ[環境変数](general-environment-variables.md)または **-hd**コマンド ライン オプション。

また、対象アプリケーションは、デバッガーの子プロセスであるために、デバッガーのアクセス許可を継承します。 このアクセス許可には、それ以外の場合を実行できなかった特定のアクションを実行する対象のアプリケーションが有効にすることがあります。 たとえば、対象アプリケーションは保護されているプロセスを制御することにあります。

コマンド プロンプト ウィンドウで CDB を起動するときに、新しいプロセスを起動できます。 次のコマンドを入力します。

**cdb \[-o\]**  *ProgramName* **\[**<em>引数</em>**\]**

**-O**オプションにより、デバッガーの子プロセスにアタッチします。 いくつかその他の便利なコマンド ライン オプションがあります。 コマンドライン構文の詳細については、[ **CDB コマンド ライン オプション**](cdb-command-line-options.md)を参照してください。

入力して、新しいプロセスを作成するには、デバッガーは 1 つまたは複数のプロセスをデバッグして既に場合、 [ **(プロセスの作成) に関する**](-create--create-process-.md)コマンド。

デバッガーは常に対象プロセスを複数同時に開始、いくつかのスレッドの凍結または中断がない限り。

場合、 [**に関する**](-create--create-process-.md)コマンドが成功すると、デバッガーは、次回のデバッガー実行コマンドを発行する、指定されたプロセスを作成します。 行でこのコマンド何回かを使用する場合実行を何度でも、このコマンドを使用すると、デバッガーによって要求される必要があります。

使用して、アプリケーションの開始ディレクトリを制御することができます、 [ **.createdir (作成プロセス ディレクトリの設定)** ](-createdir--set-created-process-directory-.md)する前にコマンド[**に関する**](-create--create-process-.md). 使用することができます、 **.createdir-は**コマンドまたは **- noinh**ターゲット アプリケーションが、デバッガーのハンドルを継承するかどうかを制御するコマンド ライン オプション。

アクティブ化またはを使用して子プロセスのデバッグを非アクティブ化することができます、 [ **.childdbg (子プロセスのデバッグ)** ](-childdbg--debug-child-processes-.md)コマンド。

## <a name="span-idreattachingtoaprocessspanspan-idreattachingtoaprocessspanspan-idreattachingtoaprocessspanreattaching-to-a-process"></a><span id="Reattaching_to_a_Process"></span><span id="reattaching_to_a_process"></span><span id="REATTACHING_TO_A_PROCESS"></span>プロセスに再アタッチ


デバッガーでは、応答を停止したり、フリーズする場合、は、ターゲット プロセスに新しいデバッガーを添付できます。 このような状況でデバッガーをアタッチする方法の詳細については、[対象アプリケーションを再アタッチ](reattaching-to-the-target-application.md)を参照してください。

 

 





