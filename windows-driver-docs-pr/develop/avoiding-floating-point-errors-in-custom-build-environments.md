---
ms.assetid: 47AC8BD7-7098-43C3-A198-3622D465B142
title: カスタム ビルド環境での浮動小数点エラーの回避
description: この情報は、Windows 用のカーネル モード ドライバーをコンパイルする開発者とビルド エンジニア向けです。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c2f017367c211eb8020ea8ee3f29d29509467ee
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "63359487"
---
# <a name="avoiding-floating-point-errors-in-custom-build-environments"></a>カスタム ビルド環境での浮動小数点エラーの回避

この情報は、Windows 用のカーネル モード ドライバーをコンパイルする開発者とビルド エンジニア向けです。 Microsoft Visual Studio Professional 2012 では、Visual C++ (VC++) コンパイラの既定のアーキテクチャが IA32 からストリーム SIMD 拡張機能 2 (SSE2) 命令セットに変更されました。 この変更のために、実行時にバイナリに組み込まれた SSE2 浮動小数点 (FP) 命令は、対処されていない場合、浮動小数点エラーを生成することがあります。 この問題が発生する可能性があるのは、Microsoft VC++ コンパイラを使うか、Windows ドライバーの開発にカスタム ビルド環境を使う場合です。 Microsoft Visual Studio 開発環境を使うか、ドライバーのビルドに、変更していないツールセットで MSbuild ユーティリティを使う場合、問題は発生しません。

## <a name="span-idfloating_point_errors_can_cause_data_corruption_or_computer_crashes_spanspan-idfloating_point_errors_can_cause_data_corruption_or_computer_crashes_spanspan-idfloating_point_errors_can_cause_data_corruption_or_computer_crashes_spanfloating-point-errors-can-cause-data-corruption-or-computer-crashes"></a><span id="Floating_point_errors_can_cause_data_corruption_or_computer_crashes_"></span><span id="floating_point_errors_can_cause_data_corruption_or_computer_crashes_"></span><span id="FLOATING_POINT_ERRORS_CAN_CAUSE_DATA_CORRUPTION_OR_COMPUTER_CRASHES_"></span>浮動小数点エラーによりデータの破損やコンピューターのクラッシュが発生する可能性がある


WDK、Visual Studio、Windows ドライバー用に推奨されるプラットフォーム ツールセット (**WindowsKernelModeDriver8.0**) を*使わずに*ドライバーをコンパイルした場合、エラーなしでコンパイルできたとしても、小数点操作を適切に管理できない場合があります。

**/arch:sse2** コンパイラ オプションを設定すると、Visual Studio Professional 2012 VC++ コンパイラでは、SSE2 命令セットを使うコードが作成されます。 Visual Studio Professional 2012 以降では、これが x86 VC++ コンパイラ コード生成の既定のオプションになっています。 具体的には、既定値は **/arch:ia32** から **/arch:sse2** に変更されます。

アプリケーションにとっては、この変更により、生成されるコードのパフォーマンスが向上し、実行時に使うプロセッサ時間が少なくなります。 ただし、カーネル モード ドライバーにとっては、この変更によって浮動小数点 (FP) 状態が適切に管理できなくなります。 原因は、VC++ コンパイラが FP 命令シーケンスをコンテキストが保存されていない場所に組み込むことです。 どのバイナリ浮動小数点システムも、正確な形式で表現できるのは有限個の浮動小数点値だけであり、他は近似値になります。 丸めモード、精度などの浮動小数点制御状態によって、FP 演算は互いに同期を保たれています。 状態が定義されていないと、FP 計算エラーが発生します。 このような計算エラーは、多くの場合、アプリケーションの状態の破損が唯一の兆候であるため、検出が困難です。 この破損の症状は、ランダムなクラッシュからデータ破損まで、さまざまな形態で現れます。

## <a name="span-idsolutionspanspan-idsolutionspanspan-idsolutionspansolution"></a><span id="Solution"></span><span id="solution"></span><span id="SOLUTION"></span>解決方法


浮動小数点計算のこの問題を回避するには、C++ コンパイラとリンカーのコマンド ラインに **/kernel** フラグを追加し、SSE2 命令が生成されないようにします。 **/kernel** フラグは、既定値の **/arch:sse2** から **/arch:ia32** に変更されます。

また、WDK と Visual Studio Professional 2012 開発環境を使用して、または Visual Studio のコマンド プロンプト ウィンドウで MSBuild を使用して、ドライバーをビルドする場合は、Microsoft 提供のプラットフォーム ツールセット (**WindowsKernelModeDriver8.0**) によって **/kernel** フラグが設定されます。 そのため、浮動小数点生成エラーが回避されます。

```cpp
msbuild myProject.vcxproj /p:PlatformToolset=WindowsKernelModeDriver8.0
```

## <a name="span-idrecommendationsspanspan-idrecommendationsspanspan-idrecommendationsspanrecommendations"></a><span id="Recommendations"></span><span id="recommendations"></span><span id="RECOMMENDATIONS"></span>推奨事項


使用する開発環境の種類に基づいてお勧めするソリューションは、次のとおりです。

-   **Microsoft ツールセット (MSBuild)** - 対処は不要です。 **WindowsKernelModeDriver8.0** をプラットフォーム ツールセットとして使うと、 **/kernel** が必要に応じて自動的に追加されます。
-   **Microsoft VC++ コンパイラ** - **/kernel** フラグを追加し、コンパイラが SSE2 を作成しないようにします。
-   **カスタム ツール/非 Microsoft コンパイラ** - 生成されたバイナリ内で使われているアセンブリ命令に手動で対処する必要があります。

 

 





