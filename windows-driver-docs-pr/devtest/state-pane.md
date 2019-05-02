---
title: State (状態) ウィンドウ
description: State (状態) ウィンドウ
ms.assetid: 20fb016e-249b-4d28-9fa8-5d2dd837109f
keywords:
- WDK Static Driver Verifier のペイン
- Static Driver Verifier レポート WDK の状態 ウィンドウ
- 状態ウィンドウ WDK Static Driver Verifier
- WDK Static Driver Verifier のブール式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd6c43db50fb4a9a3c568fc4babcfaf9a021f260
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343956"
---
# <a name="state-pane"></a>State (状態) ウィンドウ


**状態**ペインには、ドライバー、オペレーティング システムのモデル、およびルールで変数の値のブール式が表示されます。 SDV は、これらの式を使用して、ドライバー、オペレーティング システムのモデルと、ルールの抽象化を作成しの検証に使用します。

次のスクリーン ショットは例を示しています。**状態**欠陥ビューアー ペイン。

![欠陥のビューアーでの状態 ウィンドウのスクリーン ショット](images/sdv-state.png)

**状態**ウィンドウは、欠陥ビューアー コンポーネントです。 コード要素が強調表示されている場合、[トレース ツリー ウィンドウ](trace-tree-pane.md)でソース コードの対応する行が強調表示し、[ソース コード ウィンドウ](source-code-pane.md)、**状態**ペインが表示されます評価されるブール式 (ドライバーの SDV を追跡する式のセット) から**TRUE**コードの行が実行される前にします。

### <a name="span-idtrackingbooleanexpressionsspanspan-idtrackingbooleanexpressionsspantracking-boolean-expressions"></a><span id="tracking_boolean_expressions"></span><span id="TRACKING_BOOLEAN_EXPRESSIONS"></span>ブール式の追跡

ドライバーの各ルールを確認するには、中には、SDV は、一連のブール式を追跡します。 表示されるブール式、**状態**ウィンドウはそのセットに評価される式**TRUE**します。 場合内の要素、**トレース ツリー**ウィンドウの内容、任意の式の値を変更する、**状態**に評価される式の新しいセットを表示するウィンドウ変更**TRUE**.

### <a name="span-idinterpretingexpressionsinthestatepanespanspan-idinterpretingexpressionsinthestatepanespaninterpreting-expressions-in-the-state-pane"></a><span id="interpreting_expressions_in_the_state_pane"></span><span id="INTERPRETING_EXPRESSIONS_IN_THE_STATE_PANE"></span>状態のウィンドウで式の解釈

ほとんどの式に表示される、**状態**ルール コードでは変数に関連するウィンドウ。 規則のソース コードを使用することができます (で、 *RuleName*.slic ファイルで、**ソース コード**ウィンドウ)、式を解釈するのに役立ちます。

ただし、一部の式の表示、**状態**の内部表現に変換するために役立つ可能性がある詳細ウィンドウ。 以下に例を示します。

```
x!=x
```

SDV は、この式を表しますを条件変数の値*x*この時点で、トレースでは、トレース内の別の時点で同じ変数の値と同じです。 ドライバーのソース コード、規則コードを使用 (\*.slic)、および内の要素、**トレース ツリー**ウィンドウで、式を解釈するのに役立ちます。

### <a name="span-idsteptabsinthestatepanespanspan-idsteptabsinthestatepanespanstep-tabs-in-the-state-pane"></a><span id="step_tabs_in_the_state_pane"></span><span id="STEP_TABS_IN_THE_STATE_PANE"></span>状態ウィンドウ内の手順のタブ

内のブール式、**状態**ウィンドウがタブに表示されます。 各タブは、すべての検証で使用するソース コードをトレースにステップを表します。 [ステップ] タブでは、トレースには、そのステップの順序を表します。

通常、ソース コードの各行は、トレース内の 1 つのステップを表しているためがありますのみ 1 つのステップ タブで、**状態**ウィンドウ。 ただし、複雑なコードは、多くの手順を生成することができます。

たとえば、次のスクリーン ショットでは、関数ポインターを含むコード行を表示する [状態] ウィンドウが表示されます。 この場合、各ステップ タブは、ポインター、関数に示される、その結果の呼び出し元の解像度で手順を表します。 (手順タブの数が数は、関数ポインターを解決するのには、SDV のステップします。)

![関数ポインターを含むコード行を表示する [状態] ウィンドウのスクリーン ショット](images/sdv-statetab.png)

手順の各タブに表示する、**状態**順番では、ウィンドウ内のコードの関連付けられている行を選択する、**ソース コード**ウィンドウ。 内のコード行をクリックし、**ソース コード**ウィンドウ繰り返し。 選択した行のコードをクリックするたびにすべてのステップ タブ循環がまで、SDV に次の手順のタブが表示されます。 曲線の黄色の矢印 (![曲線の黄色の矢印アイコンが選択されている手順を示す](images/sdv-ico-steptab.png)) 選択されている手順を示します。 任意のタブをクリックすることも、**状態**そのコンテンツを表示するウィンドウ。

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>コメント

SDV は、内の式を多くの場合、追跡、**状態**ウィンドウで、ルールには表示されませんし、直接関連するルールは表示されません。 これらの式は、SDV を別の値と別の規則違反を関連付けるために、試行に使用する高度なヒューリスティックの結果としてください。 場合によっては、SDV は正しく式を評価できません。 このような場合は、SDV は、現在の状態が不明ですし、最後の既知の状態と手順の式を表示することを示すメッセージを提供します。 詳細については、次のコード例を参照します。

```
Unknown state. Last known state from step 120.
sdv irql current ==2
sdv irql current!=1
sdv irql current!=0
```

 

 





