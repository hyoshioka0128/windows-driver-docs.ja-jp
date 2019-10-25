---
title: 静的ドライバー検証ツールのレポートの使用
description: 静的ドライバー検証ツールのレポートの使用
ms.assetid: ca6eaa53-cee5-4caf-b1e1-035ea800779b
keywords:
- 静的ドライバー検証ツール WDK、検証結果
- StaticDV WDK、検証結果
- SDV WDK、検証結果
- 静的ドライバー検証ツール WDK、エラーの特定
- StaticDV WDK、エラーの特定
- SDV WDK、エラーの特定
- エラーの検出 WDK 静的ドライバー検証ツール
- エラー WDK 静的ドライバーの検証ツール
- 障害ビューアー WDK 静的ドライバー検証ツール
- ABORT ルーチン
- WDK 静的ドライバーの検証のトレース
- 規則 WDK 静的ドライバー検証ツール
- ペイン WDK 静的ドライバー検証ツール
- 静的ドライバー検証ツールレポート WDK、ペイン
- 静的ドライバ検証ツールレポート WDK、静的ドライバ検証ツールについて
- 静的ドライバー検証ツール WDK、静的ドライバー検証ツールレポート
- StaticDV WDK、静的ドライバー検証ツールレポート
- SDV WDK、静的ドライバーの検証ツールレポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c4e9b6ac920c67fbd5705016779a2d75d51ff1d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839991"
---
# <a name="using-the-static-driver-verifier-report"></a>静的ドライバー検証ツールのレポートの使用


SDV レポートは、検証結果を対話形式で表示します。 このセクションでは、SDV レポートを使用して、ドライバーのコードエラーを見つける方法について説明します。 レポート、ウィンドウの機能、およびウィンドウの要素の詳細については、「 [Static Driver Verifier report](static-driver-verifier-report.md)」を参照してください。

### <a name="span-idopen_the_static_driver_verifier_defect_viewerspanspan-idopen_the_static_driver_verifier_defect_viewerspanopen-the-static-driver-verifier-defect-viewer"></a><span id="open_the_static_driver_verifier_defect_viewer"></span><span id="OPEN_THE_STATIC_DRIVER_VERIFIER_DEFECT_VIEWER"></span>静的ドライバー検証ツールの障害ビューアーを開く

SDV が**結果**ウィンドウで "欠陥" (規則違反) を報告した場合は、静的ドライバー検証ツールレポートの [[欠陥ビューアー](defect-viewer.md) ] ウィンドウで違反に関連するコードを確認できます。 [欠陥ビューアー] ウィンドウには、規則違反のパスのコードが表示されます。 違反したルールごとに1つの**欠陥ビューアー**ウィンドウがあります (一度に表示できるのは、1つの**欠陥ビューアー**ウィンドウのみです)。

欠陥の [欠陥ビューアー] ウィンドウを開くには、次のようにします。

-   **結果**ウィンドウで、 **[欠陥]** ノード (白い x 印が付いた赤い円のアイコン![](images/sdv-ico-defect.png)) の下の一覧からルールを選択し、ルール名をダブルクリックします。

この手順は、欠陥に対してのみ機能します。 検証の結果に欠陥がない場合 (パス、タイムアウト、スペース不足、適用できない、その他の欠陥以外の結果など)、SDV では**欠陥ビューアー**ウィンドウが生成されません。

次のスクリーンショットは、静的なドライバーの検証ツールレポートページを示しています。

![静的ドライバーの検証ツールレポートページのスクリーンショット](images/sdv-defectviewer.png)

### <a name="span-idreview_the_rulespanspan-idreview_the_rulespanreview-the-rule"></a><span id="review_the_rule"></span><span id="REVIEW_THE_RULE"></span>ルールを確認する

コードで規則違反を検出する前に、ドライバーが違反している規則について理解しておいてください。

「[静的ドライバーの検証規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」セクションには、各規則 ( [cancelspinlock ロック](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-cancelspinlock)など) について説明するトピックが含まれています。

ルールのコードを表示するには、静的なドライバーの検証ツールレポートの**ソースコード**ペインで、ルールコードを含むタブをクリックします。

たとえば、ドライバーが[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))または[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を順不同で呼び出す場合、またはドライバーがスピンロックを解除する前にルーチンを終了する場合、 **cancelspinlock ロック**規則に違反します。

### <a name="span-idtrace_the_defect_pathspanspan-idtrace_the_defect_pathspantrace-the-defect-path"></a><span id="trace_the_defect_path"></span><span id="TRACE_THE_DEFECT_PATH"></span>欠陥のパスをトレースする

**[欠陥ビューアー]** ウィンドウが開いたら、 **[トレースツリー]** ウィンドウで、[欠陥] パスにある最初の重要なドライバーの呼び出しを表す要素が選択されます。 **ソース**コードペインで、関連付けられているソースコード行が青色で強調表示されます。

次のスクリーンショットは、Fail\_Driver1 サンプルドライバーによって[Cancelspinlock ロック](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-cancelspinlock)規則に違反している場合に、 **[静的なドライバー検証ツール]** ウィンドウの開始ビューを示しています。 この例では、CancelSpinLock ロック規則の違反へのパスでの最初のドライバー呼び出しは、ドライバーの**DispatchSystemControl**ルーチンでの[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))の呼び出しです。

![cancelspinlock ロック規則に違反する場合の [静的ドライバー検証ツール] ウィンドウの開始ビューのスクリーンショット](images/sdv-tracetree.png)

### <a name="span-iduse_the_source_code_panespanspan-iduse_the_source_code_panespanuse-the-source-code-pane"></a><span id="use_the_source_code_pane"></span><span id="USE_THE_SOURCE_CODE_PANE"></span>ソースコードペインを使用する

[ソースコードペイン](source-code-pane.md)に、検証で使用されるソースファイルが表示されます。 **[トレースツリー]** ペインの要素を選択すると、その要素に関連付けられているソースコードファイルが、隣接する**ソースコード**ペインのファイルスタックの一番上に表示されます。 別のソースファイルを表示するには、ソース**コード**ペインでソースファイルのタブをクリックします。

次のスクリーンショットは、ソースコードペインを示しています。 この**ソースコード**ペインでは、ペール blue で強調表示されているコード行が、 **[トレースツリー]** ペインで選択されている要素に関連付けられています。

![ソースコードペインのスクリーンショット](images/sdv-sourcecode.png)

欠陥のパスで実行されるドライバーコード内の行は、赤いテキストで表示されます。 この例の行116や118など、赤いテキストの行だけを調べると、不具合が発生することがあります。特に、この例で使用されているような単純な欠陥です。 この場合、ドライバーはスピンロックを取得し、スピンロックを解放せずにディスパッチルーチンからを返します。

### <a name="span-idstep_through_the_tracespanspan-idstep_through_the_tracespanstep-through-the-trace"></a><span id="step_through_the_trace"></span><span id="STEP_THROUGH_THE_TRACE"></span>トレースのステップ実行

トレースを開始するには、 **[トレースツリー]** ペインで要素を選択し、下方向キーを押します。 下方向キーを押すたびに、 **[トレースツリー]** ペインの次の要素が選択されます。

**[トレースツリー]** ウィンドウで要素をステップ実行するときに、ドライバーコードの要素の**ソースコード**ペインを見てください。 折りたたまれたコードセクションを展開するには、右矢印キーを押します。 コードの展開されたセクションを折りたたむには、左矢印キーを押します。 カーソルは、コードの折りたたまれたセクションをすべてスキップします。

**トレースツリー**ペインの要素を下にスクロールすると、選択した要素のソースコードファイルが**ソースコード**ペイン内のファイルのスタックの一番上に移動し、関連するコード行が強調表示されます。

次のスクリーンショットは、トレースツリーとソースコードのウィンドウが表示された静的ドライバー検証ツールの欠陥ビューアーを示しています。

![静的ドライバーの検証ツールレポートページのスクリーンショット](images/sdv-trace1.png)

### <a name="span-iduse_the_rule_file_and_state_panespanspan-iduse_the_rule_file_and_state_panespanuse-the-rule-file-and-state-pane"></a><span id="use_the_rule_file_and_state_pane"></span><span id="USE_THE_RULE_FILE_AND_STATE_PANE"></span>[規則ファイルと状態] ウィンドウを使用する

[[状態] ペイン](state-pane.md)を使用すると、検証中に sdv が追跡する変数の値を表すブール式のセットを表示できます。

**[状態]** ペインに表示されるブール式は、そのセット内で**TRUE**に評価される式です。 トレースツリーペインの要素によっていずれかの式の値が変更された場合、 **[状態]** ペインの内容は、 **TRUE**に評価される式の新しいセットを表示するように変更されます。

**[トレースツリー]** ペインをステップ実行すると、sdv がこれらの変数の値を使用して、ルールファイル (\*) で使用されている式を評価する方法を確認できます。

静的ドライバーの検証ツールレポートページの次のスクリーンショットでは、SDV テストで、ドライバーが以前にスピンロックを取得したかどうかを示しています。 SDV は、ドライバーが以前にスピンロックを取得したかどうかをテストします。つまり、 **s**変数の値が**1**である場合は、ロックされていることを意味します。 この場合、[[状態] ウィンドウ](state-pane.md)に表示される**s! = 1** (ロック解除) であるため、sdv は**の値を** **1**に設定し、ロックが取得されることを示します。

![ドライバーが以前にスピンロックを取得したかどうかを sdv テストで確認する方法を示す静的ドライバー検証ツールレポートページのスクリーンショット](images/sdv-trace2.png)

### <a name="span-idfind_the_abort_routinespanspan-idfind_the_abort_routinespanfind-the-abort-routine"></a><span id="find_the_abort_routine"></span><span id="FIND_THE_ABORT_ROUTINE"></span>ABORT ルーチンを検索する

ドライバーコードがルールに違反している場合、 **[トレースツリー]** ウィンドウには、その欠陥を報告するための**ABORT**ルーチンが含まれています。

欠陥へのコードパスが長く複雑な場合は、 **ABORT**ルーチンが見つかるまで**トレースツリー**ペインを下にスクロールすると便利です。その後、上方向キーを使用して、欠陥レポートをすぐにトリガーしたコードを見つけます。

たとえば、次のスクリーンショットに示すように、ABORT ルーチンは、ロックが取得されたかどうかをテストした後に欠陥を報告する CancelSpinLock ロックの行に関連付けられています (**s = = ロック**済み)。 このテストは、ディスパッチルーチンが終了したときに実行されるサブルーチンの一部です。 この情報から、ドライバーがディスパッチルーチンから戻る前にスピンロックを解除できなかったことを推測できます。

![abort ルーチンが cancelspinlock ロックファイルの行に関連付けられていることを示す静的ドライバー検証ツールレポートページのスクリーンショット](images/sdv-trace3.png)

### <a name="span-idclose_the_static_driver_verifier_defect_viewerspanspan-idclose_the_static_driver_verifier_defect_viewerspanclose-the-static-driver-verifier-defect-viewer"></a><span id="close_the_static_driver_verifier_defect_viewer"></span><span id="CLOSE_THE_STATIC_DRIVER_VERIFIER_DEFECT_VIEWER"></span>静的ドライバー検証ツールの欠陥ビューアーを閉じる

障害の原因となったコードエラーを特定した後、現在のルールに対して **[静的ドライバー検証ツールの欠陥のビューアー]** ウィンドウを閉じて、別のルールの **[欠陥ビューアー]** を開くことができます。

ルールの欠陥ビューアーを閉じるには、次のようにします。

-   **[ファイル]** メニューの **[終了]** をクリックします。

また、 **[問題ビューアー]** の **[閉じる]** ボタン (**X**) をクリックすることもできます。 静的ドライバーの検証ツールレポートの **[閉じる]** ボタン (**X**) のすぐ下にあります。

次のスクリーンショットは、欠陥表示モジュールを閉じる方法を示しています。

![ルールの欠陥ビューアーを閉じる方法を示すスクリーンショット](images/sdv-defectviewerclose.png)

 

 





