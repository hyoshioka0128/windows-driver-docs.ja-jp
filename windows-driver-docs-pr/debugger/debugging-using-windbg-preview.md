---
title: WinDbg プレビューを使用したデバッグ
description: このセクションでは、WinDbg プレビュー デバッガーを使用して基本的なデバッグ タスクを実行する方法について説明します。
ms.date: 04/03/2019
ms.localizationpriority: High
ms.openlocfilehash: 5ccb2cdbfe47bfbbdcdb54cb9c361da899e41aa5
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916235"
---
# <a name="debugging-using-windbg-preview"></a>WinDbg プレビューを使用したデバッグ 

![WinDbg プレビューの小さなロゴ](images/windbgx-preview-logo.png) 

WinDbg プレビューは、最新の外観、高速なウィンドウ、本格的なスクリプトの操作性を備え、拡張可能なデバッガー データモデルを中心に構築された WinDbg の新しいバージョンです。 WinDbg プレビューは、現行の WinDbg と同じ基本エンジンを使用しているため、使い慣れたすべてのコマンド、拡張機能、ワークフローがこれまでどおり動作します。

デバッガー開発チームからの最新のニュース、ヒント、コツについては、デバッガー ツール チームのブログを参照してください。
[https://blogs.msdn.microsoft.com/windbg/](https://blogs.msdn.microsoft.com/windbg/)

## <a name="major-features-of-windbg-preview"></a>WinDbg プレビューの主な機能

変更または新たに追加された主な点を次に説明します。

![デバッガーのメイン画面](images/windbgx-main-menu.png)

### <a name="general-features"></a>全般的な機能

- **より簡単になった接続設定と呼び出し** - WinDbg プレビューは、前のセッション構成情報を呼び出す機能を備えています。

![デバッガーのメイン画面のスクリーン ショット](images/windbgx-start-debugging-menu.png)

- **簡単なフィードバック チャネル** - お客様からのフィードバックは、開発を進める助けになります。 詳細については、「[フィードバックの提供](#providing-feedback)」を参照してください

- **ダンプ ファイル プロセッサ検出** - プロセッサ アーキテクチャを自動検出できるので、デバッグの管理が容易になります。

- **パフォーマンスの向上** ウィンドウが非同期で読み込まれるようになり、キャンセルできるようになりました - ユーザーが別のコマンドを実行すると、WinDbg プレビューはローカル、ウォッチ、またはその他のウィンドウの読み込みを停止します。

### <a name="windowing-improvements"></a>ウィンドウの機能強化

- **逆アセンブリ ウィンドウの機能強化** - 逆アセンブリ ウィンドウも改善されました。現在の命令の強調表示は、スクロールしても元の位置のままになります。 

    ![デバッガーの逆アセンブリ ウィンドウ](images/windbgx-disassembly.png)


- **メモリ ウィンドウの機能強化** - メモリ ウィンドウに強調表示機能が加わり、スクロールも改善されました。

- **ローカルおよびウォッチのデータ モデルの視覚化** - ローカル ウィンドウとウォッチ ウィンドウは、どちらも dx コマンドによって使用されるデータ モデルに基づいて表示されます。 このため、ローカル ウィンドウとウォッチ ウィンドウは、dx コマンドと同様に、ユーザーが読み込んだ任意の NatVis 拡張機能や JavaScript 拡張機能を利用でき、完全な LINQ クエリをサポートすることもできます。 

- **ログ** - これは、WinDbg プレビュー内部の内部ログです。 これは、トラブルシューティングや長時間実行されるプロセスを監視する目的で表示できます。 

詳細については、「[WinDbg プレビュー - [表示] メニュー](windbg-view-preview.md)」を参照してください。

- **コマンド ウィンドウ** - コマンド ウィンドウを使用すると、DML の切り替えや、デバッガー コマンド ウィンドウのクリアを簡単に実行できます。 現在のすべてのデバッガー コマンドは WinDbg プレビューと互換性があり、引き続き WinDbg Preview で動作します。


### <a name="dark-theme"></a>濃色テーマ 

濃色テーマを有効にするには、**ファイル** > **設定** を使用します。

![濃色テーマを示すスクリーン ショット](images/windbgx-dark-theme.png)

### <a name="ribbon-quick-access"></a>リボン クイック アクセス

最もよく使用するボタンをピン留めすることにより、リボンを折りたたんで画面領域を節約できます。 

![ピン留めされた項目を含むリボンを示すスクリーン ショット](images/windbgx-quick-access.png)

### <a name="source-window"></a>ソース ウィンドウ

最新のエディターに合うように、ソース ウィンドウが更新されました。 

![デバッガーのスクリプト作成メニューのスクリーン ショット](images/windbgx-source-window.png)

### <a name="highlighting"></a>強調表示

コマンド ウィンドウに、2 つの新しい強調表示機能が追加されました。 任意のテキストを選択すると、そのテキストの他のすべてのインスタンスがわずかに強調表示されます。 次に、[Highlight/Un-highlight (強調表示/強調表示解除)] または Ctrl + Alt + H を押すと、強調表示を保持できます。 

![列が黄色で強調表示されていることを示すスクリーン ショット](images/windbgx-highlighting.gif)

### <a name="better-keyboard-navigation"></a>改善されたキーボード ナビゲーション

Ctrl + Tab を押すだけで、キーボードだけでウィンドウ間を簡単に移動できます。 

![Ctrl Tab メニューを示すスクリーン ショット](images/windbgx-ctrl-tab.gif)

### <a name="integrated-time-travel-debugging-ttd"></a>統合された Time Travel Debugging (TTD)

アプリケーションを TTD トレースする必要がある場合は、起動時またはアタッチ時に、[Record process with Time Travel Debugging (Time Travel Debugging でプロセスを記録)] ボックスをオンにします。 WinDbgNext がこれを TTD に設定し、記録が完了するとトレースを開きます。

![Ctrl Tab メニューを示すスクリーン ショット](images/windbgx-ttd.png)

詳細については、「[Time Travel Debugging - 概要](time-travel-debugging-overview.md)」を参照してください。

### <a name="debugging-app-packages"></a>アプリ パッケージのデバッグ

ユニバーサルアプリやバックグラウンド タスクのデバッグを、シングル クリックで実行できるようになりました。

![検索ボックスに「cal」と入力され 3 つのアプリが一覧表示されている [Launch App Package (アプリ パッケージの起動)] の [アプリケーション] タブ](images/windbgx-launch-app-package.png)

詳細については、「[アプリ パッケージの起動](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-user-mode-preview#launch-app-package)」を参照してください。

### <a name="attach-to-a-process"></a>プロセスへのアタッチ

アタッチ ダイアログが、従来より高速でより詳細になり、使いやすくなりました。

![プロセスへのアタッチのダイアログ](images/windbgx-attach-to-a-process-zoomed.png)

### <a name="enhanced-breakpoint-tracking"></a>強化されたブレークポイント追跡  

- **ブレークポイントの有効化/無効化** - ブレークポイント ウィンドウに現在のすべてのブレークポイントが表示され、それらを簡単に有効化または無効化できます。 
- **ヒット カウント** - ブレークポイント ウィンドウには、ブレークポイントにヒットするたびにそれまでの合計が表示されます。

詳細については、「[ブレークポイント](windbg-breakpoints-preview.md)」を参照してください。


### <a name="enhanced-data-model-support"></a>強化されたデータ モデルのサポート

- **組み込みデータ モデルのサポート** - WinDbg プレビューは、組み込みのデータ モデルがサポートされて作成されており、そのデータ モデルをデバッガーを通じて利用できます。
- **モデル ウィンドウ** - モデル ウィンドウを使用すると、dx や dx -g を展開表示することができ、NatVis、JavaScript、LINQ のクエリを基に強力なテーブルを作成できます。 

詳細については、「[WinDbg プレビュー - データ モデル](windbg-data-model-preview.md)」を参照してください。

![デバッガーのデータ モデル メニューのスクリーン ショット](images/windbgx-data-model-menu.png)

### <a name="new-scripting-development-ui"></a>新しいスクリプト開発 UI

- **スクリプト開発 UI** - エラーの強調表示と IntelliSense により JavaScript スクリプトや NatVis スクリプトの開発を簡単にする、専用のスクリプト作成ウィンドウが用意されました。

![デバッガーのスクリプト作成メニューのスクリーン ショット](images/windbgx-scripting-intellisense.png)

詳細については、「[WinDbg プレビュー - スクリプト](windbg-scripting-preview.md)」を参照してください。

### <a name="backwards-compatibility"></a>下位互換性 

基になるデバッガー エンジンは同じなので、従来のデバッガー コマンドやデバッガー拡張機能はすべて引き続き動作します。

## <a name="span-idproviding-feedbackspanproviding-feedback"></a><span id="providing-feedback"></span>フィードバックの提供

お客様からのフィードバックは、WinDbg の開発を進める助けになります。 

- 実現を希望される機能や問題の原因となっているバグなどのフィードバックがある場合は、フィードバック Hub をご利用ください。

![[新しいフィードバックの追加] ボタンを含むフィードバック オプションを示すフィードバック Hub のスクリーンショット](images/windbgx-feedback.png)

## <a name="videos"></a>ビデオ

[デフラグ ツール](https://channel9.msdn.com/Shows/Defrag-Tools) ショーの次のエピソードから、Windbg プレビューの実際の動作をご覧いただけます。  
- [デフラグ ツール #182](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-182-WinDbg-Preview-Part-1) - Tim、Chad、Andy による、WinDbg プレビューの基本と一部の機能の紹介。
- [デフラグ ツール #183](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-183-WinDbg-Preview-Part-2) - Nick、Tim、Chad による、WinDbg プレビューを使用した簡単なデモ。
- [デフラグ ツール #184](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-184-JavaScript-in-WinDbg-Preview) - Bill と Andrew による、WinDbg プレビューのスクリプト機能の紹介。
- [デフラグ ツール #185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) - James と Ivette による、Time Travel Debugging の紹介。
- [デフラグ ツール #186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) - James と JCAB による、Time Travel Debugging の高度な使用方法の説明。

## <a name="next-steps"></a>次のステップ

最新リリースの新機能については、「[WinDbg プレビュー - 新機能](windbg-what-is-new-preview.md)」を参照してください。

WinDbg プレビューをインストールして構成するには、次のトピックをご確認ください。

- [WinDbg プレビュー - インストール](windbg-install-preview.md)
- [WinDbg プレビュー - コマンド ライン スタートアップ オプション](windbg-command-line-preview.md)
- [WinDbg プレビュー - 設定とワークスペース](windbg-setup-preview.md)
- [WinDbg プレビュー - キーボード ショートカット](windbg-keyboard-shortcuts-preview.md)

デバッグする環境に接続する方法については、以下のトピックで説明されています。 

- [WinDbg プレビュー - ユーザーモード セッションの開始](windbg-user-mode-preview.md)
- [WinDbg プレビュー - カーネルモード セッションの開始](windbg-kernel-mode-preview.md)

いくつかの一般的なタスクについては、メニュー タブ別に以下のトピックで説明されています。

- [WinDbg プレビュー - ファイル メニュー](windbg-file-preview.md)
- [WinDbg プレビュー – ホーム メニュー](windbg-home-preview.md)
- [WinDbg プレビュー – 表示メニュー](windbg-view-preview.md)
- [WinDbg プレビュー – ブレークポイント](windbg-breakpoints-preview.md)
- [WinDbg プレビュー - データ モデル](windbg-data-model-preview.md)
- [WinDbg プレビュー - スクリプト](windbg-scripting-preview.md)

---