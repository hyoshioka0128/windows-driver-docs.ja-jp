---
title: インジケーター テスト
description: このトピックでは、一般的なインジケーターの手順と例について説明します。
ms.assetid: 8FD5728C-30E3-4998-A01D-80894BDB379A
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5ea28fcbc8e85286083521fe4cf00cb8ddd5747b
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242915"
---
# <a name="indicator-testing"></a>インジケーター テスト


このトピックでは、一般的なインジケーターの手順と例について説明します。

## <a name="span-idtouchkbdspanspan-idtouchkbdspantouch-keyboard-deployment-steps"></a><span id="touchkbd"></span><span id="TOUCHKBD"></span>タッチキーボード展開の手順


次の手順では、ユーザーがタスクバーから開くのではなく、タッチキーボードを自動的に開くかどうかをテストします。 テストで "タッチキーボード展開の手順を実行する" ように指示するたびに、次の手順を適用します。

1.  Windows ボタンを押して **[スタート]** に移動します。
2.  スライドして **[Charms]** メニューを表示し、 **[検索]** を選択します。
3.  [編集] フィールドをタップします。

## <a name="span-idconvspanspan-idconvspanslatelaptop-mode-conversion-steps"></a><span id="conv"></span><span id="CONV"></span>スレート/ラップトップモードの変換手順


テストで示されているようにスレート (またはラップトップ) に変換します。

**注**   複数の方法を使用してシステムをスレートモードに変換できる場合は、メソッドごとにテストステップを繰り返してください。

さまざまなフォームファクターで、次のようなさまざまな変換方法を使用できます。

-   キーボードの接続または切断
-   画面を反転する
-   画面を回転させる
-   画面をスライドしてキーボードを覆う、または見つける

**変換の例:**

![変換可能なキーボードのアタッチとデタッチ](images/keyboardattachdetachconvertible.jpg)

**図1キーボードのアタッチとデタッチの変換**

![画面の回転を変換可能](images/screenswivelconvertible.jpg)

**図2画面の回転の変換**

 

**スレートの例:**

-   キーボードがデタッチされました
-   キーボードは存在しますが、入力しやすいようにアクセスできません
    -   キーボード flapped の下
    -   スライドの下
    -   Swivelled

**ラップトップモード:**

キーボードは存在し、入力しやすくするために使用できます。

## <a name="span-idlaptop_slate_mode_indicator_scenariosspanspan-idlaptop_slate_mode_indicator_scenariosspanspan-idlaptop_slate_mode_indicator_scenariosspanlaptopslate-mode-indicator-scenarios"></a><span id="Laptop_slate_mode_indicator_scenarios"></span><span id="laptop_slate_mode_indicator_scenarios"></span><span id="LAPTOP_SLATE_MODE_INDICATOR_SCENARIOS"></span>ノート pc/スレートモードインジケーターのシナリオ


コンバーチブルのエンドツーエンドのインジケーターテストを実行して、次の領域で潜在的な問題を明らかにすることが重要です。

-   システムをあるモードから別のモードに変換するときのさまざまなタイミング。
-   変換可能なの機械的な仕様。

 

 




