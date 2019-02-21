---
title: インジケーターのテスト
description: このトピックでは、インジケーターの一般的な手順の手順と例について説明します。
ms.assetid: 8FD5728C-30E3-4998-A01D-80894BDB379A
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5ea28fcbc8e85286083521fe4cf00cb8ddd5747b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559371"
---
# <a name="indicator-testing"></a>インジケーターのテスト


このトピックでは、インジケーターの一般的な手順の手順と例について説明します。

## <a name="span-idtouchkbdspanspan-idtouchkbdspantouch-keyboard-deployment-steps"></a><span id="touchkbd"></span><span id="TOUCHKBD"></span>タッチ キーボードの展開手順


次の手順では、タッチ キーボードが自動的に (ではなく、ユーザーは、タスク バーから開くこと) が開くかどうかをテストします。 テストによって「を実行するタッチ キーボードの配置手順」するように指示するたびに、次の手順を適用します。

1.  移動する Windows ボタンを押して**開始**します。
2.  表示するスライド、**チャーム**メニュー選択し、**検索**します。
3.  編集フィールドにタップします。

## <a name="span-idconvspanspan-idconvspanslatelaptop-mode-conversion-steps"></a><span id="conv"></span><span id="CONV"></span>スレート/ラップトップ モード変換手順


テストで示されている、スレート (またはラップトップ) に変換します。

**注**  場合は、システムは、1 つ以上のメソッドを使用してスレート モードに変換できる、各メソッドのテスト ステップを繰り返してください。

次のように、変換のさまざまな方法についてさまざまなフォーム ファクターを許可します。

-   アタッチまたはデタッチ キーボード
-   画面を反転します。
-   画面の回転
-   説明またはキーボードを明らかに、画面をスライドします。

**変換の例:**

![キーボードのアタッチし、デタッチを変換できます。](images/keyboardattachdetachconvertible.jpg)

**図 1 キーボードは、アタッチし、デタッチの変換**

![画面の回転の変換](images/screenswivelconvertible.jpg)

**図 2 画面の回転の変換**

 

**スレートの例:**

-   キーボードのデタッチ
-   キーボードの入力を快適に存在するもののアクセスできません。
    -   キーボードの下にある flapped
    -   下にスライドします。
    -   Swivelled

**ラップトップ モード:**

キーボードでは、存在し、アクセスを快適に入力します。

## <a name="span-idlaptopslatemodeindicatorscenariosspanspan-idlaptopslatemodeindicatorscenariosspanspan-idlaptopslatemodeindicatorscenariosspanlaptopslate-mode-indicator-scenarios"></a><span id="Laptop_slate_mode_indicator_scenarios"></span><span id="laptop_slate_mode_indicator_scenarios"></span><span id="LAPTOP_SLATE_MODE_INDICATOR_SCENARIOS"></span>ラップトップ/スレート モードのインジケーターのシナリオ


エンド ツー エンドのインジケーター コンバーチブル次の領域における潜在的な問題を公開するためのテストを実行する必要があります。

-   システムを 1 つのモードから別のモードを変換する際のさまざまなタイミングです。
-   機械の詳細、変換可能なのです。

 

 




