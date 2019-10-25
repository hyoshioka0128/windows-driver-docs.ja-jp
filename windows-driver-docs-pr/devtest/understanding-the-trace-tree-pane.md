---
title: トレースツリーウィンドウについて
description: トレースツリーウィンドウについて
ms.assetid: 98640d7e-29fc-4397-ac6b-47f4e17f88a1
keywords:
- 静的ドライバー検証ツールレポート WDK、トレースツリーウィンドウ
- トレースツリーペイン WDK 静的ドライバー検証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e81e348b7e05e2f7e77b3cfc71682282fd2f444b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839269"
---
# <a name="understanding-the-trace-tree-pane"></a>トレースツリーウィンドウについて


**[トレースツリー]** ウィンドウは、問題のビューアーにフォーカスがあることを示します。 通常は、 **[トレースツリー]** ウィンドウのコードをステップ実行し、 **[ソースコード]** ペインのコードおよび **[状態]** ペインの値に対する影響を監視します。

**トレースツリー**ペインは、一連の展開可能なノードと折りたたみ可能なノードを含む階層構造に編成されています。 階層は、他の要素が実行される原因となったコード要素を示します。 この形式は、各コード分岐を解釈し、トレースをステップ実行するときにコードセクションを簡単に表示したり非表示にしたりするのに役立ちます。

次のスクリーンショットは、**トレースツリー**ペインの例を示しています。

![欠陥ビューアーの [トレースツリー] ウィンドウのスクリーンショット](images/sdv-tracetree.png)

**トレースツリー**ペインの各コード要素の前に、ソースファイル内の行番号が表示されます。 この番号付けを使用すると、ソースツリーウィンドウとソースファイル内のコード要素を見つけることができます。

**ソースコード**ペインの一部のコード行は、**トレースツリー**ペイン内の複数の要素に対応しています。 この状況は、コード行によって複数のアクションが発生した場合に発生します。 たとえば、関数呼び出しパラメーターが IRQL の場合、関数呼び出しを含むコード行には、現在の IRQL を検索するための呼び出しも含まれる場合があります。次に例を示します。

```
IoReleaseCancelSpinLock(KeGetCurrentIrql());
```

この場合、**トレースツリー**ウィンドウには[**KegetIoReleaseCancelSpinLock entirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kegetcurrentirql)関数呼び出しの重要な要素が含まれ、sdv オペレーティングシステムモデルを呼び出して、ランダムに IRQL を生成[**した後**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))、返された IRQL。

 

 





