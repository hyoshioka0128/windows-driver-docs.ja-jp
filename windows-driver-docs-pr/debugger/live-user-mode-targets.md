---
title: ライブ ユーザーモード ターゲット
description: ライブ ユーザーモード ターゲット
ms.assetid: 2709dd01-6486-471d-afa1-a8441665da8d
keywords:
- デバッガーエンジン API、ターゲット、ユーザーモード
- デバッガーエンジン API, プロセスからの切断
- デバッガーエンジン API, プロセスオプション
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143d8c1e026d6c1928835f4c914601d956a9fb13
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534341"
---
# <a name="live-user-mode-targets"></a>ライブ ユーザーモード ターゲット


## <span id="ddk_live_user_mode_targets_dbx"></span><span id="DDK_LIVE_USER_MODE_TARGETS_DBX"></span>


このトピックに記載されているプロセスを作成およびアタッチする方法は、ローカルコンピューターと、プロセスサーバーを実行しているリモートコンピューターに使用できます。

ユーザーモードプロセスは、 [**Create process**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)または[**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)を使用して作成できます。このプロセスでは、特定のコマンドを実行してプロセスを作成します。 メソッド[**Attachprocess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-attachprocess)は、[デバッガーエンジン](introduction.md#debugger-engine)を既存のユーザーモードプロセスにアタッチするために使用できます。 [**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)と[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)は、新しいユーザーモードプロセスを作成し、同じコンピューター上のそのプロセスまたは別のユーザーモードプロセスにアタッチします。 [**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request)の[**デバッグ要求の \_ 追加の \_ \_ \_ 作成 \_ オプションの取得**](debug-request-get-additional-create-options.md)、[**デバッグ \_ 要求セットの追加の \_ \_ \_ 作成 \_ オプション**](debug-request-set-additional-create-options.md)、[**デバッグ \_ 要求 \_ セットローカルの暗黙的な \_ \_ \_ コマンド \_ ライン**](debug-request-set-local-implicit-command-line.md)を使用して、プロセスを作成するための既定のオプションをいくつか設定できます。

**メモ**   [**Waitforevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)メソッドが呼び出されるまで、エンジンはプロセスに完全にアタッチされません。 プロセスによってイベント (プロセス作成イベントなど) が生成された後にのみ、デバッガーセッションで使用できるようになります。 詳細については[、「デバッグセッションと実行モデル](debugging-session-and-execution-model.md)」を参照してください。

 

[**GetRunningProcessSystemIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getrunningprocesssystemids)メソッドは、コンピューター上で実行されているすべてのプロセスのプロセス id を返します。 特定のプログラムのプロセス ID は、 [**GetRunningProcessSystemIdByExecutableName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getrunningprocesssystemidbyexecutablename)を使用して見つけることができます。 プロセス ID が指定されている場合は、プロセスの説明が[**GetRunningProcessDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getrunningprocessdescription)によって返されます。

### <a name="span-idprocess_optionsspanspan-idprocess_optionsspanspan-idprocess_optionsspanprocess-options"></a><span id="Process_Options"></span><span id="process_options"></span><span id="PROCESS_OPTIONS"></span>処理オプション

プロセスオプションは、ユーザーモードプロセスにアタッチされるときのエンジンの動作の一部を決定します。これには、ターゲットプロセスによって作成された子プロセスにデバッガーエンジンが自動的にアタッチされるかどうか、およびエンジンが終了時にエンジンが実行する処理を指定します。 プロセスオプションの詳細については、「 [**DEBUG \_ process \_ XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-process-xxx) 」を参照してください。

プロセスオプションは、 [**Getprocessoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getprocessoptions)を使用して照会できます。 これらは、 [**Addprocessoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-addprocessoptions)、 [**removeprocessoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-removeprocessoptions)、および[**SetProcessOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setprocessoptions)を使用して変更できます。

### <a name="span-iddisconnecting_from_processesspanspan-iddisconnecting_from_processesspanspan-iddisconnecting_from_processesspandisconnecting-from-processes"></a><span id="Disconnecting_from_Processes"></span><span id="disconnecting_from_processes"></span><span id="DISCONNECTING_FROM_PROCESSES"></span>プロセスからの切断

エンジンがプロセスとの接続を切断するには、3つの方法があります。

1.  *Detach*。 プロセス内のすべてのスレッドを再開して、デバッグされなくなっても実行を継続できるようにします。 [**DetachCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-detachcurrentprocess)は、現在のプロセスからエンジンをデタッチし、 [**DetachProcesses**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-detachprocesses)はすべてのプロセスからエンジンをデタッチします。 すべてのターゲットでデタッチがサポートされていません。 ターゲットがデタッチをサポートしているかどうかを確認するために、デバッグ要求のターゲットとして[** \_ \_ \_ \_ デタッチできる**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-can-detach)[**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request)操作を使用できます。

2.  *Terminate*。 プロセスを強制終了します。 [**TerminateCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-terminatecurrentprocess)は現在のプロセスを終了し、 [**TerminateProcesses**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-terminateprocesses)はデバッガーセッションのすべてのプロセスを終了します。

3.  *破棄*します。 デバッグ中のプロセスの一覧からプロセスを削除します。 このプロセスは、オペレーティングシステムによってデバッグされていると見なされ、別のデバッガーがアタッチするか強制終了されるまで中断されたままになります。 [**AbandonCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-abandoncurrentprocess)は現在のプロセスを破棄します。

 

 





