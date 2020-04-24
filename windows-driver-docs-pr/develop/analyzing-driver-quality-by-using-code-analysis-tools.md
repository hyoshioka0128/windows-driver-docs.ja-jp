---
ms.assetid: 0FEF982B-7FEE-47C8-A906-F881E9D8F3D7
title: コード分析ツールと検証ツールを使ったドライバーの分析
description: コード分析ツールと検証ツールは、ソース コードを体系的に分析することによって、ドライバーの安定性と信頼性の向上に役立ちます。
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: ed0b8345d86e3f15f21a7d8a4443a8c618dd1358
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67369322"
---
# <a name="analyzing-a-driver-using-code-analysis-and-verification-tools"></a>コード分析ツールと検証ツールを使ったドライバーの分析

コード分析ツールと検証ツールは、ソース コードを体系的に分析することによって、ドライバーの安定性と信頼性の向上に役立ちます。 コンパイラや従来の実行時テストでは見逃されるエラーを検出できます。 また、ドライバーが Windows オペレーティング システム カーネルと正しく情報をやり取りしているかどうかを調べます。 Microsoft Visual Studio と Windows Driver Kit (WDK) を使うと、コード分析ツールと検証ツールをビルド プロセスの一部として実行するように構成したり、あらかじめ決めておいた時刻にツールがドライバーを分析するようにスケジュールしたりすることができます。

## <a name="span-idc_c___code_analysis_tool_for_windows_driversspanspan-idc_c___code_analysis_tool_for_windows_driversspanspan-idc_c___code_analysis_tool_for_windows_driversspancc-code-analysis-tool-for-windows-drivers"></a><span id="C_C___Code_Analysis_Tool_for_Windows_Drivers"></span><span id="c_c___code_analysis_tool_for_windows_drivers"></span><span id="C_C___CODE_ANALYSIS_TOOL_FOR_WINDOWS_DRIVERS"></span>Windows ドライバー用 C/C++ コード分析ツール


Windows 8 リリースの WDK には、Visual Studio に含まれている C/C++ コード分析ツールの拡張機能が用意されています。 具体的には、カーネル モード ドライバーのコード内のエラーを検出するように設計された専用のドライバー モジュールが提供されます。 このドライバー モジュールは、C/C++ コード分析ツールに統合されます。

**用途:** C/C++ コード分析ツールは、開発サイクルのごく初期 (コードを正しくコンパイルした直後) のドライバーに実行できます。

Visual Studio のコード分析ツールについて詳しくは、以下のトピックをご覧ください。

-   [コード分析によるアプリケーション品質の分析](https://go.microsoft.com/fwlink/p/?linkid=226836)
-   [ドライバーのコード分析](https://docs.microsoft.com/windows-hardware/drivers/devtest/code-analysis-for-drivers)
-   [ドライバーのコード分析を実行する方法](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-to-run-code-analysis-for-drivers)
-   [C/C++ コードの欠陥を減らすための SAL 注釈の使用](https://go.microsoft.com/fwlink/p/?linkid=247283)
-   [Windows ドライバーの SAL 2.0 注釈](https://docs.microsoft.com/windows-hardware/drivers/devtest/sal-2-annotations-for-windows-drivers)

**注**  以前のバージョンの WDK では、コード分析用のドライバー固有のモジュールが、PREfast for Drivers (PFD) と呼ばれるスタンドアロン ツールに組み込まれていました。 また、PREfast for Drivers は、Microsoft Automated Code Review (OACR) の一部として、WDK ビルド環境に統合されていました。

 

## <a name="span-idstatic_driver_verifierspanspan-idstatic_driver_verifierspanspan-idstatic_driver_verifierspanstatic-driver-verifier"></a><span id="Static_Driver_Verifier"></span><span id="static_driver_verifier"></span><span id="STATIC_DRIVER_VERIFIER"></span>静的ドライバー検証ツール


静的ドライバー検証ツール (SDV) は、Windows カーネル モード ドライバーのソース コードを体系的に分析する、静的な検証ツールです。 SDV は、ドライバーが Windows オペレーティング システム カーネルと正しく情報をやり取りしているかどうかを調べます。 SDV の起動は、Visual Studio の **[ドライバー]** メニューから行うか、 **[Visual Studio コマンド プロンプト]** ウィンドウから行います。

**用途:** 静的ドライバー検証ツールは、開発サイクルの初期に、正しくコンパイルされたドライバーに対して実行します。 また、テスト サイクルを始める前に実行します。

静的ドライバー検証ツールについて詳しくは、以下のトピックをご覧ください。

-   概要:[静的ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)
-   手順[ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)


 

 

 





