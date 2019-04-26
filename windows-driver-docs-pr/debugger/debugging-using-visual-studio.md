---
title: Visual Studio を使用したデバッグ
description: Windows Driver Kit (WDK) 8、ドライバーの開発環境および Windows のデバッガーは、Microsoft Visual Studio に統合されて開始しています。
ms.assetid: B961B0C9-FF6C-4F6B-AC15-CA1B405A4C4C
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: d52bf3207354471280f523c1106664cd2723e516
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346318"
---
# <a name="debugging-using-visual-studio"></a>Visual Studio を使用したデバッグ

Windows Driver Kit (WDK) 8、ドライバーの開発環境および Windows のデバッガーは、Microsoft Visual Studio に統合されて開始しています。 この統合された環境でのコーディング、構築、する必要があるツールのほとんどをパッケージ化、テスト、デバッグ、およびドライバーの展開がで使用できます、Visual Studio ユーザー インターフェイス。

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>
 
統合環境を取得するには、最初に、Visual Studio をインストールし、Windows Driver Kit (WDK) をインストールします。 詳細については、次を参照してください。 [Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p?linkid=391063)します。

通常カーネル モードのデバッグには、2 台のコンピューターが必要です。 デバッガーは*ホスト コンピューター*上で実行され、デバッグ対象のコードは*ターゲット コンピューター*上で実行されます。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 場合によっては別のターゲット コンピューターで実行されているユーザー モード プロセスをデバッグする場合がありますが、1 台のコンピューターでユーザー モードのデバッグを行うことができます。

Visual Studio 環境では、カーネル モードとユーザー モードのデバッグのターゲット コンピュータを構成できます。 カーネル モードのデバッグ セッションを確立することができます。 ユーザー モード プロセスにアタッチまたは起動して、ホスト コンピューターまたは対象のコンピュータ上のユーザー モード プロセスをデバッグできます。 ダンプ ファイルを分析することができます。 Visual Studio でサインイン、デプロイをインストールしてターゲット コンピューター上のドライバーの読み込み。

これらのトピックでは、Visual Studio を使用して、いくつかのドライバーのデバッグに関連するタスクを実行する方法を示します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [Visual Studio を使用してユーザー モード プロセスのデバッグ](debugging-a-user-mode-process-using-visual-studio.md)
-   [Visual Studio を使用してダンプ ファイルを開く](opening-a-crash-dump-file-using-visual-studio.md)
-   [カーネル モードの Visual Studio でのデバッグ](performing-kernel-mode-debugging-using-visual-studio.md)
-   [Visual Studio でのデバッグ セッションを終了します。](ending-a-debugging-session-in-visual-studio.md)
-   [Visual Studio でのシンボルと実行可能イメージのパスの設定](setting-symbol-and-source-paths-in-visual-studio.md)
-   [リモート デバッグを使用して Visual Studio](remote-debugging-using-visual-studio.md)
-   [Visual Studio のデバッガー コマンドを入力します。](entering-debugger-commands-in-visual-studio.md)
-   [Visual Studio でブレークポイントの設定](setting-breakpoints-in-visual-studio.md)
-   [Visual Studio での呼び出し履歴の表示](viewing-the-call-stack-in-visual-studio.md)
-   [ソース コードを Visual Studio でのデバッグ](viewing-source-and-assembly-code-in-visual-studio.md)
-   [メモリとレジスタ Visual Studio で表示および編集](viewing-memory--variables--and-registers-in-visual-studio.md)
-   [スレッドと Visual Studio でのプロセスを制御します。](viewing-threads-and-processes-in-visual-studio.md)
-   [Visual Studio での例外とイベントの構成](configuring-exceptions-and-events-in-visual-studio.md)
-   [Visual Studio でログ ファイルを維持する方法](keeping-a-log-file-in-visual-studio.md)

 

 





