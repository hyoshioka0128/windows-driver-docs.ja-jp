---
title: トレースの呼び出しと、fprintf 関数を redefine 方法
description: トレースの呼び出しと、fprintf 関数を redefine 方法
ms.assetid: def82d48-454b-421b-a63d-695dae733fd0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98a9ca30dca368e7bf167f3eaf94a61324b0f74c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341680"
---
# <a name="how-do-i-redefine-an-fprintf-function-as-a-tracing-call"></a>トレース呼び出しとして fprintf 関数を再定義する方法


**Fprintf**関数の呼び出しに変換されて最終的に、 **sprintf**関数呼び出しを使用している場合に特に perceptibly、パフォーマンスを低下させるそのリソースを大量に消費の呼び出し何度も何度も。

再定義する、 **fprintf**トレース メッセージはバイナリ形式で格納され、トレース ログを表示するまで延期が書式設定するため、トレースの呼び出しははるかに効率的に機能します。

などの印刷機能を再定義する**fprintf**トレースの呼び出しと、結果として得られる呼び出しが 2 つの処理を行う必要があります。

-   エラー、警告、またはノイズなど、トレース機能の既定のレベルを割り当てます。

-   ハンドルを無視します。

次の例は、両方を行う関数の説明を示しています。

```
-func:fprintf{LEVEL=Noise}(NULL,MSG,...)
```

Localwpp.ini などのローカル構成ファイルでこの関数の説明を定義したり、使用して、 **- func**実行のパラメーター\_WPP (WPP プリプロセッサを呼び出すマクロ) 関数の説明を定義します。

実行の省略可能なパラメーターの完全な一覧については\_WPP を参照してください[WPP プリプロセッサ](wpp-preprocessor.md)します。

 

 





