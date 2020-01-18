---
title: WinDbg プレビューの基礎
description: ここでは、WinDbg preview デバッガーの基本的な機能について説明します。
ms.date: 05/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6467c8157e361aebdb5a8204ddd9dcabb5283b8e
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256684"
---
# <a name="windbg-preview-basics"></a>WinDbg プレビューの基礎

![WinDbg プレビューの小さなロゴ](images/windbgx-preview-logo.png) 

| Title (タイトル)               | 説明        |
| ------------------- | -------------------|
|[WinDbg Preview-新機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-using-windbg-preview)|WinDbg Preview の新機能 |

## <a name="the-debugger-data-model"></a>デバッガーデータモデル

| Title (タイトル)               | 説明        |
| ------------------- | -------------------|
| [dx コマンド](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-) | デバッガーオブジェクトモデル式を表示する対話型コマンド |
| [デバッガーオブジェクトでの LINQ の使用](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-linq-with-the-debugger-objects) | SQL のようなクエリ言語 |
| [NatVis のネイティブデバッガーオブジェクト](https://docs.microsoft.com/windows-hardware/drivers/debugger/native-debugger-objects-in-natvis)| NatVis でのオブジェクトの使用 |
| [WinDbg プレビュー-データモデル](windbg-data-model-preview.md) | WinDbg Preview で組み込みデータモデルのサポートを使用する方法 |

## <a name="extending-the-data-model"></a>データモデルの拡張

| Title (タイトル)               | 説明        |
| ------------------- | -------------------|
| [JavaScript デバッガー スクリプト](https://docs.microsoft.com/windows-hardware/drivers/debugger/javascript-debugger-scripting) | JavaScript を使用してデバッガーオブジェクトを理解するスクリプトを作成する方法  |
| [WinDbg プレビュー-スクリプト](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-scripting-preview) |スクリプトに組み込まれている WinDbg Preview の使用  |
| https://github.com/Microsoft/WinDbg-Samples |最新の JavaScript (およびC++) サンプルコードを共有するデバッガーチーム GitHub サイト。 |
|[JavaScript 拡張機能のネイティブデバッガーオブジェクト](https://docs.microsoft.com/windows-hardware/drivers/debugger/native-objects-in-javascript-extensions) | 共通オブジェクトを使用して、それらの属性と動作に関する参照情報を提供する方法について説明します。|

## <a name="ttd-basics"></a>TTD の基礎

| Title (タイトル)               | 説明        |
| ------------------- | -------------------|
| [タイムトラベルのデバッグ-概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-overview) | TTD の概要 |
[タイムトラベルデバッグ-サンプルアプリのチュートリアル](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-walkthrough) |  タイムトラベルを行うには、このチュートリアルをお試しください |

## <a name="ttd-queries"></a>TTD クエリ
| Title (タイトル)               | 説明        |
| ------------------- | -------------------|
| [タイムトラベルデバッグオブジェクトの概要につい](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-object-model)て説明します。 |データモデルを使用して、タイムトラベルトレースのクエリを実行できます。  
|  https://github.com/Microsoft/WinDbg-Samples/blob/master/TTDQueries/tutorial-instructions.md |TTD クエリを使用してC++コードをデバッグし、問題のあるコードを見つける方法に関するチュートリアル |
| https://github.com/Microsoft/WinDbg-Samples/tree/master/TTDQueries/app-sample | ラボで使用されているすべてのコードは、こちらから入手できます。

## <a name="videos"></a>ビデオ

これらの[デフラグツール](https://channel9.msdn.com/Shows/Defrag-Tools)のエピソードをご覧になり、Windbg Preview の動作を確認してください。  

| Title (タイトル)               | 説明        |
|-------------------- |--------------------|
| [デフラグツール #182](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-182-WinDbg-Preview-Part-1) |Tim、チャド、Andy では、WinDbg Preview の基本と一部の機能について紹介します。 |
| [デフラグツール #183](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-183-WinDbg-Preview-Part-2) | チャド、Tim、およびでは、WinDbg Preview を使用して、簡単なデモをご覧ください |
| [デフラグツール #184](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-184-JavaScript-in-WinDbg-Preview) | WinDbg Preview でのスクリプト作成機能の使用に関する請求と Andrew |
| [デフラグツール #185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) | James と Ivette が時間旅行のデバッグを提供し、概要を説明します |
| [デフラグツール #186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) | James と JCAB が高度なタイムトラベルデバッグをカバーする |

## <a name="installation-and-getting-connected"></a>インストールと接続の取得 

| Title (タイトル)               | 説明        |
| ------------------- | -------------------|
| [WinDbg プレビュー - インストール](windbg-install-preview.md) | インストールの指示 |
| [WinDbg プレビュー - ユーザーモード セッションの開始](windbg-user-mode-preview.md) | ユーザー モード  |
| [WinDbg プレビュー - カーネルモード セッションの開始](windbg-kernel-mode-preview.md) | カーネル モード |
