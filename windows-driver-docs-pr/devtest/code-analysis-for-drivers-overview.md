---
title: ドライバーのコード分析の概要
description: Windows Driver Kit には、Microsoft Visual Studio Ultimate 2012 のコード分析ツールにドライバー固有の拡張機能が用意されています。
ms.assetid: 2A780608-F386-4838-A4EB-022C2F0EED3B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 692ac4ebc62b7a3ee03a83b5e44ec9d06e6104ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840295"
---
# <a name="code-analysis-for-drivers-overview"></a>ドライバーのコード分析の概要


Windows Driver Kit には、Microsoft Visual Studio の[コード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)に対するドライバー固有の拡張機能が用意されています。 ドライバーのコード分析には、ドライバー、特にカーネルモードドライバーにのみ適用される規則が含まれています。 コードをコンパイルするとすぐに、ドライバーのコード分析によって、コード内の潜在的なエラーが検出される可能性があります。

## <a name="span-idhow_the_code_analysis_tool_worksspanspan-idhow_the_code_analysis_tool_worksspanspan-idhow_the_code_analysis_tool_worksspanhow-the-code-analysis-tool-works"></a><span id="How_the_Code_Analysis_tool_works"></span><span id="how_the_code_analysis_tool_works"></span><span id="HOW_THE_CODE_ANALYSIS_TOOL_WORKS"></span>コード分析ツールの動作


コード分析ツールは、標準コンパイラ Cl.exe およびのビルドユーティリティの呼び出しをインターセプトし、その代わりに、ドライバーのソースコードを分析し、エラーメッセージと警告メッセージのログファイルを作成する CL インターセプトコンパイラを実行します。 コード分析ツールは単独で実行することも、ドライバーのビルド時に実行するようにコード分析ツールを構成することもできます。 コード分析ツールを単独で実行すると (**ソリューションでコード分析を実行 &gt;** )、コード分析レポート ウィンドウに結果が表示されます。 ビルドの一部としてコード分析ツールを実行すると、CL インターセプトコンパイラによってエラーメッセージと警告メッセージのログファイルが作成され、Cl.exe の標準バージョンが呼び出されてビルド出力が生成されます。 結果として得られるオブジェクトファイルは、標準のビルドコマンドによって生成されるものと同じです。

インターセプトコンパイラが実行されると、ドライバーのコード分析によって、コード内の各関数が独立して調査され、コードを介して可能なすべてのパスの実行がシミュレートされます。これにより、一般的なドライバーエラーと、それ以外のコーディング方法が求められます。 コード分析ツールは、大規模なドライバーでも比較的高速に実行されます。生成されたレポートでは、問題が発生していると思われるドライバーコード行が正確に特定されます。

## <a name="span-idthe_types_of_errors_code_analysis_can_detectspanspan-idthe_types_of_errors_code_analysis_can_detectspanspan-idthe_types_of_errors_code_analysis_can_detectspanthe-types-of-errors-code-analysis-can-detect"></a><span id="The_types_of_errors_Code_Analysis_can_detect"></span><span id="the_types_of_errors_code_analysis_can_detect"></span><span id="THE_TYPES_OF_ERRORS_CODE_ANALYSIS_CAN_DETECT"></span>コード分析で検出できるエラーの種類


コード分析では、次のカテゴリのエラーを含む、いくつかの種類のエラーを検出できます。

-   **メモリ:** メモリリークの可能性、逆参照された**NULL**ポインター、初期化されていないメモリへのアクセス、カーネルモードスタックの過剰な使用、プールタグの不適切な使用。

-   **リソース:** ロック、関数の呼び出し時に保持する必要があるリソース、他の関数を呼び出すときに保持してはならないリソースなどのリソースを解放できませんでした。

-   **関数の使用法:** 特定の関数が正しく使用されていない可能性があります。関数の引数の型が厳密にチェックされない関数、特定の古い関数の使用可能性がある関数、および関数呼び出しの可能性があります。IRQL が正しくありません。

-   **浮動小数点の状態:** ドライバーの浮動小数点ハードウェアの状態を保護し、別の IRQL で保存した後に浮動小数点の状態を復元しようとすると失敗します。

-   **優先順位の規則:** C プログラミングの優先順位規則により、プログラマが意図した動作をしない可能性のあるコード。

-   **カーネルモードのコーディング方法:** 不透明なメモリ記述子リスト (MDL) 構造の変更、呼び出された関数によって設定された変数の値の検査、およびセーフ文字列ではなく C/C++文字列操作関数の使用など、エラーが発生する可能性があるコーディング手法、Ntstrsafe.h で定義されている関数。

-   **ドライバー固有のコーディング方法:** 多くの場合、カーネルモードドライバーでのエラーの原因となる特定の操作。 たとえば、すべての i/o 要求パケット (IRP) をコピーするときに、 [*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンで引数をコピーするのではなく、メンバーを変更したり、文字列または構造体の引数へのポインターを保存したりする必要はありません。

## <a name="span-idcode_analysis_warningsspanspan-idcode_analysis_warningsspanspan-idcode_analysis_warningsspancode-analysis-warnings"></a><span id="Code_Analysis_warnings"></span><span id="code_analysis_warnings"></span><span id="CODE_ANALYSIS_WARNINGS"></span>コード分析の警告


コード分析ツールは、規則ベースのモデルを使用して、プログラムまたはドライバーコードのエラーを識別します。 各ルールは、コード分析ツールによってルールの違反が検出された場合に報告される警告に関連付けられています。 ドライバー固有の警告の詳細については、「 [Code Analysis For Drivers warning](prefast-for-drivers-warnings.md)」を参照してください。 Visual Studio のコード分析ツールによって報告される、警告のコアセットの詳細については、「[コード分析の警告](https://go.microsoft.com/fwlink/p/?linkid=226853)」を参照してください。

## <a name="span-idannotationsspanspan-idannotationsspanspan-idannotationsspanannotations"></a><span id="Annotations"></span><span id="annotations"></span><span id="ANNOTATIONS"></span>エンジニアリング


コード分析ツールに用意されている重要な機能の1つに、関数の説明や、ドライバーのソースコード内の他のエンティティに注釈を付ける機能があります。 コード分析ツールには、機能的なスコープがあります。つまり、関数間の相互作用を分析します。 注釈の目的は、呼び出された関数と呼び出し元関数の間にコントラクトの完全な式を提供して、コード分析ツールでコントラクトが満たされているかどうかを確認できるようにすることです。 注釈のもう1つの目的は、関数がどのように使用されるか、およびどのような結果が得られるかを、ユーザーに通知することです。 注釈は、インターフェイスのコントラクトを宣言し、そのコントラクトの達成方法を記述しません。 多くの場合、コード分析ツールを実行した結果、適切な注釈がないことがわかります。注釈を追加すると、不足している注釈に関する警告が抑制され、追加のチェックが有効になります。 詳細については、「 [Windows ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)」を参照してください。 SAL 2.0 の詳細については、「 [Sal 注釈を使用C++した C/コードの欠陥の削減](https://go.microsoft.com/fwlink/p/?linkid=247283)」を参照してください。 Sal 2.0 が SAL 1.0 に置き換えられます。 SAL 2.0 は、Windows 8 用の WDK で使用する必要があります。 ドライバーの SAL 1.0 に関する情報が必要な場合は、Windows 7 用の WDK に同梱されている PREfast for Drivers の注釈に関するドキュメントを参照してください。

## <a name="span-idinterpreting_the_resultspanspan-idinterpreting_the_resultspanspan-idinterpreting_the_resultspaninterpreting-the-result"></a><span id="Interpreting_the_result"></span><span id="interpreting_the_result"></span><span id="INTERPRETING_THE_RESULT"></span>結果の解釈


ドライバーのコード分析は、非常に大規模なドライバーやプログラムを使用している場合でも、簡単に実行でき、高速に実行されます。 開発者の作業は、出力の調査、コード分析ツールによって検出されたエラーの分析、およびコード分析ツールが誤って解釈した有効なコードからの実際のコーディングエラーの識別を行います。

コード分析ツールによって検出される可能性のある各警告について説明する包括的なリファレンスについては、「[ドライバーの警告のコード分析](prefast-for-drivers-warnings.md)」を参照してください。 Visual Studio のコード分析ツールによって報告される、警告のコアセットの詳細については、「[コード分析の警告](https://go.microsoft.com/fwlink/p/?linkid=226853)」を参照してください。

通常、コード分析の警告を解決するには、必要に応じてソースコードを更新するか、関数コントラクトを明確にする注釈を追加する必要があります。 注釈を追加すると、analyzer は、今後のすべての呼び出し元にコントラクトを適用できるようになり、読みやすさも向上します。

**コード分析の結果**に特定のエラーが表示された場合は、慎重に検証した後に、注釈を使用しても、これらの警告を除外するか抑制するかを選択できます。 詳細については、「[ドライバーのコード分析を実行する方法](how-to-run-code-analysis-for-drivers.md)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ドライバーのコード分析を実行する方法](how-to-run-code-analysis-for-drivers.md)

[Visual Studio のコード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)

[ドライバーの警告のコード分析](prefast-for-drivers-warnings.md)

[コード分析の警告](https://go.microsoft.com/fwlink/p/?linkid=226853)

[Windows ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)

 

 






