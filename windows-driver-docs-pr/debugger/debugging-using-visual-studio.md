---
title: Visual Studio を使用したデバッグ
description: Windows Driver Kit (WDK) 8 以降では、ドライバー開発環境と Windows デバッガーが Microsoft Visual Studio に統合されています。
ms.assetid: B961B0C9-FF6C-4F6B-AC15-CA1B405A4C4C
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 344bdf0df5ef685335b0d9bea44c4ef924bf38c0
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534451"
---
# <a name="debugging-using-visual-studio"></a>Visual Studio を使用したデバッグ

Windows Driver Kit (WDK) 8 以降では、ドライバー開発環境と Windows デバッガーが Microsoft Visual Studio に統合されています。 この統合環境では、ドライバーのコーディング、ビルド、パッケージ化、テスト、デバッグ、および配置に必要なツールのほとんどは、Visual Studio のユーザーインターフェイスで利用できます。

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>
 
統合環境を入手するには、まず Visual Studio をインストールしてから、Windows Driver Kit (WDK) をインストールします。 詳細については、「 [Windows Driver Kit (WDK) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)」を参照してください。

通常、カーネルモードのデバッグには2台のコンピューターが必要です。 デバッガーは*ホスト コンピューター*上で実行され、デバッグ対象のコードは*ターゲット コンピューター*上で実行されます。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 1台のコンピューターでユーザーモードのデバッグを実行できますが、場合によっては、別のターゲットコンピューターで実行されているユーザーモードのプロセスをデバッグする必要があります。

Visual Studio 環境では、カーネルモードとユーザーモードのデバッグ用にターゲットコンピューターを構成できます。 カーネルモードのデバッグセッションを確立できます。 ユーザーモードプロセスにアタッチするか、ホストコンピューターまたは対象コンピューターでユーザーモードプロセスを起動してデバッグすることができます。 ダンプファイルを分析することができます。 Visual Studio では、ターゲットコンピューター上でのドライバーの署名、展開、インストール、および読み込みを行うことができます。

これらのトピックでは、Visual Studio を使用して、ドライバーのデバッグに関連するいくつかのタスクを実行する方法について説明します。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [Visual Studio を使用したユーザーモード プロセスのデバッグ](debugging-a-user-mode-process-using-visual-studio.md)
-   [Visual Studio を使用してダンプ ファイルを開く](opening-a-crash-dump-file-using-visual-studio.md)
-   [Visual Studio でのカーネルモード デバッグ](performing-kernel-mode-debugging-using-visual-studio.md)
-   [Visual Studio のデバッグ セッションの終了](ending-a-debugging-session-in-visual-studio.md)
-   [Visual Studio でのシンボルと実行可能イメージ パスの設定](setting-symbol-and-source-paths-in-visual-studio.md)
-   [Visual Studio を使用したリモート デバッグ](remote-debugging-using-visual-studio.md)
-   [Visual Studio でのデバッガー コマンドの入力](entering-debugger-commands-in-visual-studio.md)
-   [Visual Studio でのブレークポイントの設定](setting-breakpoints-in-visual-studio.md)
-   [Visual Studio でのコール スタックの表示](viewing-the-call-stack-in-visual-studio.md)
-   [Visual Studio でのソース コードのデバッグ](viewing-source-and-assembly-code-in-visual-studio.md)
-   [Visual Studio でのメモリとレジスタの表示と編集](viewing-memory--variables--and-registers-in-visual-studio.md)
-   [Visual Studio でのスレッドとプロセスの制御](viewing-threads-and-processes-in-visual-studio.md)
-   [Visual Studio での例外とイベントの構成](configuring-exceptions-and-events-in-visual-studio.md)
-   [Visual Studio でのログ ファイルの保持](keeping-a-log-file-in-visual-studio.md)

 

 





