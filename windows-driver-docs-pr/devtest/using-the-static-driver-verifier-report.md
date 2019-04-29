---
title: 静的ドライバー検証ツールのレポートの使用
description: 静的ドライバー検証ツールのレポートの使用
ms.assetid: ca6eaa53-cee5-4caf-b1e1-035ea800779b
keywords:
- 静的ドライバー検証ツールの WDK、検証結果
- StaticDV WDK、検証結果
- SDV の WDK、検証結果
- 静的ドライバー検証ツールの WDK、エラーの検索
- StaticDV WDK、エラーの検索
- SDV の WDK、エラーの検索
- エラー WDK Static Driver Verifier の検索
- エラー WDK Static Driver Verifier
- 欠陥ビューアー WDK Static Driver Verifier
- ルーチンを中止します。
- トレース WDK Static Driver Verifier
- WDK Static Driver Verifier の規則
- WDK Static Driver Verifier のペイン
- 静的ドライバー検証レポートの WDK、ペイン
- WDK、static Driver Verifier レポートは、Static Driver Verifier のレポートについて
- Static Driver Verifier WDK、Static Driver Verifier のレポート
- StaticDV WDK、Static Driver Verifier のレポート
- SDV の WDK、Static Driver Verifier のレポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cc0afed9f938254957b4cd9d8c08a83e6102158
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327271"
---
# <a name="using-the-static-driver-verifier-report"></a>静的ドライバー検証ツールのレポートの使用


SDV レポートは、検証結果の対話型の表示です。 このセクションでは、SDV レポートを使用して、ドライバー内でコードのエラーを検索する方法について説明します。 レポートの詳細については、windows、および windows で要素の機能を参照してください[静的ドライバー検証ツールのレポート](static-driver-verifier-report.md)します。

### <a name="span-idopenthestaticdriververifierdefectviewerspanspan-idopenthestaticdriververifierdefectviewerspanopen-the-static-driver-verifier-defect-viewer"></a><span id="open_the_static_driver_verifier_defect_viewer"></span><span id="OPEN_THE_STATIC_DRIVER_VERIFIER_DEFECT_VIEWER"></span>Static Driver Verifier の欠陥ビューアーを開く

SDV で「欠陥」(規則の違反) を報告する場合、**結果**ウィンドウで違反に関連するコードを表示することができます、[欠陥ビューアー](defect-viewer.md)静的ドライバー検証ツールのレポートのウィンドウ。 欠陥ビューアー ウィンドウでは、規則違反へのパスの中に、コードが表示されます。 1 つである**欠陥ビューアー**各ルールに違反していたのウィンドウ (1 つだけを表示することができます**欠陥ビューアー**一度にウィンドウ)。

障害に対するビューアーの参加を解除 ウィンドウを開きます。

-   ルールの下の一覧から選択、 **Defect(s)** ノード (![白い x 欠陥を示す赤い円のアイコン](images/sdv-ico-defect.png)) で、**結果**ウィンドウで、ルールの名前をダブルクリックします。

この手順は、障害の検出のみ有効です。 SDV は生成されません、**ビューアーの参加を解除**パス、タイムアウト、spaceouts、該当なし、またはその他の非参加の解除結果など、検証の結果がない場合は、ウィンドウの障害。

次のスクリーン ショットは、静的ドライバー検証ツールのレポート ページを示しています。

![静的ドライバー検証ツールのレポート ページのスクリーン ショット](images/sdv-defectviewer.png)

### <a name="span-idreviewtherulespanspan-idreviewtherulespanreview-the-rule"></a><span id="review_the_rule"></span><span id="REVIEW_THE_RULE"></span>ルールを確認してください。

検索しようとする前に、コードでは、規則違反は、ドライバーに違反した規則に詳しくなります。

[静的ドライバー検証規則](https://msdn.microsoft.com/library/windows/hardware/ff551714)セクションには、たとえば、各ルールを説明するトピックが含まれています。 [CancelSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff542478)します。

規則のコードを表示する、**ソース コード**静的ドライバー検証ツールのレポートのペインが CancelSpinLock.slic など、ルールのコードを持つタブをクリックします。

たとえば、 **CancelSpinLock**規則に違反する場合は、ドライバーは呼び出し[ **IoAcquireCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548196)または[ **IoReleaseCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549550)順序、またはドライバーが、スピン ロックを解除する前に、ルーチンを終了します。

### <a name="span-idtracethedefectpathspanspan-idtracethedefectpathspantrace-the-defect-path"></a><span id="trace_the_defect_path"></span><span id="TRACE_THE_DEFECT_PATH"></span>欠陥のパスをトレースします。

ときに、**ビューアーの参加を解除**ウィンドウが開き、内の要素、**トレース ツリー**欠陥パスの最初の不可欠なドライバーの呼び出しを表すペインが選択されています。 **ソース コード**ウィンドウで、ソース コードの関連する行が青色で強調表示されます。

次のスクリーン ショットが開いたときのビューを示しています、**静的ドライバー検証ツールの欠陥ビューアー**の違反をウィンドウ、 [CancelSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff542478)ルールによって、失敗\_Driver1 サンプル ドライバー。 この例で CancelSpinLock ルールに違反するパスの最初のドライバー呼び出しがへの呼び出し[ **IoAcquireCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548196)ドライバーの**DispatchSystemControl**ルーチン。

![静的ドライバー検証ツールの開始ビューのスクリーン ショット cancelspinlock 規則違反のビューア ウィンドウの参加を解除します。](images/sdv-tracetree.png)

### <a name="span-idusethesourcecodepanespanspan-idusethesourcecodepanespanuse-the-source-code-pane"></a><span id="use_the_source_code_pane"></span><span id="USE_THE_SOURCE_CODE_PANE"></span>ソース コード ウィンドウを使用します。

[ソース コード ウィンドウ](source-code-pane.md)検証で使用されるソース ファイルが表示されます。 内の要素のときに、**トレース ツリー**ペインが選択されている場合に、隣接するファイルのスタックの上部にある要素に関連付けられているソース コード ファイルが表示されます**ソース コード**ウィンドウ。 異なるソース ファイルを表示するには、内のソース ファイルのタブをクリックして、**ソース コード**ウィンドウ。

次のスクリーン ショットは、ソース コード ウィンドウを示しています。 この**ソース コード**ウィンドウで、薄い青色で強調表示されている行のコードはで選択した要素に関連付けられているもの、**トレース ツリー**ウィンドウ。

![ソース コード ウィンドウのスクリーン ショット](images/sdv-sourcecode.png)

赤いテキストでは、障害へのパスで実行されるドライバー コードの行が表示されます。 116 と、この例では 118 行などの赤いテキストの行のみを調べることで、障害では、この例で使用されるよう特に単純な欠陥を場合があります参照してくださいことができます。 この場合、ドライバーは、スピン ロックをスピン ロックを解放しないままディスパッチ ルーチンから返します。

### <a name="span-idstepthroughthetracespanspan-idstepthroughthetracespanstep-through-the-trace"></a><span id="step_through_the_trace"></span><span id="STEP_THROUGH_THE_TRACE"></span>トレースをステップ

トレースを開始するには、内の要素を選択、**トレース ツリー**ペイン、および下方向キーを押します。 下方向の次の要素をクリックするたびに、**トレース ツリー**ペインが選択されています。

内の要素をステップ実行すると、**トレース ツリー**  ウィンドウで、ウォッチ、**ソース コード**ドライバー コードからの要素のウィンドウ。 コードの折りたたまれたセクションを展開するには、右矢印キーを押します。 展開したコードのセクションを折りたたむには、左矢印キーを押します。 カーソルは、コードの折りたたまれているすべてのセクションをスキップします。

内の要素を下へスクロールすると、**トレース ツリー**  ウィンドウで、ソース コード ファイルを選択した要素の発生元のファイルのスタックの一番上に移動、**ソース コード**ウィンドウと関連付けられています。コード行を強調表示されます。

次のスクリーン ショットは、トレースのツリーおよびソース コードのウィンドウを持つ静的ドライバー検証ツール欠陥ビューアーを示しています。

![静的ドライバー検証ツールのレポート ページのスクリーン ショット](images/sdv-trace1.png)

### <a name="span-idusetherulefileandstatepanespanspan-idusetherulefileandstatepanespanuse-the-rule-file-and-state-pane"></a><span id="use_the_rule_file_and_state_pane"></span><span id="USE_THE_RULE_FILE_AND_STATE_PANE"></span>規則ファイルと状態のウィンドウを使用して、

使用することができます、[状態ウィンドウ](state-pane.md)SDV を検証中に追跡する変数の値を表すブール式のセットを表示します。

表示されるブール式、**状態**ウィンドウはそのセットに評価される式**TRUE**します。 トレースのツリー ウィンドウで要素のコンテンツ、任意の式の値が変更された場合、**状態**に評価される式の新しいセットを表示するウィンドウ変更**TRUE**します。

ステップ実行、**トレース ツリー**ウィンドウで、SDV でこれらの変数の値を使用して、ルール ファイルで使用される式を評価する方法を確認できます (\*.slic)。

かどうか、ドライバーが、スピン ロックを取得した以前に SDV のテストが示すため、静的ドライバー検証ツールのレポート ページに示す次のスクリーン ショット。 SDV テストするかどうか、ドライバーが前に取得した、スピン ロックを参照する場合の値、 **s**変数は**1**意味がロックされています。 この場合、 **s! = 1** (、ロックを解除) に表示される、[状態ウィンドウ](state-pane.md)SDV の値を設定するため、 **s**に**1**ロックがあることを示す取得されます。

![sdv をテストする方法を示す静的ドライバー検証ツールのレポート ページのスクリーン ショットを示すかどうかは、ドライバーが、スピン ロックを取得した以前](images/sdv-trace2.png)

### <a name="span-idfindtheabortroutinespanspan-idfindtheabortroutinespanfind-the-abort-routine"></a><span id="find_the_abort_routine"></span><span id="FIND_THE_ABORT_ROUTINE"></span>中止ルーチンを検索します。

ドライバー コードには、ルールに違反しているときに、**トレース ツリー**ペインには、**中止**不具合の報告の日常的な。

下にスクロールすると便利ですが多くの場合、長くて複雑な問題へのコード パスがある場合、**トレース ツリー**ウィンドウが表示されるまで、**中止**ルーチンとし、コードを検索するには、そのほとんどを上方向キーを使用してすぐに障害レポートがトリガーされます。

たとえば、次のスクリーン ショットに示すように、中止ルーチンに関連付けられているロックが取得されたかどうかをテストした後、障害を報告する CancelSpinLock.slic ファイルの行を (**s = = ロック**)。 テストは、ディスパッチ ルーチンの終了時に実行されるサブルーチンの一部です。 この情報からディスパッチ ルーチンから戻る前に、スピン ロックを解放するドライバーが失敗したことを推測できます。

![中止ルーチンが cancelspinlock.slic ファイルからの行を関連付ける方法を示しています。 静的ドライバー検証ツールのレポート ページのスクリーン ショット](images/sdv-trace3.png)

### <a name="span-idclosethestaticdriververifierdefectviewerspanspan-idclosethestaticdriververifierdefectviewerspanclose-the-static-driver-verifier-defect-viewer"></a><span id="close_the_static_driver_verifier_defect_viewer"></span><span id="CLOSE_THE_STATIC_DRIVER_VERIFIER_DEFECT_VIEWER"></span>Static Driver Verifier の欠陥のビューアーを閉じます

閉じることができます、障害の原因となったコードのエラーを特定した後、**静的ドライバー検証ツールの参加を解除ビューアー**ウィンドウを開くと、現在のルールを**ビューアーの参加を解除**のさまざまなルール。

ルールの欠陥ビューアーを閉じます。

-   **ファイル**メニューの **終了**します。

クリックすることも、**閉じる**ボタン (**X**) の**欠陥ビューアー**します。 すぐ下にある、**閉じる**ボタン (**X**) 静的ドライバー検証レポートのためです。

次のスクリーン ショットでは、欠陥のビューアーを終了する方法を示します。

![ルールの欠陥のビューアーを終了する方法を示すスクリーン ショット](images/sdv-defectviewerclose.png)

 

 





