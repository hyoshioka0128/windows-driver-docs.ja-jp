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
ms.openlocfilehash: 418e8ca690b1d41046faa8cdba9f62d252725c05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56465675"
---
# <a name="debugging-tools-for-windows-windbg-kd-cdb-ntsd"></a>Debugging Tools for Windows (WinDbg、KD、CDB、NTSD)


ここでは、Debugging Tools for Windows の概要について説明します。 このツール セットには、WinDbg および他のデバッガーが含まれます。

## <a name="span-id3waystogetdebuggingtoolsforwindowsspanspan-id3waystogetdebuggingtoolsforwindowsspanspan-id3waystogetdebuggingtoolsforwindowsspan3-ways-to-get-debugging-tools-for-windows"></a><span id="3_ways_to_get_Debugging_Tools_for_Windows"></span><span id="3_ways_to_get_debugging_tools_for_windows"></span><span id="3_WAYS_TO_GET_DEBUGGING_TOOLS_FOR_WINDOWS"></span>Debugging Tools for Windows を入手する 3 つの方法

-   **WDK の一部として**

    Debugging Tools for Windows は WDK に含まれます。 [WDK はこちらから入手する](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)ことができます。

   
-   **スタンドアロン ツール セットとして**

    Debugging Tools for Windows だけをダウンロードしたい場合は、[Windows SDK をインストール](https://developer.microsoft.com/windows/downloads/windows-10-sdk)し、インストールの間に、**[Debugging Tools for Windows]\(Windows 用デバッグ ツール\)** ボックスをオンにして、他のすべてのボックスをオフにします。


-   **Windows SDK の一部として**

    完全な Windows ソフトウェア開発キット (SDK) をインストールします。 Debugging Tools for Windows は Windows SDK に含まれます。 [Windows SDK はこちらで入手](https://developer.microsoft.com/windows/downloads/windows-10-sdk)できます。


## <a name="span-idgettingstartedwithwindowsdebuggingspanspan-idgettingstartedwithwindowsdebuggingspanspan-idgettingstartedwithwindowsdebuggingspangetting-started-with-windows-debugging"></a><span id="Getting_Started_with_Windows_Debugging"></span><span id="getting_started_with_windows_debugging"></span><span id="GETTING_STARTED_WITH_WINDOWS_DEBUGGING"></span>Windows のデバッグの概要


Windows のデバッグの概要については、「[Getting Started with Windows Debugging](getting-started-with-windows-debugging.md)」(Windows のデバッグの概要) をご覧ください。

カーネル モード ドライバーのデバッグの概要については、「[Debug Universal Drivers - Step by Step Lab (Echo Kernel-Mode)](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)」(ユニバーサル ドライバーをデバッグする - ステップ バイ ステップ ラボ (Echo カーネル モード)) をご覧ください。 このステップ バイ ステップ ラボでは、WinDbg を使用してサンプルの KMDF echo ドライバーをデバッグする方法が示されています。

## <a name="span-iddebuggingenvironmentsspanspan-iddebuggingenvironmentsspanspan-iddebuggingenvironmentsspandebugging-environments"></a><span id="Debugging_environments"></span><span id="debugging_environments"></span><span id="DEBUGGING_ENVIRONMENTS"></span>デバッグ環境


Visual Studio と WDK をインストールした後は、6 つの[デバッグ環境](debuggers-in-the-debugging-tools-for-windows-package.md)を使用できます。 これらのデバッグ環境で提供されるユーザー インターフェイスはすべて、基になる同じデバッグ エンジンに対するものであり、このエンジンは dbgeng.dll で実装されます。 このデバッグ エンジンは "*Windows デバッガー*" と呼ばれ、6 つのデバッグ環境の総称も "*Windows デバッガー*" です。

**注**  Visual Studio は独自のデバッグ環境とデバッグ エンジンを備えており、それらはまとめて "*Visual Studio デバッガー*" と呼ばれます。 Visual Studio でのデバッグについては、[Visual Studio デバッガー](https://go.microsoft.com/fwlink/p/?LinkID=238333)に関する記事をご覧ください。 C# のようなマネージド コードをデバッグする場合は、通常、Visual Studio デバッガーを使用して始めるのが最も簡単な方法です。

 

## <a name="span-idwindowsdebuggersspanspan-idwindowsdebuggersspanspan-idwindowsdebuggersspanwindows-debuggers"></a><span id="Windows_debuggers"></span><span id="windows_debuggers"></span><span id="WINDOWS_DEBUGGERS"></span>Windows デバッガー


Windows デバッガーは x86 ベース、x64 ベース、ARM ベースのプロセッサで実行でき、x86 ベース、x64 ベース、ARM ベースのプロセッサで実行されるコードをデバッグできます。 デバッガーとデバッグ対象のコードは、同じコンピューター上で実行されることも、別々のコンピューターで実行されることもあります。 いずれの場合も、デバッガーが実行されるコンピューターは "*ホスト コンピューター*" と呼ばれ、デバッグ対象のコンピューターは "*ターゲット コンピューター*" と呼ばれます。 Windows デバッガーでは、ホストとターゲットの両方のコンピューターについて、次のバージョンの Windows がサポートされます。

-   Windows 10、Windows Server 2016

-   Windows 8.1、Windows Server 2012 R2

-   Windows 8、Windows Server 2012

-   Windows 7、Windows Server 2008 R2

## <a name="span-idsymbolsandsymbolfilesspanspan-idsymbolsandsymbolfilesspanspan-idsymbolsandsymbolfilesspansymbols-and-symbol-files"></a><span id="Symbols_and_Symbol_Files"></span><span id="symbols_and_symbol_files"></span><span id="SYMBOLS_AND_SYMBOL_FILES"></span>シンボルとシンボル ファイル


シンボル ファイルには、バイナリを実行するときは実際には必要ありませんが、コードをデバッグするときは非常に役に立つ、さまざまなデータが保持されています。 シンボル ファイルの作成と使用の詳細については、「[Symbols for Windows debugging (WinDbg, KD, CDB, NTSD)](symbols.md)」 (Windows のデバッグで使用するシンボル (WinDbg、KD、CDB、NTSD)) を参照してください。

## <a name="span-idbluescreensandcrashdumpfilesspanspan-idbluescreensandcrashdumpfilesspanspan-idbluescreensandcrashdumpfilesspanblue-screens-and-crash-dump-files"></a><span id="Blue_Screens_and_crash_dump_files"></span><span id="blue_screens_and_crash_dump_files"></span><span id="BLUE_SCREENS_AND_CRASH_DUMP_FILES"></span>ブルー スクリーンとクラッシュ ダンプ ファイル


Windows の動作が停止してブルー スクリーンが表示された場合は、コンピューターはデータの損失を防ぐためにすぐにシャットダウンされて、バグ チェック コードが表示されます。 詳細については、「[Bug Checks (Blue Screens)](bug-checks--blue-screens-.md)」(バグ チェック (ブルー スクリーン)) を参照してください。 WinDbg およびその他の Windows デバッガーを使用して、Windows のシャットダウン時に作成されるクラッシュ ダンプ ファイルを分析します。 詳細については、「[Crash dump analysis using the Windows debuggers (WinDbg) ](crash-dump-files.md)」(Windows デバッガーを用いたクラッシュ ダンプ分析 (WinDbg)) を参照してください。

## <a name="span-idtoolsandutilitiesspanspan-idtoolsandutilitiesspanspan-idtoolsandutilitiesspantools-and-utilities"></a><span id="Tools_and_utilities"></span><span id="tools_and_utilities"></span><span id="TOOLS_AND_UTILITIES"></span>ツールとユーティリティ


デバッガーだけでなく、Debugging Tools for Windows にはデバッグに役立つ一連のツールが含まれています。 ツールの詳細な一覧については、「[Tools Included in Debugging Tools for Windows](extra-tools.md)」(Debugging Tools for Windows に含まれるツール) を参照してください。

## <a name="span-idadditionaldocumentationspanspan-idadditionaldocumentationspanspan-idadditionaldocumentationspanadditional-documentation"></a><span id="Additional_documentation"></span><span id="additional_documentation"></span><span id="ADDITIONAL_DOCUMENTATION"></span>その他のドキュメント


Debugging Tools for Windows に関するその他の情報については、「[Debugging Resources](debugging-resources.md)」 (デバッグに関するリソース) を参照してください。 Windows 10 での新機能については、「[Debugging Tools for Windows: New for Windows 10](debugging-tools-for-windows--new-for-windows-10.md)」 (Debugging Tools for Windows: Windows 10 での新機能) を参照してください。

## <a name="span-idinthissectionspanspan-idinthissectionspanspan-idinthissectionspanin-this-section"></a><span id="In_this_section"></span><span id="in_this_section"></span><span id="IN_THIS_SECTION"></span>このセクションの内容


-   [Windows のデバッグの概要](getting-started-with-windows-debugging.md)
-   [デバッグに関するリソース](debugging-resources.md)
-   [デバッガーの操作](debugger-operation-win8.md)
-   [デバッグの手法](debugging-techniques.md)
-   [シンボル](symbols.md)
-   [クラッシュ ダンプ分析](crash-dump-files.md)
-   [バグ チェック (ブルー スクリーン)](bug-checks--blue-screens-.md)
-   [デバッガー リファレンス](debugger-reference.md)

 

 





