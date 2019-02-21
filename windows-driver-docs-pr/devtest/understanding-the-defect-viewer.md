---
title: トレース ビューアーを理解します。
description: トレース ビューアーを理解します。
ms.assetid: 2b839e7f-770f-4bf4-96e1-98524768f4f0
keywords:
- Static Driver Verifier レポート WDK、欠陥ビューアー
- 欠陥ビューアー WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd007d9372688d1cb3b043de1f349c971a7f8c0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557297"
---
# <a name="understanding-the-trace-viewer"></a>トレース ビューアーを理解します。


トレース ビューアーは、SDV 検証用に選択された規則には少なくとも 1 つの規則違反を検出したときに使用できます。

トレース ビューアーは、3 つのウィンドウで構成されます。

-   [トレースのツリー ペイン](trace-tree-pane.md)

-   [ソース コード ウィンドウ](source-code-pane.md)

-   [状態ウィンドウ](state-pane.md)

次のスクリーン ショットでは、欠陥のビューアー ウィンドウとそのトレース-ツリー、ソース コードを示します。

![欠陥ビューア ウィンドウとそのトレース ツリー、ソース コード、および結果ペインに表示のスクリーン ショット](images/sdv-defectviewerlabeled.png)

SDV は、自動的に 3 つの欠陥ビューアー ウィンドウの表示を調整します。 ソース コード要素を選択する場合など、**トレース ツリー**ウィンドウで、SDV 自動的にカーソルを移動、対応する行のコード、**ソース コード**ウィンドウ (その逆)。

同様に、ソース コード要素で選択されている場合、**トレース ツリー**または**ソース コード**ペイン SDV を監視して、それらの変更は、に自動的に表示される変数の値を変更する**状態**ウィンドウ。

 

 





