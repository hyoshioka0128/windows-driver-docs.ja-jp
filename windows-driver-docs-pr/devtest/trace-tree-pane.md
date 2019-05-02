---
title: Trace Tree (トレース ツリー) ウィンドウ
description: Trace Tree (トレース ツリー) ウィンドウ
ms.assetid: 0035e926-7332-45a6-84ea-8c36bc23c61a
keywords:
- WDK Static Driver Verifier のペイン
- 静的ドライバー検証レポートの WDK、トレースのツリー ウィンドウ
- トレースのツリー ペイン WDK Static Driver Verifier
- トレース WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe7b768ed2dcd0294ade866b9e5dcf182bb78169
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373146"
---
# <a name="trace-tree-pane"></a>Trace Tree (トレース ツリー) ウィンドウ


**トレース ツリー**ペインは、次のスクリーン ショットに示すように、ルール違反へのパスで実行されたソース コードの重要な要素のトレースが表示されます。

![規則違反へのパスで実行されたソース コードの重要な要素のトレースを表示するトレースのツリー ウィンドウのスクリーン ショット](images/sdv-tracetree.png)

関数呼び出しと割り当てなど、これらの重要な要素がすべての規則違反などの SDV のオペレーティング システム モデル コード (sdv harness.c ファイル)、SDV 規則のソース ファイルを検出するために使用されたソース ファイルから取得 (\*.slic)、およびドライバーのソース コードです。 複数のファイルが作成された場合でも、実行された、順序でコード要素が表示されます。

SDV の表示の調整、**トレース ツリー**内の表示 ウィンドウ、[ソース コード ウィンドウ](source-code-pane.md)と[の状態 ウィンドウ](state-pane.md)します。 ソース コードをステップ実行すると、**トレース ツリー**ウィンドウで、SDV は自動的に、対応する行のコードのハイライト、**ソース コード**ウィンドウと、対応するでの変数の値を表示します特定の時点、**状態**ウィンドウ。

このセクションの内容:

[トレースのツリー ペインを理解します。](understanding-the-trace-tree-pane.md)

[トレースのツリー ペインで色の設定](color-coding-in-the-trace-tree-pane.md)

[ツリー ウィンドウ操作をトレースします。](trace-tree-pane-actions.md)

 

 





