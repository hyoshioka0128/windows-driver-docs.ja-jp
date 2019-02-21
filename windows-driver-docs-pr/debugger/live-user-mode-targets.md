---
title: ライブ ユーザー モードのターゲット
description: ライブ ユーザー モードのターゲット
ms.assetid: 2709dd01-6486-471d-afa1-a8441665da8d
keywords:
- エンジン API、ターゲット、ユーザー モードをデバッガーします。
- デバッガー エンジン API、プロセスから切断しています
- デバッガー エンジン API、処理オプション
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77e8334d317a916dd397891b8e77dbbee142c7ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550729"
---
# <a name="live-user-mode-targets"></a>ライブ ユーザー モードのターゲット


## <span id="ddk_live_user_mode_targets_dbx"></span><span id="DDK_LIVE_USER_MODE_TARGETS_DBX"></span>


ローカル コンピューターとプロセス サーバーを実行しているリモート コンピューターを作成して、このトピックに記載されているプロセスにアタッチする方法を使用できます。

使用してユーザー モード プロセスを作成できる[**プロセスの作成**](https://msdn.microsoft.com/library/windows/hardware/ff539321)または[ **CreateProcess2**](https://msdn.microsoft.com/library/windows/hardware/ff539323)を作成する特定のコマンドを実行する、プロセスです。 メソッド[ **AttachProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff538150)アタッチに使用できる、[デバッガー エンジン](introduction.md#debugger-engine)を既存のユーザー モード プロセスです。 [**CreateProcessAndAttach** ](https://msdn.microsoft.com/library/windows/hardware/ff540048)と[ **CreateProcessAndAttach2** ](https://msdn.microsoft.com/library/windows/hardware/ff540055)新しいユーザー モード プロセスを作成し、同じコンピューター上の別のユーザー モード プロセスにアタッチします。 [**要求**](https://msdn.microsoft.com/library/windows/hardware/ff554564)操作[**デバッグ\_要求\_取得\_追加\_作成\_オプション**](https://msdn.microsoft.com/library/windows/hardware/ff541553)、 [**デバッグ\_要求\_設定\_追加\_作成\_オプション**](https://msdn.microsoft.com/library/windows/hardware/ff541586)、および[**デバッグ\_要求\_設定\_ローカル\_暗黙的\_コマンド\_行**](https://msdn.microsoft.com/library/windows/hardware/ff541592)一部のプロセスを作成するための既定のオプションの設定を使用できます。

**注**  エンジンがまでプロセスにアタッチが完全に、 [ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)メソッドが呼び出されました。 プロセスは、- など、プロセス作成イベント - イベントを生成した後にのみになる場合が、デバッガー セッションで使用します。 参照してください[デバッグ セッションと実行モデル](debugging-session-and-execution-model.md)の詳細。

 

メソッド[ **GetRunningProcessSystemIds** ](https://msdn.microsoft.com/library/windows/hardware/ff548265)コンピューターで実行中のすべてのプロセスのプロセス Id が返されます。 使用して、特定のプログラムのプロセス ID を検出できる[ **GetRunningProcessSystemIdByExecutableName**](https://msdn.microsoft.com/library/windows/hardware/ff548254)します。 プロセス ID を指定するには、プロセスの説明がによって返される[ **GetRunningProcessDescription**](https://msdn.microsoft.com/library/windows/hardware/ff548243)します。

### <a name="span-idprocessoptionsspanspan-idprocessoptionsspanspan-idprocessoptionsspanprocess-options"></a><span id="Process_Options"></span><span id="process_options"></span><span id="PROCESS_OPTIONS"></span>処理オプション

デバッガー エンジンがターゲット プロセスと、エンジンが何をターゲットによって作成された子プロセスに自動的に関連付けるかどうかを含む、ユーザー モード プロセスにアタッチされている場合、エンジンの動作の一部を決定する処理オプションプロセスが終了する場合。 参照してください[**デバッグ\_プロセス\_XXX** ](https://msdn.microsoft.com/library/windows/hardware/ff541534)の処理オプションの説明。

処理オプションを使用して照会できます[ **GetProcessOptions**](https://msdn.microsoft.com/library/windows/hardware/ff548163)します。 使用して変更できる[ **AddProcessOptions**](https://msdn.microsoft.com/library/windows/hardware/ff537917)、 [ **RemoveProcessOptions**](https://msdn.microsoft.com/library/windows/hardware/ff554505)、および[ **SetProcessOptions**](https://msdn.microsoft.com/library/windows/hardware/ff556765)します。

### <a name="span-iddisconnectingfromprocessesspanspan-iddisconnectingfromprocessesspanspan-iddisconnectingfromprocessesspandisconnecting-from-processes"></a><span id="Disconnecting_from_Processes"></span><span id="disconnecting_from_processes"></span><span id="DISCONNECTING_FROM_PROCESSES"></span>プロセスから切断しています

プロセスから切断するエンジンの 3 つのさまざまな方法はあります。

1.  *デタッチ*します。 不要になったデバッグ中、実行を続行するために、プロセス内のすべてのスレッドを再開します。 [**DetachCurrentProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff541846) 、エンジン現在のプロセスからをデタッチし、 [ **DetachProcesses** ](https://msdn.microsoft.com/library/windows/hardware/ff541851)エンジンのすべてのプロセスからデタッチします。 デタッチをサポートしていないすべてのターゲット。 [**要求**](https://msdn.microsoft.com/library/windows/hardware/ff554564)操作[**デバッグ\_要求\_ターゲット\_できます\_デタッチ**](https://msdn.microsoft.com/library/windows/hardware/ff541602)ターゲットがデタッチをサポートしているかを確認するために使用できます。

2.  *終了*します。 プロセスを終了しようとしてください。 [**TerminateCurrentProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff558866)は現在のプロセスを終了し、 [ **TerminateProcesses** ](https://msdn.microsoft.com/library/windows/hardware/ff558867)デバッガー セッション側ですべてのプロセスを終了します。

3.  *破棄*します。 デバッグ中のプロセスの一覧から、プロセスを削除します。 オペレーティング システムは、デバッグ中とプロセスも考慮され、別のデバッガーが接続すると、またはが強制終了されたまで中断された、残ります。 [**AbandonCurrentProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff537786)現在のプロセスを中止します。

 

 





