---
title: '[Trace Tree] (トレース ツリー) ウィンドウの概要'
description: '[Trace Tree] (トレース ツリー) ウィンドウの概要'
ms.assetid: 98640d7e-29fc-4397-ac6b-47f4e17f88a1
keywords:
- 静的ドライバー検証レポートの WDK、トレースのツリー ウィンドウ
- トレースのツリー ペイン WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c98788e5e772bfc8aa32038a80f832cf77cd3cf9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363798"
---
# <a name="understanding-the-trace-tree-pane"></a>[Trace Tree] (トレース ツリー) ウィンドウの概要


**トレース ツリー**ウィンドウ欠陥ビューアーの焦点であります。 コードでは、順を追って通常、**トレース ツリー**内のコードでは、その効果を見ているときに、ウィンドウ、**ソース コード**ウィンドウ内の値で、**状態**ウィンドウ。

**トレース ツリー**ウィンドウは一連の展開と折りたたみ可能なノードを持つ階層構造に編成されます。 階層では、実行するには、その他の要素の原因となったコード要素を示します。 この形式では各コード分岐を解釈および表示し、トレースをステップ実行すると、簡単にコードのセクションでは非表示にすることができます。

次のスクリーン ショットは例を示しています。**トレース ツリー**ウィンドウ。

![欠陥のビューアーにトレースのツリー ウィンドウのスクリーン ショット](images/sdv-tracetree.png)

内の各コード要素、**トレース ツリー**ウィンドウには、ソース ファイルでの行番号が付きます。 この番号では、ソース ツリー ウィンドウとソース ファイルにコード要素を検索できます。

いくつかの行のコード、**ソース コード**ウィンドウ内の 1 つ以上の要素に対応して、**トレース ツリー**ウィンドウ。 このような状況では、コードの行では、複数のアクションは、するときに発生します。 たとえば、関数呼び出しのパラメーターが、IRQL の場合は、関数呼び出しを含むコード行場合もあります呼び出しなど、現在の IRQL を検索します。

```
IoReleaseCancelSpinLock(KeGetCurrentIrql());
```

このような状況で、**トレース ツリー**ウィンドウには重要な要素が含まれます、 [ **KeGetCurrentIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kegetcurrentirql)関数呼び出し、SDV オペレーティング システムのモデルにいくつかの呼び出しランダムに生成、IRQL とし、呼び出しを[ **IoReleaseCancelSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))返された IRQL とします。

 

 





