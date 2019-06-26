---
title: デバッグに関するリソース
description: Windows のツールのデバッグを使用して、ドライバー、アプリケーション、および Windows システム上のサービスをデバッグします。
ms.assetid: F2111416-EC6C-4967-B123-9A6101040561
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 687ba28524fc2d972c600c36838a499cfe3ed0ef
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391972"
---
# <a name="debugging-resources"></a>デバッグに関するリソース


Windows のツールのデバッグを使用して、ドライバー、アプリケーション、および Windows システム上のサービスをデバッグします。 中核的なツール セット内のエンジンのデバッグには、Windows のデバッガーは呼び出されます。 Windows 8 以降、Visual Studio を使用して、Windows デバッガーのインターフェイスとして。 従来のインターフェイス (WinDbg、CDB、NTSD) ツールを Windows のデバッグに含まれているを使用することもできます。

## <a name="span-idgettingstartedwithdebuggingtoolsforwindowsspanspan-idgettingstartedwithdebuggingtoolsforwindowsspanspan-idgettingstartedwithdebuggingtoolsforwindowsspangetting-started-with-debugging-tools-for-windows"></a><span id="Getting_Started_with_Debugging_Tools_for_Windows"></span><span id="getting_started_with_debugging_tools_for_windows"></span><span id="GETTING_STARTED_WITH_DEBUGGING_TOOLS_FOR_WINDOWS"></span>Windows 用デバッグ ツールの概要


-   [Windows デバッグ](index.md)

## <a name="span-idinstallingdebuggingtoolsforwindowsspanspan-idinstallingdebuggingtoolsforwindowsspanspan-idinstallingdebuggingtoolsforwindowsspaninstalling-debugging-tools-for-windows"></a><span id="Installing_Debugging_Tools_for_Windows"></span><span id="installing_debugging_tools_for_windows"></span><span id="INSTALLING_DEBUGGING_TOOLS_FOR_WINDOWS"></span>Windows 用デバッグ ツールをインストールします。


-   [ダウンロードして Windows 用デバッグ ツールをインストールします。](https://msdn.microsoft.com/windows/hardware/gg463009)

## <a name="span-iddebuggerhow-tosspanspan-iddebuggerhow-tosspanspan-iddebuggerhow-tosspandebugger-how-tos"></a><span id="Debugger_How-Tos"></span><span id="debugger_how-tos"></span><span id="DEBUGGER_HOW-TOS"></span>デバッガーの操作方法


-   [高度なドライバーは、次のデバッグ:第 1 部\[メディア ファイル\]](https://download.microsoft.com/download/B/1/6/B161948D-EDE1-4AEF-8776-AD485CDDCD9E/TDDR05003.wvx)
-   [高度なドライバーは、次のデバッグ:第 2 部\[メディア ファイル\]](https://download.microsoft.com/download/B/1/6/B161948D-EDE1-4AEF-8776-AD485CDDCD9E/TDDR05004.wvx)
-   [不要にするデバッガーが不要なシンボルを検索します。](https://docs.microsoft.com/windows-hardware/drivers/debugger/avoiding-debugger-searches-for-unneeded-symbols)
-   [カーネル モード ドライバー フレームワーク ドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-kernel-mode-driver-framework-drivers)
-   [ドライバーを WDF のデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)
-   [さまざまなドライバーとサブシステムの詳細なデバッグ トレースを有効にする方法](https://support.microsoft.com/en-us)
-   [ドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers)
-   [**BCDEdit/dbgsettings**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--dbgsettings)
-   [ドライバーをデバッグするためのツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-debugging-drivers)(WDK ドキュメント)

## <a name="span-idknowledgebasearticlesfordebuggingspanspan-idknowledgebasearticlesfordebuggingspanspan-idknowledgebasearticlesfordebuggingspanknowledge-base-articles-for-debugging"></a><span id="Knowledge_base_articles_for_debugging"></span><span id="knowledge_base_articles_for_debugging"></span><span id="KNOWLEDGE_BASE_ARTICLES_FOR_DEBUGGING"></span>デバッグのサポート技術情報記事


さまざまな[サポート技術情報の記事](https://support.microsoft.com/en-us)デバッグ関連のトピックを利用します。 このページでは、デバッグに関連する製品サポートのリンクの例をいくつか提供します。

-   [2816225:デバッグ モードを有効にすると Windows デバッガーが接続されていない場合にハングするには](https://support.microsoft.com/help/2816225/enabling-debug-mode-causes-windows-to-hang-if-no-debugger-is-connected/)
-   [311503:Microsoft シンボル サーバーを使用して、デバッグ シンボル ファイルを入手するには](https://support.microsoft.com/help/311503)
-   [Q248413:情報:NDIS カーネル デバッガー拡張機能](https://support.microsoft.com/help/248413)
-   [(Q121366):情報:PDB and DBG Files - は何かとそのしくみ](https://support.microsoft.com/help/121366)
-   [Q121543:リモート デバッグ用の設定](https://support.microsoft.com/help/121543)
-   [Q129845:Microsoft を呼び出す前にブルー スクリーンの準備](https://support.microsoft.com/help/129845)
-   [Q128372:デバイス ドライバーからシンボルを削除する方法](https://support.microsoft.com/help/128372)
-   [Q97858:CTRL + C 例外の処理の Windbg](https://support.microsoft.com/help/97858)
-   [Q102351:リダイレクトを使用してコンソール アプリのデバッグ](https://support.microsoft.com/help/102351)
-   [Q117559:INF:相互に関連付ける Spid、Kpid、スレッドのインスタンスにする方法](https://support.microsoft.com/help/117559)
-   [Q121434:ハンドルされていないユーザー モード例外にデバッガーを指定します。](https://support.microsoft.com/help/121434)
-   [Q133722:Windows 2000 IIS SMTP サービスを手動でテストする方法フラット サンクをデバッグします。](https://support.microsoft.com/help/133722)
-   [Q148220:[PRB]:Debugger Reports "WARNING: symbols checksum is wrong"](https://support.microsoft.com/help/148220)
-   [Q137199:[PRB]:デバッガーがデバッグ登録用のブレークポイントを確実に使用できません。](https://support.microsoft.com/help/137199)
-   [Q100957:[PRB]:MS TEST で駆動型アプリケーションのデバッグ](https://support.microsoft.com/help/100957)
-   [Q130667:[PRB]:デバッグするときに、F12 原因ハード コーディングされたブレークポイント例外](https://support.microsoft.com/help/130667)
-   [Q173260:[PRB]:デバッグするときに、同期エラー](https://support.microsoft.com/help/173260)
-   [Q168609:ヒープの表示 (DH を使用する方法。EXE) ユーティリティ](https://support.microsoft.com/help/168609)
-   [Q103861:情報:システムを起動するデバッガーを選択します。](https://support.microsoft.com/help/103861)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[DebugView 監視ツール](https://technet.microsoft.com/sysinternals/bb896647.aspx)

[ドライバー開発者向けコミュニティ リソース](https://msdn.microsoft.com/windows/hardware/gg454517)

[Windows のドライバー署名の要件](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn653563(v=vs.85))

[開発者向けキットとツールのサポート](https://docs.microsoft.com/previous-versions/gg454528(v=msdn.10))

 

 






