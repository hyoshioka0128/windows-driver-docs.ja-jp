---
title: リソースのデバッグ
description: Windows のツールのデバッグを使用して、ドライバー、アプリケーション、および Windows システム上のサービスをデバッグします。
ms.assetid: F2111416-EC6C-4967-B123-9A6101040561
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb2431ebd44c6e3c2338b7859e3daf03b7988c07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559875"
---
# <a name="debugging-resources"></a>リソースのデバッグ


Windows のツールのデバッグを使用して、ドライバー、アプリケーション、および Windows システム上のサービスをデバッグします。 中核的なツール セット内のエンジンのデバッグには、Windows のデバッガーは呼び出されます。 Windows 8 以降、Visual Studio を使用して、Windows デバッガーのインターフェイスとして。 従来のインターフェイス (WinDbg、CDB、NTSD) ツールを Windows のデバッグに含まれているを使用することもできます。

## <a name="span-idgettingstartedwithdebuggingtoolsforwindowsspanspan-idgettingstartedwithdebuggingtoolsforwindowsspanspan-idgettingstartedwithdebuggingtoolsforwindowsspangetting-started-with-debugging-tools-for-windows"></a><span id="Getting_Started_with_Debugging_Tools_for_Windows"></span><span id="getting_started_with_debugging_tools_for_windows"></span><span id="GETTING_STARTED_WITH_DEBUGGING_TOOLS_FOR_WINDOWS"></span>Windows 用デバッグ ツールの概要


-   [Windows デバッグ](index.md)

## <a name="span-idinstallingdebuggingtoolsforwindowsspanspan-idinstallingdebuggingtoolsforwindowsspanspan-idinstallingdebuggingtoolsforwindowsspaninstalling-debugging-tools-for-windows"></a><span id="Installing_Debugging_Tools_for_Windows"></span><span id="installing_debugging_tools_for_windows"></span><span id="INSTALLING_DEBUGGING_TOOLS_FOR_WINDOWS"></span>Windows 用デバッグ ツールをインストールします。


-   [ダウンロードして Windows 用デバッグ ツールをインストールします。](https://msdn.microsoft.com/windows/hardware/gg463009)

## <a name="span-iddebuggerhow-tosspanspan-iddebuggerhow-tosspanspan-iddebuggerhow-tosspandebugger-how-tos"></a><span id="Debugger_How-Tos"></span><span id="debugger_how-tos"></span><span id="DEBUGGER_HOW-TOS"></span>デバッガーの操作方法


-   [高度なドライバーは、次のデバッグ:第 1 部\[メディア ファイル\]](https://download.microsoft.com/download/B/1/6/B161948D-EDE1-4AEF-8776-AD485CDDCD9E/TDDR05003.wvx)
-   [高度なドライバーは、次のデバッグ:第 2 部\[メディア ファイル\]](https://download.microsoft.com/download/B/1/6/B161948D-EDE1-4AEF-8776-AD485CDDCD9E/TDDR05004.wvx)
-   [不要にするデバッガーが不要なシンボルを検索します。](https://msdn.microsoft.com/library/windows/hardware/gg463239)
-   [カーネル モード ドライバー フレームワーク ドライバーのデバッグ](https://msdn.microsoft.com/library/windows/hardware/gg463020)
-   [ドライバーを WDF のデバッグ](https://msdn.microsoft.com/library/windows/hardware/ff540790)
-   [さまざまなドライバーとサブシステムの詳細なデバッグ トレースを有効にする方法](https://support.microsoft.com/default.aspx?scid=kb;en-us;q314743)
-   [ドライバーのデバッグ](https://msdn.microsoft.com/windows-drivers/develop/debugging_a_driver)
-   [**BCDEdit/dbgsettings**](https://msdn.microsoft.com/library/windows/hardware/ff542187)
-   [ドライバーをデバッグするためのツール](https://msdn.microsoft.com/library/windows/hardware/ff552951)(WDK ドキュメント)

## <a name="span-idknowledgebasearticlesfordebuggingspanspan-idknowledgebasearticlesfordebuggingspanspan-idknowledgebasearticlesfordebuggingspanknowledge-base-articles-for-debugging"></a><span id="Knowledge_base_articles_for_debugging"></span><span id="knowledge_base_articles_for_debugging"></span><span id="KNOWLEDGE_BASE_ARTICLES_FOR_DEBUGGING"></span>デバッグのサポート技術情報記事


さまざまな[サポート技術情報の記事](https://support.microsoft.com)デバッグ関連のトピックを利用します。 このページでは、デバッグに関連する製品サポートのリンクの例をいくつか提供します。

-   [2816225:デバッグ モードを有効にすると Windows デバッガーが接続されていない場合にハングするには](https://support.microsoft.com/kb/2816225/)
-   [311503:Microsoft シンボル サーバーを使用して、デバッグ シンボル ファイルを入手するには](https://support.microsoft.com/kb/311503)
-   [Q248413:情報:NDIS カーネル デバッガー拡張機能](https://support.microsoft.com/kb/248413)
-   [(Q121366):情報:PDB and DBG Files - は何かとそのしくみ](https://support.microsoft.com/kb/121366)
-   [Q121543:リモート デバッグ用の設定](https://support.microsoft.com/kb/121543)
-   [Q129845:Microsoft を呼び出す前にブルー スクリーンの準備](https://support.microsoft.com/kb/129845)
-   [Q128372:デバイス ドライバーからシンボルを削除する方法](https://support.microsoft.com/kb/128372)
-   [Q97858:CTRL + C 例外の処理の Windbg](https://support.microsoft.com/kb/97858)
-   [Q102351:リダイレクトを使用してコンソール アプリのデバッグ](https://support.microsoft.com/kb/102351)
-   [Q117559:INF:相互に関連付ける Spid、Kpid、スレッドのインスタンスにする方法](https://support.microsoft.com/kb/117559)
-   [Q121434:ハンドルされていないユーザー モード例外にデバッガーを指定します。](https://support.microsoft.com/kb/121434)
-   [Q133722:Windows 2000 IIS SMTP サービスを手動でテストする方法フラット サンクをデバッグします。](https://support.microsoft.com/kb/133722)
-   [Q148220:[PRB]:Debugger Reports "WARNING: symbols checksum is wrong"](https://support.microsoft.com/kb/148220)
-   [Q137199:[PRB]:デバッガーがデバッグ登録用のブレークポイントを確実に使用できません。](https://support.microsoft.com/kb/137199)
-   [Q100957:[PRB]:MS TEST で駆動型アプリケーションのデバッグ](https://support.microsoft.com/kb/100957)
-   [Q130667:[PRB]:デバッグするときに、F12 原因ハード コーディングされたブレークポイント例外](https://support.microsoft.com/kb/130667)
-   [Q173260:[PRB]:デバッグするときに、同期エラー](https://support.microsoft.com/kb/173260)
-   [Q168609:ヒープの表示 (DH を使用する方法。EXE) ユーティリティ](https://support.microsoft.com/kb/168609)
-   [Q103861:情報:システムを起動するデバッガーを選択します。](https://support.microsoft.com/kb/103861)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[DebugView 監視ツール](https://technet.microsoft.com/sysinternals/bb896647.aspx)

[ドライバー開発者向けコミュニティ リソース](https://msdn.microsoft.com/windows/hardware/gg454517)

[Windows のドライバー署名要件](https://msdn.microsoft.com/library/windows/hardware/gg487317)

[開発者向けキットとツールのサポート](https://msdn.microsoft.com/windows/hardware/gg454528)

 

 






