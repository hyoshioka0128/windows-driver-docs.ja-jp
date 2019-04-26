---
title: トレース ビューアーの概要
description: トレース ビューアーの概要
ms.assetid: 2b839e7f-770f-4bf4-96e1-98524768f4f0
keywords:
- Static Driver Verifier レポート WDK、欠陥ビューアー
- 欠陥ビューアー WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd007d9372688d1cb3b043de1f349c971a7f8c0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351806"
---
# <a name="understanding-the-trace-viewer"></a>トレース ビューアーの概要


トレース ビューアーは、SDV 検証用に選択された規則には少なくとも 1 つの規則違反を検出したときに使用できます。

トレース ビューアーは、3 つのウィンドウで構成されます。

-   [トレースのツリー ペイン](trace-tree-pane.md)

-   [ソース コード ウィンドウ](source-code-pane.md)

-   [状態ウィンドウ](state-pane.md)

次のスクリーン ショットでは、欠陥のビューアー ウィンドウとそのトレース-ツリー、ソース コードを示します。

![欠陥ビューア ウィンドウとそのトレース ツリー、ソース コード、および結果ペインに表示のスクリーン ショット](images/sdv-defectviewerlabeled.png)

SDV は、自動的に 3 つの欠陥ビューアー ウィンドウの表示を調整します。 ソース コード要素を選択する場合など、**トレース ツリー**ウィンドウで、SDV 自動的にカーソルを移動、対応する行のコード、**ソース コード**ウィンドウ (その逆)。

同様に、ソース コード要素で選択されている場合、**トレース ツリー**または**ソース コード**ペイン SDV を監視して、それらの変更は、に自動的に表示される変数の値を変更する**状態**ウィンドウ。

 

 





