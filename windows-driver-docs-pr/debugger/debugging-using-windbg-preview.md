---
title: WinDbg プレビューを使用したデバッグ
description: ここでは、WinDbg preview デバッガーを使用して基本的なデバッグタスクを実行する方法について説明します。
ms.date: 04/03/2019
ms.localizationpriority: High
ms.openlocfilehash: 7d81b172213ebccffd0b126e9ed0432bcbfc9424
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007579"
---
![Windbg プレビューの小さいロゴ](images/windbgx-preview-logo.png) 

# <a name="debugging-using-windbg-preview"></a>WinDbg プレビューを使用したデバッグ 

WinDbg Preview は、最新のビジュアルと、拡張可能なデバッガーデータモデルの front と center を使用して構築された本格的なスクリプト作成エクスペリエンスを備えた、新しいバージョンの WinDbg です。 WinDbg Preview は、現在の WinDbg と同じ基になるエンジンを使用しています。したがって、使用しているすべてのコマンド、拡張機能、ワークフローは、以前と同じように動作します。

デバッガー開発チームの最新のニュース、ヒント、コツについては、デバッガーツールチームのブログを参照してください。
[https://blogs.msdn.microsoft.com/windbg/](https://blogs.msdn.microsoft.com/windbg/)


## <a name="major-features-of-windbg-preview"></a>WinDbg プレビューの主な機能

ここでは、変更された、または新機能を紹介します。

![デバッガーのメイン画面](images/windbgx-main-menu.png)


### <a name="general-features"></a>一般的な機能

- **接続の設定と再呼び出しが簡単**-WinDbg プレビューには、前のセッション構成情報を再呼び出しする機能が含まれています。

![デバッガーのメイン画面のスクリーンショット](images/windbgx-start-debugging-menu.png)

- **簡単なフィードバックチャネル**-今後の開発作業についてのご意見をお寄せください。 詳細については、「[フィードバックの提供](#providing-feedback)」を参照してください。

- **ダンプファイルプロセッサの検出**-マネージデバッグを容易にするためのプロセッサアーキテクチャを自動検出します。

- **パフォーマンスの向上**Windows が非同期的に読み込まれ、取り消すことができるようになりました。別のコマンドを実行すると、WinDbg Preview によって、ローカル、ウォッチ、またはその他のウィンドウの読み込みが停止します。

### <a name="windowing-improvements"></a>ウィンドウの機能強化

- **逆アセンブリウィンドウの機能強化**-[逆アセンブル] ウィンドウも改善され、現在の命令の強調表示はスクロール時の状態のままになります。 

    ![デバッガーでのウィンドウの逆アセンブリ](images/windbgx-disassembly.png)


- [**メモリウィンドウの改善]** -[メモリ] ウィンドウのスクロールが強調表示され、改善されました。

- **ローカルおよびウォッチデータモデルの視覚化**-[ローカル] ウィンドウと [ウォッチ] ウィンドウは、どちらも dx コマンドによって使用されるデータモデルに基づいています。 つまり、[ローカル] ウィンドウと [ウォッチ] ウィンドウでは、読み込まれた NatVis または JavaScript の拡張機能を利用できます。また、dx コマンドと同様に、完全な LINQ クエリをサポートすることもできます。 

- **ログ**-これは、WinDbg プレビューの内部のログの下にあります。 トラブルシューティングのために、または実行時間の長いプロセスを監視するために表示できます。 

詳細については、「 [WinDbg プレビュー-表示メニュー](windbg-view-preview.md)」を参照してください。

- **コマンドウィンドウ**-[コマンド] ウィンドウを使用すると、DML の切り替えとデバッガーコマンドウィンドウのクリアに簡単にアクセスできます。 現在のすべてのデバッガーコマンドはと互換性があり、引き続き WinDbg Preview で動作します。


### <a name="dark-theme"></a>ダーク テーマ 

**ファイル** >  の**設定**を使用して、ダークテーマを有効にします。

![ダークテーマを示すスクリーンショット](images/windbgx-dark-theme.png)


### <a name="ribbon-quick-access"></a>リボンクイックアクセス

最もよく使用するボタンをピン留めするだけで、リボンを折りたたんで画面の不動産を保存することができます。 
 
![ピン留めされた項目を含む ribon を示すスクリーンショット](images/windbgx-quick-access.png)



### <a name="source-window"></a>ソースウィンドウ

ソースウィンドウは、最新のエディターを使用して、より多くの行に更新されています。 

![デバッガーの [スクリプト] メニューのスクリーンショット](images/windbgx-source-window.png)


### <a name="highlighting"></a>ペン

[コマンド] ウィンドウには、2つの新しい強調表示機能があります。 テキストを選択すると、そのテキストの他のインスタンスに対して微妙な強調表示が行われます。 強調表示を維持するには、[強調表示/強調表示解除] または Ctrl + Alt + H を押します。 

![黄色で強調表示されている列を示すスクリーンショット](images/windbgx-highlighting.gif)


### <a name="better-keyboard-navigation"></a>キーボードナビゲーションの向上

Ctrl + Tab キーを押すだけで、キーボードだけでウィンドウ間を簡単に移動できます。 

![Ctrl tab メニューが表示されているスクリーンショット](images/windbgx-ctrl-tab.gif)


### <a name="integrated-time-travel-debugging-ttd"></a>統合タイムトラベルデバッグ (TTD)

アプリケーションの TTD トレースが必要な場合は、起動時またはアタッチ時に [タイムトラベルによるプロセスの記録] ボックスをオンにするだけです。 WinDbgNext は、TTD に設定し、記録が完了したらトレースを開きます。

![Ctrl tab メニューが表示されているスクリーンショット](images/windbgx-ttd.png)

詳細については、「[タイムトラベルデバッグ-概要](time-travel-debugging-overview.md)」を参照してください。


### <a name="debugging-app-packages"></a>アプリケーションパッケージのデバッグ

ユニバーサルアプリまたはバックグラウンドタスクのデバッグが1回のクリックになりました。

![[アプリパッケージアプリケーション] タブを起動し、3つのアプリが一覧表示された [検索] ボックスに cal を表示します。](images/windbgx-launch-app-package.png)

詳細については、「[アプリパッケージの起動](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-user-mode-preview#launch-app-package)」を参照してください。


### <a name="attach-to-a-process"></a>プロセスにアタッチする

[アタッチ] ダイアログの方が高速で、より詳細で、使いやすくなります。

![プロセスにアタッチダイアログ](images/windbgx-attach-to-a-process-zoomed.png)


### <a name="enhanced-breakpoint-tracking"></a>拡張されたブレークポイントの追跡  

- **ブレークポイントの有効化/無効化**-[ブレークポイント] ウィンドウには、現在のすべてのブレークポイントが表示され、それらを有効または無効にするための簡単なアクセスを提供します。 
- **ヒットカウント**-ブレークポイントにヒットするたびに、ブレークポイント ウィンドウには実行中の合計が保持されます。

詳細については、「[ブレークポイント](windbg-breakpoints-preview.md)」を参照してください。


### <a name="enhanced-data-model-support"></a>強化されたデータモデルのサポート

- **組み込みのデータモデルサポート**-WinDbg Preview は、組み込みのデータモデルサポートを使用して記述されており、データモデルはデバッガーを通じて利用できます。
- **モデルウィンドウ**-[モデル] ウィンドウには、"dx" と "dx" という拡張可能でブラウズ可能なバージョンが用意されており、NatVis、JAVASCRIPT、LINQ クエリの上に強力なテーブルを作成できます。 

詳細については、「 [WinDbg Preview-Data model](windbg-data-model-preview.md)」を参照してください。

![デバッガーの [データモデル] メニューのスクリーンショット](images/windbgx-data-model-menu.png)


### <a name="new-scripting-development-ui"></a>新しいスクリプト開発 UI 

- **スクリプト開発 UI** -NatVis スクリプトを作成するためのスクリプトウィンドウが作成されました。これにより、エラーの強調表示と IntelliSense を使用して JavaScript およびスクリプトを簡単に開発できます。

![デバッガーの [スクリプト] メニューのスクリーンショット](images/windbgx-scripting-intellisense.png)

詳細については、「 [WinDbg Preview-Scripting](windbg-scripting-preview.md)」を参照してください。

### <a name="backwards-compatibility"></a>旧バージョンとの互換性 

このデバッガーエンジンは同じであるため、以前のすべてのデバッガーコマンドとデバッガー拡張機能は引き続き動作します。

## <a name="span-idproviding-feedbackspanproviding-feedback"></a><span id="providing-feedback"></span>フィードバックの提供

お客様のご意見をお寄せいただくと、今後の WinDbg 開発に役立ちます。 

- 実際に表示する機能や、何らかの問題が発生するバグなどのフィードバックがある場合は、フィードバックハブを使用してください。

![[新しいフィードバックの追加] ボタンを含むフィードバックオプションを示すフィードバックハブのスクリーンショット](images/windbgx-feedback.png)

## <a name="videos"></a>ビデオ

この2回の[最適化ツール](https://channel9.msdn.com/Shows/Defrag-Tools)が表示されているので、Windbg のプレビューが動作しています。  
- [デフラグツール #182](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-182-WinDbg-Preview-Part-1) -Tim、チャド、Andy では、WinDbg Preview の基本と一部の機能について紹介します。
- [デフラグツール #183](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-183-WinDbg-Preview-Part-2) -チャド、Tim、およびでは、WinDbg Preview を使用して、簡単なデモを見ていきます。
- [デフラグツール #184](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-184-JavaScript-in-WinDbg-Preview) -Bill and Andrew では、WinDbg Preview のスクリプト機能について説明しています。
- [デフラグツール #185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) -James と Ivette は、タイムトラベルデバッグを提供し、概要を説明します。
- [デフラグツール #186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) -JAMES および jcab では、高度なタイムトラベルデバッグについて説明しています。

## <a name="next-steps"></a>次の手順

最新のリリースの新機能については、「 [WinDbg Preview-新機能](windbg-what-is-new-preview.md)」を参照してください。

これらのトピックを確認して、WinDbg Preview のインストールと構成を行います。

- [WinDbg プレビュー–インストール](windbg-install-preview.md)
- [WinDbg プレビュー–コマンドラインスタートアップオプション](windbg-command-line-preview.md)
- [WinDbg プレビュー–設定とワークスペース](windbg-setup-preview.md)
- [WinDbg プレビュー–キーボードショートカット](windbg-keyboard-shortcuts-preview.md)

これらのトピックでは、デバッグする環境に接続する方法について説明します。 

- [WinDbg Preview –ユーザーモードセッションを開始する](windbg-user-mode-preview.md)
- [WinDbg Preview –カーネルモードセッションを開始する](windbg-kernel-mode-preview.md)

これらのトピックでは、いくつかの一般的なタスクについて、メニュータブ別に説明します。

- [WinDbg プレビュー-[ファイル] メニュー](windbg-file-preview.md)
- [WinDbg プレビュー–ホームメニュー](windbg-home-preview.md)
- [WinDbg プレビュー-[表示] メニュー](windbg-view-preview.md)
- [WinDbg プレビュー–ブレークポイント](windbg-breakpoints-preview.md)
- [WinDbg プレビュー–データモデル](windbg-data-model-preview.md)
- [WinDbg プレビュー–スクリプト](windbg-scripting-preview.md)


--- 





