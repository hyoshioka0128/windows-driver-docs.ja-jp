---
title: ドライバーのコード分析の概要
description: Windows ドライバー キットは、Microsoft Visual Studio Ultimate 2012 でコード分析ツールにドライバー固有の拡張機能を提供します。
ms.assetid: 2A780608-F386-4838-A4EB-022C2F0EED3B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b775f9e6a8d7ae59dfe91045577b4016bee7ae8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371619"
---
# <a name="code-analysis-for-drivers-overview"></a>ドライバーのコード分析の概要


Windows Driver Kit にドライバー固有の拡張機能を提供する、[コード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)Microsoft Visual Studio でします。 Code Analysis for Drivers は、特にカーネル モード ドライバーをドライバーにのみ適用される規則が含まれています。 コード Analysis for Drivers は、コードをコンパイルするとすぐに、コードで潜在的なエラーを検出できます。

## <a name="span-idhowthecodeanalysistoolworksspanspan-idhowthecodeanalysistoolworksspanspan-idhowthecodeanalysistoolworksspanhow-the-code-analysis-tool-works"></a><span id="How_the_Code_Analysis_tool_works"></span><span id="how_the_code_analysis_tool_works"></span><span id="HOW_THE_CODE_ANALYSIS_TOOL_WORKS"></span>コード分析ツールのしくみ


コード分析ツールでは、標準のコンパイラでは、Cl.exe のビルド ユーティリティの呼び出しをインターセプトし、代わりに、ドライバーのソース コードを分析し、エラーと警告メッセージのログ ファイルを作成する CL 切片コンパイラを実行します。 コード分析ツールを実行するには、単独でまたはドライバーをビルドするときに実行するコード分析ツールを構成することができます。 単独でコード分析ツールを実行すると (**分析&gt;ソリューションでコード分析を実行**) コード分析のレポート ウィンドウで、結果が表示されます。 ビルドの一部としてコード分析ツールを実行して、CL 切片コンパイラ エラーと警告メッセージのログ ファイルが作成ビルド出力を生成する Cl.exe の standard バージョンを呼び出しています。 生成されるオブジェクト ファイルは、標準によって生成されたそれらのビルド コマンドと同じです。

インターセプト コンパイラを実行すると Code Analysis for Drivers は、コード内の各関数を個別に調べし、一般的なドライバーのエラーと不適切なコーディング手法を探して、コードでは、すべての可能なパスの実行をシミュレートします。 コード分析ツールは大規模なドライバーは、上であっても比較的高速に実行され、正確に生成されるレポートは、疑わしいエラー ドライバー コードの行を識別します。

## <a name="span-idthetypesoferrorscodeanalysiscandetectspanspan-idthetypesoferrorscodeanalysiscandetectspanspan-idthetypesoferrorscodeanalysiscandetectspanthe-types-of-errors-code-analysis-can-detect"></a><span id="The_types_of_errors_Code_Analysis_can_detect"></span><span id="the_types_of_errors_code_analysis_can_detect"></span><span id="THE_TYPES_OF_ERRORS_CODE_ANALYSIS_CAN_DETECT"></span>コード分析で検出できるエラーの種類


コード分析は、次のカテゴリのエラーを含む、エラーのいくつかの種類を検出できます。

-   **メモリ:** 逆参照、メモリ リークの可能性**NULL**初期化されていないメモリ、カーネル モードのスタックの過剰な使用、およびプール タグの不適切な使用へのポインター、アクセスします。

-   **リソース:** など、いくつかの関数を呼び出すときに保持するリソースとその他の関数を呼び出すときに持ってはならないリソースのリソースの解放に失敗します。

-   **関数を使用します。** 特定の関数の不適切な可能性のある使用は、関数に引数が正しくない、可能な引数が厳密に型を特定の古い機能の考えられる用途をチェックしない関数の不一致を入力しで関数が呼び出す、可能性があります無効な IRQL します。

-   **浮動小数点状態:** ドライバーと、さまざまな IRQL で保存した後、浮動小数点状態を復元しようとしています。 浮動小数点演算ハードウェアの状態の保護に失敗しました。

-   **優先順位の規則:** C 言語のプログラミングの優先順位の規則のためのもの、プログラマとして動作しないコードです。

-   **カーネル モードのコーディング プラクティス:** 不透明なメモリ記述子のリスト (MDL) 構造の変更によって呼び出された関数では、一連の変数の値を確認に失敗する、安全な文字列関数ではなく、C と C++ の文字列操作関数を使用してなどのエラーを引き起こす可能性のあるコーディングのプラクティスNtstrsafe.h で定義されます。

-   **ドライバー固有のコーディング プラクティス:** 多くの場合、カーネル モード ドライバーでエラーの原因を特定の操作。 たとえば、メンバーを変更してで引数をコピーする代わりに引数を文字列または構造体を指すポインターを保存せず全体の I/O 要求パケット (IRP) をコピー、 [ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。

## <a name="span-idcodeanalysiswarningsspanspan-idcodeanalysiswarningsspanspan-idcodeanalysiswarningsspancode-analysis-warnings"></a><span id="Code_Analysis_warnings"></span><span id="code_analysis_warnings"></span><span id="CODE_ANALYSIS_WARNINGS"></span>コード分析の警告


コード分析ツールは、プログラムまたはドライバーのコード内のエラーを識別するために、ルールに基づくモデルを使用します。 各ルールは、コード分析ツール規則の違反を検出した場合に報告される警告に関連付けられます。 ドライバー固有の警告の詳細については、次を参照してください。 [Code Analysis for Drivers 警告](prefast-for-drivers-warnings.md)します。 Visual Studio でコード分析ツールをレポートする警告のコア セットについては、次を参照してください。[コード分析の警告](https://go.microsoft.com/fwlink/p/?linkid=226853)します。

## <a name="span-idannotationsspanspan-idannotationsspanspan-idannotationsspanannotations"></a><span id="Annotations"></span><span id="annotations"></span><span id="ANNOTATIONS"></span>注釈


コード分析ツールを提供する重要な機能の 1 つは、関数の説明と、ドライバーのソース コード内の他のエンティティの注釈を設定する機能です。 コード分析ツールには、機能内のスコープつまり、関数間の相互作用を分析します。 注釈のでは、呼び出されると、呼び出し元関数の間のコントラクトのより完全な式を提供するコード分析ツールは、コントラクトが満たされているをチェックできるようにします。 注釈の別の目的は、関数の使用方法のコードを読み取るすべてのユーザーに通知を予想される結果です。 注釈は、インターフェイスのコントラクトを宣言し、そのコントラクトを実現する方法について説明しようとはしないでください。 多くの場合、コード分析ツールを実行してから結果がない場合、適切な注釈を反映して、注釈を追加することで注釈がに関する警告を抑制すると追加のチェックが有効になっています。 詳細については、次を参照してください。 [Windows ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)します。 詳細については、SAL 2.0 についてを参照してください[C と C++ コードの欠陥を削減する SAL 注釈を使って](https://go.microsoft.com/fwlink/p/?linkid=247283)します。 SAL 2.0 には、SAL 1.0 が置き換えられます。 WDK for Windows 8 では、SAL 2.0 を使用する必要があります。 ドライバーの SAL 1.0 についての情報を必要がある場合は、Windows 7 の WDK に同梱されているドライバーの注釈のドキュメントの PREfast を参照してください。

## <a name="span-idinterpretingtheresultspanspan-idinterpretingtheresultspanspan-idinterpretingtheresultspaninterpreting-the-result"></a><span id="Interpreting_the_result"></span><span id="interpreting_the_result"></span><span id="INTERPRETING_THE_RESULT"></span>結果の解釈


ドライバーのコード分析が簡単に実行できると非常に大きなドライバーとプログラムでも、迅速に実行されます。 開発者の作業では、出力を調べる、コード分析ツールが検出されると、エラーを分析およびコード分析ツールが誤って解釈される有効なコードから実際のコーディング エラーを区別します。

コード分析ツールが検出される警告をすべてを説明する包括的なリファレンスを参照してください[Code Analysis for Drivers 警告](prefast-for-drivers-warnings.md)します。 Visual Studio でコード分析ツールをレポートする警告のコア セットについては、次を参照してください。[コード分析の警告](https://go.microsoft.com/fwlink/p/?linkid=226853)します。

警告は、通常のコード分析を解決するには、必要に応じて、ソース コードを更新または関数のコントラクトを明確にするための注釈を追加する必要があります。 将来のすべての呼び出し元のコントラクトを強制するアナライザーは、注釈を追加し、読みやすさも向上します。

場合、**コード分析結果**、慎重に調査した後、ユーザーが決定した表示エラーが有効でないし、注釈を使用しても回避することはできません、除外するか、これらの警告を抑制することもできます。 詳細については、次を参照してください。[ドライバーのコード分析を実行する方法](how-to-run-code-analysis-for-drivers.md)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ドライバーのコード分析を実行する方法](how-to-run-code-analysis-for-drivers.md)

[Visual Studio でコード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)

[Code Analysis for Drivers の警告](prefast-for-drivers-warnings.md)

[コード分析の警告](https://go.microsoft.com/fwlink/p/?linkid=226853)

[Windows ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)

 

 






