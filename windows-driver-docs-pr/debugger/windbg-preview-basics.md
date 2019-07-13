---
title: WinDbg のプレビューの基礎
description: このセクションでは、WinDbg プレビュー デバッガーの基本機能について説明します。
ms.date: 05/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 98986a36c9094322e60a9f0436182ecbce654217
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866495"
---
![Windbg のプレビューの小さいロゴ](images/windbgx-preview-logo.png) 

| [タイトル]               | 説明        |
| ------------------- | -------------------|
|[WinDbg のプレビューの新機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-using-windbg-preview)|WinDbg のプレビューでは新機能 |


## <a name="the-debugger-data-model"></a>デバッガーのデータ モデル

| [タイトル]               | 説明        |
| ------------------- | -------------------|
| [Dx コマンド](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-) | デバッガー オブジェクト モデルの式を表示する対話型コマンド |
| [デバッガー オブジェクトを LINQ で使用します。](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-linq-with-the-debugger-objects) | SQL クエリ言語と同様に |
| [NatVis でネイティブ デバッガー オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/debugger/native-debugger-objects-in-natvis)| NatVis で、オブジェクトの使用 |
| [WinDbg Preview - データ モデル](windbg-data-model-preview.md) | WinDbg のプレビューでのデータ モデルのサポートで、ビルドを使用する方法 |

## <a name="extending-the-data-model"></a>データ モデルの拡張

| [タイトル]               | 説明        |
| ------------------- | -------------------|
| [JavaScript デバッガー スクリプト](https://docs.microsoft.com/windows-hardware/drivers/debugger/javascript-debugger-scripting) | JavaScript を使用して、デバッガーのオブジェクトについて理解するスクリプトを作成する方法  |
| [WinDbg Preview - Scripting](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-scripting-preview) |スクリプトで構築された WinDbg プレビューを使用します。  |
| https://github.com/Microsoft/WinDbg-Samples |最新の JavaScript を共有する、デバッガー チームの GitHub サイト (とC++) サンプル コード。 |
|[JavaScript の拡張機能のネイティブ デバッガー オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/debugger/native-objects-in-javascript-extensions) | 一般的なオブジェクトを使用する方法について説明し、その属性とビヘイビアーを参照情報を提供します。|


## <a name="ttd-basics"></a>TTD の基礎

| [タイトル]               | 説明        |
| ------------------- | -------------------|
| [旅行時間 - デバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-overview) | TTD の概要 |
[旅行のデバッグ時間 - サンプル アプリのチュートリアル](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-walkthrough) |  付与するタイム トラベルお試しくださいチェック アウトこのチュートリアル |

## <a name="ttd-queries"></a>TTD クエリ
| [タイトル]               | 説明        |
| ------------------- | -------------------|
| [オブジェクトのタイム トラベルのデバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-object-model)します。 |クエリ時にデータ モデルを使用するトレースを移動します。  
|  https://github.com/Microsoft/WinDbg-Samples/blob/master/TTDQueries/tutorial-instructions.md |デバッグする方法に関するチュートリアルC++TTD クエリを使用して、問題のあるコードを検索するコード |
| https://github.com/Microsoft/WinDbg-Samples/tree/master/TTDQueries/app-sample | ここで使用可能なすべてのラボで使用するコードとします。

## <a name="videos"></a>ビデオ

これらのエピソードを見る[デフラグ ツール](https://channel9.msdn.com/Shows/Defrag-Tools)Windbg プレビュー動作を確認します。  

| [タイトル]               | 説明        |
|-------------------- |--------------------|
| [ツールと 182 を最適化します。](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-182-WinDbg-Preview-Part-1) |Tim, チャド、および Andy WinDbg プレビューの基本と機能の一部を参照してください。 |
| [デフラグ ツール #183](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-183-WinDbg-Preview-Part-2) | Nick、Tim、Chad WinDbg のプレビューを使用して、短いデモを経由 |
| [ツールと 184 を最適化します。](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-184-JavaScript-in-WinDbg-Preview) | 請求書と Andrew WinDbg プレビューでのスクリプト機能をについて説明します。 |
| [デフラグ ツール #185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) | James と Ivette を提供し、タイム トラベルのデバッグの概要 |
| [デフラグ ツール #186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) | James と JCAB の内部では高度なタイム トラベルのデバッグ |

## <a name="installation-and-getting-connected"></a>インストールと接続 

| [タイトル]               | 説明        |
| ------------------- | -------------------|
| [WinDbg Preview – インストール](windbg-install-preview.md) | インストールの指示 |
| [WinDbg プレビュー-ユーザー モードのセッションを開始](windbg-user-mode-preview.md) | ユーザー モード  |
| [WinDbg プレビュー-カーネル モードのセッションを開始](windbg-kernel-mode-preview.md) | カーネル モード |
