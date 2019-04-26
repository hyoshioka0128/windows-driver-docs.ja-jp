---
title: WinDbg プレビューを使用したデバッグ
description: このセクションでは、WinDbg プレビュー デバッガーを使用して、基本的なデバッグ タスクを実行する方法について説明します。
ms.date: 04/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7d3b32cfca7fee3ed39154012fc25e29f2782d8c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346408"
---
![Windbg のプレビューの小さいロゴ](images/windbgx-preview-logo.png) 

# <a name="debugging-using-windbg-preview"></a>WinDbg プレビューを使用したデバッグ 

WinDbg のプレビューは、最新のビジュアル、windows の高速化、拡張可能なデバッガー データ モデルの前面と center で構築された、本格的なスクリプト作成エクスペリエンスと WinDbg の新しいバージョンです。 WinDbg のプレビューはエンジンを使用して、同じ基になる WinDbg として今日、ため、すべてのコマンド、拡張機能、およびワークフローに慣れている方は引き続き機能する前します。

最新ニュース、ヒント、およびデバッガーの開発チームでのテクニック、デバッガー ツール チームのブログを参照してください。
[https://blogs.msdn.microsoft.com/windbg/](https://blogs.msdn.microsoft.com/windbg/)


## <a name="major-features-of-windbg-preview"></a>WinDbg の主要な機能をプレビューします。

変更されたかを初めて使用する最も注目に値するものを次に示します。

![デバッガーでのメイン画面](images/windbgx-main-menu.png)


### <a name="general-features"></a>全般的な機能

- **接続のセットアップと再現率を簡単に**-WinDbg のプレビューには機能に前のセッション構成の情報が含まれています。

![デバッガーでのメイン画面のスクリーン ショット](images/windbgx-start-debugging-menu.png)

- **簡単なフィードバック チャネル**-お客様のフィードバックは今後の開発作業を説明します。 詳細については、次を参照してください[フィードバックの提供。](#providing-feedback)

- **ダンプ ファイルのプロセッサの検出**-自動-容易にマネージ デバッグのために、プロセッサ アーキテクチャを検出します。

- **パフォーマンスの向上**WinDbg プレビュー、別のコマンドを実行する場合は、ローカル、ウォッチ、またはその他の windows の読み込みを停止 - Windows は、ここで非同期的にロードし、取り消すことができます。

### <a name="windowing-improvements"></a>ウィンドウの機能強化

- **逆アセンブル ウィンドウの機能強化**-逆アセンブル ウィンドウが向上してがスクロールすると、現在の命令の強調表示のままです。 

    ![デバッガーでの逆アセンブリ ウィンドウ](images/windbgx-disassembly.png)


- **メモリ ウィンドウに対する改良**-メモリ ウィンドウが強調表示し、強化されたスクロールします。

- **ローカルとウォッチ データ モデルの視覚エフェクト**-ローカル ウィンドウと ウォッチ ウィンドウは両方に基づいて、dx コマンドによって使用されるデータ モデル。 つまり、ローカルとウォッチ ウィンドウ役立つ NatVis、または JavaScript から拡張機能が読み込まれて、dx コマンドと同様のサポートも完全な LINQ クエリのことができます。 

- **ログ**-これは、WinDbg プレビューの内部構造の内部ではログの下。 トラブルシューティングや長時間実行されるモニターに表示できます。 

詳細については、次を参照してください。 [WinDbg プレビューの表示 メニュー](windbg-view-preview.md)します。

- **コマンド ウィンドウ**-コマンド ウィンドウを使用して DML を切り替えるし、デバッガーのコマンド ウィンドウをクリアに簡単にアクセスを提供します。 現在のすべてのデバッガー コマンドを使用して、互換性があり、WinDbg プレビューで作業を続行します。


### <a name="dark-theme"></a>ダーク テーマ 

使用**ファイル** > **設定**ダーク テーマを有効にします。

![ダーク テーマを示すスクリーン ショット](images/windbgx-dark-theme.png)


### <a name="ribbon-quick-access"></a>リボンのクイック アクセス

だけ、よく使用するボタンをピン留めして、実際の画面を保存するには、リボンを折りたたむことができます。 
 
![ピン留めされたアイテムでの ribon を示すスクリーン ショット](images/windbgx-quick-access.png)



### <a name="source-window"></a>ソース ウィンドウ

ソース ウィンドウは非常に最新のエディターに合わせて更新されました。 

![スクリプト デバッガー メニューのスクリーン ショット](images/windbgx-source-window.png)


### <a name="highlighting"></a>強調表示

コマンド ウィンドウには 2 つの新しい強調表示機能。 任意のテキストを選択すると、そのテキストの他のインスタンスに微妙な強調表示が提供されます。 「強調表示や解除-強調」または強調表示を保持するには Ctrl + Alt + H しに達すことができます。 

![スクリーン ショットが表示された列が黄色で強調表示](images/windbgx-highlighting.gif)


### <a name="better-keyboard-navigation"></a>キーボード ナビゲーションを向上させる

Ctrl キーを押しながら Tab キーを押すだけとキーボードだけで windows 間を簡単に移動できます。 

![Screen shot showing ctrl tab menu](images/windbgx-ctrl-tab.gif)


### <a name="integrated-time-travel-debugging-ttd"></a>デバッグ (TTD) 統合のタイム トラベル

TTD トレース、アプリケーションの場合は、起動または接続を行うときに、「タイム トラベル デバッグ レコード プロセス」ボックスを確認します。 WinDbgNext TTD、セットアップを完了すると、トレースを開いて記録します。

![Screen shot showing ctrl tab menu](images/windbgx-ttd.png)

詳細については、次を参照してください。[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)します。


### <a name="debugging-app-packages"></a>アプリ パッケージのデバッグ

ユニバーサル アプリまたはバック グラウンド タスクのデバッグは、1 回のクリックではようになりました。

![検索ボックスに表示されている 3 つのアプリで cal を示すアプリ パッケージのアプリケーション タブを起動します。](images/windbgx-launch-app-package.png)

詳細については、次を参照してください。[アプリ パッケージの起動](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-user-mode-preview#launch-app-package)します。


### <a name="attach-to-a-process"></a>プロセスにアタッチします。

アタッチ ダイアログが高速より詳細なとを使用する方が簡単です。

![プロセス ダイアログにアタッチします。](images/windbgx-attach-to-a-process-zoomed.png)


### <a name="enhanced-breakpoint-tracking"></a>強化されたブレークポイントの追跡  

- **ブレークポイントを有効または無効に**-[ブレークポイント] ウィンドウは、現在のすべてのブレークポイントを表示し、簡単にアクセスを提供可能にして無効にすることにします。 
- **ヒット カウント**-、[ブレークポイント] ウィンドウは、実行中のブレークポイントがヒットするたびに現在の合計。

詳細については、次を参照してください。[ブレークポイント](windbg-breakpoints-preview.md)します。


### <a name="enhanced-data-model-support"></a>強化されたデータ モデルのサポート

- **データ モデルのサポートで構築された**- 組み込まれているデータ モデルのサポートと WinDbg のプレビューが書き込まれ、データ モデルは、デバッガーを使用します。
- **[モデル] ウィンドウ**- [モデル] ウィンドウでは、'dx' の拡張可能な参照可能なバージョンと 'dx-g' できるようにする強力なを作成するためのテーブル、NatVis、JavaScript、および LINQ クエリの上位にします。 

詳細については、次を参照してください。 [WinDbg Preview - データ モデル](windbg-data-model-preview.md)します。

![デバッガーでのデータ モデル メニューのスクリーン ショット](images/windbgx-data-model-menu.png)


### <a name="new-scripting-development-ui"></a>スクリプト開発の新しい UI 

- **スクリプト開発 UI** -、エラーの強調表示と IntelliSense で、簡単に JavaScript と NatVis スクリプトの開発に特化したスクリプト ウィンドウが追加されました。

![スクリプト デバッガー メニューのスクリーン ショット](images/windbgx-scripting-intellisense.png)

詳細については、次を参照してください。 [WinDbg Preview - Scripting](windbg-scripting-preview.md)します。

### <a name="backwards-compatibility"></a>下位互換性 

元になるデバッガー エンジンが同じであるため、以前のデバッガー コマンドとデバッガー拡張機能のすべて引き続き機能します。

## <a name="span-idproviding-feedbackspanproviding-feedback"></a><span id="providing-feedback"></span>フィードバックの送信

お客様のフィードバックに役立つガイド WinDbg の開発今後します。 

- 実際に表示する機能や処理の難しいバグなどのフィードバックがあれば、フィードバック Hub を使用します。

![新しいフィードバックの追加 ボタンを含むフィードバックのオプションを示すフィードバック ハブのスクリーン ショット](images/windbgx-feedback.png)

## <a name="videos"></a>ビデオ

これらのエピソードを見る、[デフラグ ツール](https://channel9.msdn.com/Shows/Defrag-Tools)番組にアクションの Windbg のプレビューを参照してください。  
- [デフラグ ツール #182](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-182-WinDbg-Preview-Part-1) -Tim, チャド、および Andy WinDbg プレビューの基本と、機能の一部を経由します。
- [デフラグ ツール #183](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-183-WinDbg-Preview-Part-2) -Nick、Tim、Chad WinDbg のプレビューを使用して、短いデモを経由します。
- [デフラグ ツール #184](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-184-JavaScript-in-WinDbg-Preview) -請求書と Andrew は WinDbg のプレビューでのスクリプト機能を説明します。
- [デフラグ ツール #185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) -James と Ivette を提供し、タイム トラベルのデバッグの概要。
- [デフラグ ツール #186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) -James と JCAB で高度なタイム トラベルのデバッグについて説明します。

## <a name="next-steps"></a>次の手順

新機能については、この最新リリースについては、次を参照してください。 [WinDbg Preview - 新](windbg-what-is-new-preview.md)します。

これらのトピックをインストールし、WinDbg プレビューの構成を確認します。

- [WinDbg Preview – インストール](windbg-install-preview.md)
- [WinDbg のプレビュー-コマンド ライン スタートアップ オプション](windbg-command-line-preview.md)
- [WinDbg プレビュー – とワークスペースの設定](windbg-setup-preview.md)
- [WinDbg プレビュー – キーボード ショートカット](windbg-keyboard-shortcuts-preview.md)

これらのトピックでは、デバッグする環境に接続する方法について説明します。 

- [WinDbg プレビュー-ユーザー モードのセッションを開始](windbg-user-mode-preview.md)
- [WinDbg プレビュー-カーネル モードのセッションを開始](windbg-kernel-mode-preview.md)

これらのトピックでは、メニュー、タブによって編成された、一般的なタスクについて説明します。

- [WinDbg のプレビュー] – [ファイル] メニュー](windbg-file-preview.md)
- [WinDbg プレビュー – ホーム メニュー](windbg-home-preview.md)
- [WinDbg のプレビュー] – [表示] メニュー](windbg-view-preview.md)
- [WinDbg プレビュー – ブレークポイント](windbg-breakpoints-preview.md)
- [WinDbg プレビュー – データ モデル](windbg-data-model-preview.md)
- [WinDbg Preview – Scripting](windbg-scripting-preview.md)


--- 





