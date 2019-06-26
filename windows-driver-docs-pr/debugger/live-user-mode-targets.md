---
title: ライブ ユーザーモード ターゲット
description: ライブ ユーザーモード ターゲット
ms.assetid: 2709dd01-6486-471d-afa1-a8441665da8d
keywords:
- エンジン API、ターゲット、ユーザー モードをデバッガーします。
- デバッガー エンジン API、プロセスから切断しています
- デバッガー エンジン API、処理オプション
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1bfd18496378245c97fbee204708a870bdf2276
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366486"
---
# <a name="live-user-mode-targets"></a>ライブ ユーザーモード ターゲット


## <span id="ddk_live_user_mode_targets_dbx"></span><span id="DDK_LIVE_USER_MODE_TARGETS_DBX"></span>


ローカル コンピューターとプロセス サーバーを実行しているリモート コンピューターを作成して、このトピックに記載されているプロセスにアタッチする方法を使用できます。

使用してユーザー モード プロセスを作成できる[**プロセスの作成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess)または[ **CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess2)を作成する特定のコマンドを実行する、プロセスです。 メソッド[ **AttachProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-attachprocess)アタッチに使用できる、[デバッガー エンジン](introduction.md#debugger-engine)を既存のユーザー モード プロセスです。 [**CreateProcessAndAttach** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)と[ **CreateProcessAndAttach2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)新しいユーザー モード プロセスを作成し、同じコンピューター上の別のユーザー モード プロセスにアタッチします。 [**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[**デバッグ\_要求\_取得\_追加\_作成\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-get-additional-create-options)、 [**デバッグ\_要求\_設定\_追加\_作成\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-set-additional-create-options)、および[**デバッグ\_要求\_設定\_ローカル\_暗黙的\_コマンド\_行**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-set-local-implicit-command-line)一部のプロセスを作成するための既定のオプションの設定を使用できます。

**注**  エンジンがまでプロセスにアタッチが完全に、 [ **WaitForEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)メソッドが呼び出されました。 プロセスは、- など、プロセス作成イベント - イベントを生成した後にのみになる場合が、デバッガー セッションで使用します。 参照してください[デバッグ セッションと実行モデル](debugging-session-and-execution-model.md)の詳細。

 

メソッド[ **GetRunningProcessSystemIds** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getrunningprocesssystemids)コンピューターで実行中のすべてのプロセスのプロセス Id が返されます。 使用して、特定のプログラムのプロセス ID を検出できる[ **GetRunningProcessSystemIdByExecutableName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getrunningprocesssystemidbyexecutablename)します。 プロセス ID を指定するには、プロセスの説明がによって返される[ **GetRunningProcessDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getrunningprocessdescription)します。

### <a name="span-idprocessoptionsspanspan-idprocessoptionsspanspan-idprocessoptionsspanprocess-options"></a><span id="Process_Options"></span><span id="process_options"></span><span id="PROCESS_OPTIONS"></span>処理オプション

デバッガー エンジンがターゲット プロセスと、エンジンが何をターゲットによって作成された子プロセスに自動的に関連付けるかどうかを含む、ユーザー モード プロセスにアタッチされている場合、エンジンの動作の一部を決定する処理オプションプロセスが終了する場合。 参照してください[**デバッグ\_プロセス\_XXX** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-process-xxx)の処理オプションの説明。

処理オプションを使用して照会できます[ **GetProcessOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getprocessoptions)します。 使用して変更できる[ **AddProcessOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-addprocessoptions)、 [ **RemoveProcessOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-removeprocessoptions)、および[ **SetProcessOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setprocessoptions)します。

### <a name="span-iddisconnectingfromprocessesspanspan-iddisconnectingfromprocessesspanspan-iddisconnectingfromprocessesspandisconnecting-from-processes"></a><span id="Disconnecting_from_Processes"></span><span id="disconnecting_from_processes"></span><span id="DISCONNECTING_FROM_PROCESSES"></span>プロセスから切断しています

プロセスから切断するエンジンの 3 つのさまざまな方法はあります。

1.  *デタッチ*します。 不要になったデバッグ中、実行を続行するために、プロセス内のすべてのスレッドを再開します。 [**DetachCurrentProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-detachcurrentprocess) 、エンジン現在のプロセスからをデタッチし、 [ **DetachProcesses** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-detachprocesses)エンジンのすべてのプロセスからデタッチします。 デタッチをサポートしていないすべてのターゲット。 [**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[**デバッグ\_要求\_ターゲット\_できます\_デタッチ**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-can-detach)ターゲットがデタッチをサポートしているかを確認するために使用できます。

2.  *終了*します。 プロセスを終了しようとしてください。 [**TerminateCurrentProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-terminatecurrentprocess)は現在のプロセスを終了し、 [ **TerminateProcesses** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-terminateprocesses)デバッガー セッション側ですべてのプロセスを終了します。

3.  *破棄*します。 デバッグ中のプロセスの一覧から、プロセスを削除します。 オペレーティング システムは、デバッグ中とプロセスも考慮され、別のデバッガーが接続すると、またはが強制終了されたまで中断された、残ります。 [**AbandonCurrentProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-abandoncurrentprocess)現在のプロセスを中止します。

 

 





