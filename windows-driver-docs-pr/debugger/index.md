---
title: Debugging Tools for Windows (WinDbg、KD、CDB、NTSD)
description: ここでは、Debugging Tools for Windows の概要について説明します。 このツール セットには、WinDbg および他のデバッガーが含まれます。
ms.assetid: 938ef180-84de-442f-9b6c-1138c2fc8d5a
keywords:
- Debugging Tools for Windows
- Windows のデバッグ
- Windows デバッガー
- カーネル デバッグ
- カーネル デバッガー
- WinDbg
ms.date: 02/22/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 982379cd73e2949bdcd7d0bc46ff53e1fce55f2d
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74861424"
---
# <a name="debugging-tools-for-windows-windbg-kd-cdb-ntsd"></a>Debugging Tools for Windows (WinDbg、KD、CDB、NTSD)

ここでは、Debugging Tools for Windows の概要について説明します。 このツール セットには、WinDbg および他のデバッガーが含まれます。


## <a name="span-id3_ways_to_get_debugging_tools_for_windowsspanspan-id3_ways_to_get_debugging_tools_for_windowsspanspan-id3_ways_to_get_debugging_tools_for_windowsspaninstall-debugging-tools-for-windows"></a><span id="3_ways_to_get_Debugging_Tools_for_Windows"></span><span id="3_ways_to_get_debugging_tools_for_windows"></span><span id="3_WAYS_TO_GET_DEBUGGING_TOOLS_FOR_WINDOWS"></span>Debugging Tools for Windows のインストール

Debugging Tools for Windows は、開発キットの一部として、またはスタンドアロン ツール セットとして入手できます。

-   **WDK の一部として**

    Debugging Tools for Windows は Windows Driver Kit (WDK) に含まれています。 WDK を入手するには、「[Windows Driver Kit (WDK) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)」をご覧ください。


-   **Windows SDK の一部として**

    Debugging Tools for Windows は Windows ソフトウェア開発キット (SDK) に含まれています。 インストーラーまたは ISO イメージをダウンロードするには、Windows デベロッパー センターの「[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)」を参照してください。


-   **スタンドアロン ツール セットとして**

    Windows SDK または WDK なしで、Debugging Tools for Windows のみをインストールするには、Windows SDK のインストールを開始し、機能の一覧で **[Debugging Tools for Windows]** のみを選択してインストールします (その他すべての機能を選択を解除します)。 インストーラーまたは ISO イメージをダウンロードするには、Windows デベロッパー センターの「[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)」を参照してください。


## <a name="span-idgetting_started_with_windows_debuggingspanspan-idgetting_started_with_windows_debuggingspanspan-idgetting_started_with_windows_debuggingspanget-started-with-windows-debugging"></a><span id="Getting_Started_with_Windows_Debugging"></span><span id="getting_started_with_windows_debugging"></span><span id="GETTING_STARTED_WITH_WINDOWS_DEBUGGING"></span>Windows のデバッグの概要

Windows のデバッグの概要については、「[Getting Started with Windows Debugging](getting-started-with-windows-debugging.md)」(Windows のデバッグの概要) をご覧ください。

カーネル モード ドライバーのデバッグの概要については、「[ユニバーサル ドライバーをデバッグする - ステップ バイ ステップ ラボ (Echo カーネル モード))](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)」をご覧ください。 このステップ バイ ステップ ラボでは、WinDbg を使用して、カーネルモード ドライバー フレームワーク (KMDF) を使用するサンプル ドライバー、Echo をデバッグする方法を説明します。


## <a name="span-iddebugging_environmentsspanspan-iddebugging_environmentsspanspan-iddebugging_environmentsspandebugging-environments"></a><span id="Debugging_environments"></span><span id="debugging_environments"></span><span id="DEBUGGING_ENVIRONMENTS"></span>デバッグ環境

コンピューターに Visual Studio と WDK がインストールされている場合は、6 つのデバッグ環境を使用できます。 これらの環境について詳しくは、「[デバッグ環境](debuggers-in-the-debugging-tools-for-windows-package.md)」を参照してください。

これらのデバッグ環境で提供されるユーザー インターフェイスはすべて、基になる同じデバッグ エンジンに対するものであり、このエンジンは Windows Symbolic Debugger Engine (Dbgeng.dll) で実装されます。 このデバッグ エンジンは "*Windows デバッガー*" とも呼ばれ、6 つのデバッグ環境の総称も "*Windows デバッガー*" です。

> [!NOTE]
> Visual Studio は独自のデバッグ環境とデバッグ エンジンを備えており、それらはまとめて "*Visual Studio デバッガー*" と呼ばれます。 Visual Studio でのデバッグについては、「[Visual Studio でのデバッグ](https://docs.microsoft.com/visualstudio/debugger/)」をご覧ください。 C# のようなマネージド コードをデバッグする場合は、通常、Visual Studio デバッガーを使用して始めるのが最も簡単な方法です。


## <a name="span-idwindows_debuggersspanspan-idwindows_debuggersspanspan-idwindows_debuggersspanwindows-debuggers"></a><span id="Windows_debuggers"></span><span id="windows_debuggers"></span><span id="WINDOWS_DEBUGGERS"></span>Windows デバッガー

Windows デバッガーは x86 ベース、x64 ベース、ARM ベースのプロセッサで実行でき、これらの同じアーキテクチャで実行されるコードをデバッグできます。 デバッガーとデバッグ対象のコードは、同じコンピューター上で実行されることも、別々のコンピューターで実行されることもあります。 いずれの場合も、デバッガーが実行されるコンピューターは "*ホスト コンピューター*" と呼ばれ、デバッグ対象のコンピューターは "*ターゲット コンピューター*" と呼ばれます。 Windows デバッガーでは、ホストとターゲットの両方のコンピューターについて、次のバージョンの Windows がサポートされます。

-   Windows 10、Windows Server 2016
-   Windows 8.1、Windows Server 2012 R2
-   Windows 8、Windows Server 2012
-   Windows 7、Windows Server 2008 R2


## <a name="span-idsymbols_and_symbol_filesspanspan-idsymbols_and_symbol_filesspanspan-idsymbols_and_symbol_filesspansymbols-and-symbol-files"></a><span id="Symbols_and_Symbol_Files"></span><span id="symbols_and_symbol_files"></span><span id="SYMBOLS_AND_SYMBOL_FILES"></span>シンボルとシンボル ファイル

シンボル ファイルには、実行可能なバイナリの実行時に必要とされないさまざまなデータが格納されますが、シンボル ファイルはコードのデバッグ時には非常に便利です。 シンボル ファイルの作成と使用の詳細については、「[Symbols for Windows debugging (WinDbg, KD, CDB, NTSD)](symbols.md)」 (Windows のデバッグで使用するシンボル (WinDbg、KD、CDB、NTSD)) を参照してください。


## <a name="span-idblue_screens_and_crash_dump_filesspanspan-idblue_screens_and_crash_dump_filesspanspan-idblue_screens_and_crash_dump_filesspanblue-screens-and-crash-dump-files"></a><span id="Blue_Screens_and_crash_dump_files"></span><span id="blue_screens_and_crash_dump_files"></span><span id="BLUE_SCREENS_AND_CRASH_DUMP_FILES"></span>ブルー スクリーンとクラッシュ ダンプ ファイル

Windows の動作が停止してブルー スクリーンが表示された場合は、コンピューターはデータの損失を防ぐためにすぐにシャットダウンされて、バグ チェック コードが表示されます。 詳細については、「[Bug Checks (Blue Screens)](bug-checks--blue-screens-.md)」(バグ チェック (ブルー スクリーン)) を参照してください。 WinDbg およびその他の Windows デバッガーを使用して、Windows のシャットダウン時に作成されるクラッシュ ダンプ ファイルを分析します。 詳細については、「[Crash dump analysis using the Windows debuggers (WinDbg) ](crash-dump-files.md)」(Windows デバッガーを用いたクラッシュ ダンプ分析 (WinDbg)) を参照してください。


## <a name="span-idtools_and_utilitiesspanspan-idtools_and_utilitiesspanspan-idtools_and_utilitiesspantools-and-utilities"></a><span id="Tools_and_utilities"></span><span id="tools_and_utilities"></span><span id="TOOLS_AND_UTILITIES"></span>ツールとユーティリティ

デバッガーだけでなく、Debugging Tools for Windows にはデバッグに役立つ一連のツールが含まれています。 ツールの詳細な一覧については、「[Tools Included in Debugging Tools for Windows](extra-tools.md)」(Debugging Tools for Windows に含まれるツール) を参照してください。


## <a name="span-idadditional_documentationspanspan-idadditional_documentationspanspan-idadditional_documentationspanadditional-documentation"></a><span id="Additional_documentation"></span><span id="additional_documentation"></span><span id="ADDITIONAL_DOCUMENTATION"></span>その他のドキュメント

Debugging Tools for Windows に関するその他の情報については、「[Debugging Resources](debugging-resources.md)」 (デバッグに関するリソース) を参照してください。 Windows 10 での新機能については、「[Debugging Tools for Windows: New for Windows 10](debugging-tools-for-windows--new-for-windows-10.md)」 (Debugging Tools for Windows: Windows 10 での新機能) を参照してください。
