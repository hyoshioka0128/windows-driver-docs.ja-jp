---
ms.assetid: 0FEF982B-7FEE-47C8-A906-F881E9D8F3D7
title: コード分析ツールと検証ツールを使ったドライバーの分析
description: コード分析ツールと検証ツールは、ソース コードを体系的に分析することによって、ドライバーの安定性と信頼性の向上に役立ちます。
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3b5de3389a80e5b9bd7c445164d519360fc7f424
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518590"
---
# <a name="analyzing-a-driver-using-code-analysis-and-verification-tools"></a>コード分析ツールと検証ツールを使ったドライバーの分析

コード分析ツールと検証ツールは、ソース コードを体系的に分析することによって、ドライバーの安定性と信頼性の向上に役立ちます。 コンパイラや従来の実行時テストでは見逃されるエラーを検出できます。 また、ドライバーが Windows オペレーティング システム カーネルと正しく情報をやり取りしているかどうかを調べます。 Microsoft Visual Studio と Windows Driver Kit (WDK) を使うと、コード分析ツールと検証ツールをビルド プロセスの一部として実行するように構成したり、あらかじめ決めておいた時刻にツールがドライバーを分析するようにスケジュールしたりすることができます。

## <a name="span-idcccodeanalysistoolforwindowsdriversspanspan-idcccodeanalysistoolforwindowsdriversspanspan-idcccodeanalysistoolforwindowsdriversspancc-code-analysis-tool-for-windows-drivers"></a><span id="C_C___Code_Analysis_Tool_for_Windows_Drivers"></span><span id="c_c___code_analysis_tool_for_windows_drivers"></span><span id="C_C___CODE_ANALYSIS_TOOL_FOR_WINDOWS_DRIVERS"></span>Windows ドライバー用 C/C++ コード分析ツール


Windows 8 リリースの WDK には、Visual Studio に含まれている C/C++ コード分析ツールの拡張機能が用意されています。 具体的には、カーネル モード ドライバーのコード内のエラーを検出するように設計された専用のドライバー モジュールが提供されます。 このドライバー モジュールは、C/C++ コード分析ツールに統合されます。

**用途:** C/C++ コード分析ツールは、開発サイクルのごく初期 (コードを正しくコンパイルした直後) のドライバーに実行できます。

Visual Studio のコード分析ツールについて詳しくは、以下のトピックをご覧ください。

-   [コード分析によるアプリケーション品質の分析](https://go.microsoft.com/fwlink/p/?linkid=226836)
-   [ドライバーのコード分析](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454182)
-   [ドライバーのコード分析を実行する方法](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454219)
-   [C/C++ コードの欠陥を減らすための SAL 注釈の使用](https://go.microsoft.com/fwlink/p/?linkid=247283)
-   [Windows ドライバーの SAL 2.0 注釈](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454237)

**注**  以前のバージョンの WDK では、コード分析用のドライバー固有のモジュールが、PREfast for Drivers (PFD) と呼ばれるスタンドアロン ツールに組み込まれていました。 また、PREfast for Drivers は、Microsoft Automated Code Review (OACR) の一部として、WDK ビルド環境に統合されていました。

 

## <a name="span-idstaticdriververifierspanspan-idstaticdriververifierspanspan-idstaticdriververifierspanstatic-driver-verifier"></a><span id="Static_Driver_Verifier"></span><span id="static_driver_verifier"></span><span id="STATIC_DRIVER_VERIFIER"></span>静的ドライバー検証ツール


静的ドライバー検証ツール (SDV) は、Windows カーネル モード ドライバーのソース コードを体系的に分析する、静的な検証ツールです。 SDV は、ドライバーが Windows オペレーティング システム カーネルと正しく情報をやり取りしているかどうかを調べます。 SDV の起動は、Visual Studio の **[ドライバー]** メニューから行うか、**[Visual Studio コマンド プロンプト]** ウィンドウから行います。

**用途:** 静的ドライバー検証ツールは、開発サイクルの初期に、正しくコンパイルされたドライバーに対して実行します。 また、テスト サイクルを始める前に実行します。

静的ドライバー検証ツールについて詳しくは、以下のトピックをご覧ください。

-   概要:[静的ドライバー検証ツール](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552808)
-   手順[ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454281)


 

 

 





