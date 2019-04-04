---
title: スクリプト ファイルの使用
description: スクリプト ファイルの使用
ms.assetid: b78a651e-57c8-4863-a8cf-dedd8e308e66
keywords:
- スクリプト ファイル
- スクリプト ファイル、概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fad33093eeee4c895bcf2ffdd62dd243c4cdcb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582636"
---
# <a name="using-script-files"></a>スクリプト ファイルの使用


## <span id="ddk_using_script_files_dbg"></span><span id="DDK_USING_SCRIPT_FILES_DBG"></span>


A*スクリプト ファイル*デバッガー コマンドのシーケンスを含むテキスト ファイルです。 さまざまなデバッガーをスクリプト ファイルを読み込んで実行する方法があります。 スクリプト ファイルは、順番に実行されるコマンドを含めることができます。 または実行のより複雑なフローを使用することができます。

スクリプト ファイルを実行するには、次のいずれかの操作を行います。

-   (KD、CDB のみで、デバッガーが開始時のみ)Ntsd.ini というスクリプト ファイルを作成しからデバッガーを開始するディレクトリに配置します。 デバッガーでは、デバッガーの起動時にこのファイルが自動的に実行します。 スタートアップ スクリプト ファイルを別のファイルを使用するを使用してパスとファイル名を指定、 **cf** [コマンド ライン オプション](command-line-options.md)またはを使用して、 **IniFile** 内のエントリ[Tools.ini](configuring-tools-ini.md)ファイル。

-   (KD、CDB ときのみには各セッションの開始)スクリプト ファイルを作成しを使用して、パスとファイル名を指定、 **- cfr** [コマンド ライン オプション](command-line-options.md)します。 デバッガー自動的にこのスクリプト ファイル デバッガーの起動時と実行するたびに、ターゲットが再起動します。

-   使用して、 **$ &lt;**、 **$ &gt; &lt;**、 **$$ &lt;**、および**$$ &gt; &lt;** スクリプトを実行するコマンド ファイルのデバッガーが実行されています。 構文の詳細については、次を参照してください[  **$ &lt;、$&gt;&lt;、$&gt;&lt;、$$&gt; &lt; (実行スクリプトのファイル)**](-----------------------a---run-script-file-.md)。

**$ &gt; &lt;** と**$$ &gt; &lt;** コマンドは、重要なのいずれかでスクリプトを実行している他の方法によって異なります。方法です。 これらのコマンドを使用すると、デバッガーは、指定したスクリプト ファイルを開きをセミコロンで区切って、すべての改行を置き換えます、1 つのコマンド ブロックとして生成されるテキストを実行します。 これらのコマンドは、デバッガー コマンド プログラムが含まれているスクリプトを実行している場合に便利です。 これらのプログラムの詳細については、[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)を参照してください。X

WinDbg でのみ使用可能なコマンドを使用することはできません (など[ **.lsrcfix (ローカル ソース サーバーを使用して)**](-srcfix---lsrcfix--use-source-server-.md)、 [ **.lsrcpath (ローカル ソース パスを設定する)** ](-srcpath---lsrcpath--set-source-path-.md)、 [ **.open (ソース ファイルを開きます)**](-open--open-source-file-.md)、および[ **.write\_cmd\_hist (コマンドの履歴を書き込む)**](-write-cmd-hist--write-command-history-.md)) WinDbg でスクリプト ファイルが実行される場合でも、スクリプト ファイルにします。 さらに、使用することはできません、 [ **(スピーカー ビープ音) .beep**](-beep--speaker-beep-.md)、 [ **.cls (画面のクリア)**](-cls--clear-screen-.md)、 [ ***.hh* (HTML ヘルプ ファイルを開く)**](-hh--open-html-help-file-.md)、 [ **.idle\_cmd (アイドル状態のコマンドの設定)**](-idle-cmd--set-idle-command-.md)、 [ **.remote (作成 Remote.exeサーバー)**](-remote--create-remote-exe-server-.md)、カーネル モード[ **.restart (再起動カーネル接続)**](-restart--restart-kernel-connection-.md)、ユーザー モード[ **.restart (再起動ターゲットアプリケーションの)**](-restart--restart-target-application-.md)、または[ **.wtitle (ウィンドウ タイトルの設定)** ](-wtitle--set-window-title-.md)スクリプト ファイル内のコマンド。

WinDbg では、軽微な例外が 1 つとして、KD、CDB、同じスクリプトをサポートします。 使用することができます、 [ **.remote\_exit (終了デバッグ クライアント)** ](-remote-exit--exit-debugging-client-.md) KD、CDB またはを使用するスクリプト ファイルでのみコマンド。 終了できませんデバッグ クライアントから、WinDbg で実行されるスクリプト。

 

 





