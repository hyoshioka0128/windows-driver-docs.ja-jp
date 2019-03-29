---
title: ローカル カーネルモード デバッグ
description: ローカル カーネルモード デバッグ
ms.assetid: e66dc23b-9254-4148-9828-d27c30bfa492
keywords:
- ローカル カーネル デバッグ
- ローカルのカーネルが使用可能なコマンドをデバッグします。
- ローカル カーネルのデバッグ、LiveKD ツール
- LiveKD ツール
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 755e0abd8fa9b095a81f7837a922dbf4988c4937
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579235"
---
# <a name="local-kernel-mode-debugging"></a>ローカル カーネルモード デバッグ


デバッグ ツールの Windows サポート*ローカル カーネル デバッグ*します。 これは、1 台のコンピューターでカーネル モードのデバッグです。 つまり、デバッガーは、デバッグ中のと同じコンピューターで実行されます。

## <a name="span-idstartinglocalkerneldebuggingspanspan-idstartinglocalkerneldebuggingspansetting-up-local-kernel-mode-debugging"></a><span id="starting_local_kernel_debugging"></span><span id="STARTING_LOCAL_KERNEL_DEBUGGING"></span>ローカル カーネル モード デバッグの設定


ローカル カーネル モードのデバッグをセットアップする方法については、次を参照してください。[ローカル カーネル モード デバッグのセットアップの 1 つのコンピューターを手動で](setting-up-local-kernel-debugging-of-a-single-computer-manually.md)します。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg を使用します。

WinDbg を管理者として開きます。 **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、**ローカル**タブ。**[OK]** をクリックします。

WinDbg に管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力してセッションを開始することもできます。

**windbg -kl**

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD を使用します。

管理者は、コマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

**kd kl**

## <a name="span-idcommandsthatarenotavailablespanspan-idcommandsthatarenotavailablespancommands-that-are-not-available"></a><span id="commands_that_are_not_available"></span><span id="COMMANDS_THAT_ARE_NOT_AVAILABLE"></span>コマンドは使用できません。


すべてのコマンドは、ローカル カーネル デバッグ セッションで使用できます。 通常、操作を再開することはできませんので、すぐにでもを停止する対象のコンピュータを原因となる任意のコマンドを使用することはできません。

具体的には、次のコマンドを使用することはできません。

-   などの実行コマンド**g (移動)**、 **p (ステップ)**、 **t (トレース)**、 **wt (トレースとデータの監視)**、 **tb (次へのトレースブランチ)**、 **gh (例外処理での移動)**、および**gn (Go 処理されない例外を使用)**

-   などのファイル、コマンドのシャット ダウンとダンプ **.crash**、 **.dump**、および **.reboot**

-   などのブレークポイント コマンド**bp**、 **bu**、 **ba**、 **bc**、 **bd**、**する**、および**bl**

-   コマンドの表示をよう登録**r**とバリエーション

-   スタック トレース コマンドのなど**k**とバリエーション

WinDbg でローカル カーネルのデバッグを実行する場合、対応するメニュー コマンドとボタンのすべてもご利用いただけません。

## <a name="span-idcommandsthatareavailablespanspan-idcommandsthatareavailablespancommands-that-are-available"></a><span id="commands_that_are_available"></span><span id="COMMANDS_THAT_ARE_AVAILABLE"></span>使用可能なコマンド


すべてのメモリの入力とコマンドの出力が可能です。 ユーザーのメモリとカーネル メモリから自由に参照できます。 メモリを記述することもできます。 書き、カーネル メモリの問題の一部を破損する場合があるためデータ構造体し、応答を停止するコンピューターの多くの場合、確認します (つまり、*クラッシュ*)。

## <a name="span-iddifficultiesinperforminglocalkerneldebuggingspanspan-iddifficultiesinperforminglocalkerneldebuggingspandifficulties-in-performing-local-kernel-debugging"></a><span id="difficulties_in_performing_local_kernel_debugging"></span><span id="DIFFICULTIES_IN_PERFORMING_LOCAL_KERNEL_DEBUGGING"></span>ローカル カーネル デバッグを実行するときに問題がある場合


ローカル カーネル デバッグは、非常に微妙な操作です。 注意が破損する使用したり、システムがクラッシュするはしないでください。

ローカル カーネル デバッグの最も困難な側面の 1 つは、マシンの状態が常に変化します。 メモリのページは、サインアウト、常に変化し、アクティブなプロセス、および定数残っていない仮想アドレスのコンテキスト。 ただし、これらの条件下では、緩やかに変化は、特定のデバイス状態などを変更することを効果的に分析できます。

カーネル モード ドライバーと Windows オペレーティング システムの多くの場合にメッセージを送信、カーネル デバッガーを使用して**による DbgPrint**および関連する関数。 これらのメッセージは、ローカル カーネル デバッグ中に自動的には表示されません。 使用してそれらを表示することができます、 [ **! による dbgprint** ](-dbgprint.md)拡張機能。

## <a name="span-idlivekdspanspan-idlivekdspanlivekd"></a><span id="livekd"></span><span id="LIVEKD"></span>LiveKD


LiveKD ツールでは、ローカル カーネル デバッグをシミュレートします。 このツールは、このスナップショットにしている間に、カーネルを実際に停止することがなく、カーネル メモリの「スナップショット」ダンプ ファイルを作成します。 (そのため、スナップショットがありますが表示されていないコンピューターの 1 つのインスタント状態です。)

Windows のツールをデバッグ パッケージの一部でない LiveKD します。 ダウンロードできる[LiveKd](https://go.microsoft.com/fwlink/p/?linkid=56552) Windows Sysinternals サイトからします。

 

 





