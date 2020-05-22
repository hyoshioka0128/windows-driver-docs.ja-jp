---
title: 例3一般的な開始コマンド
description: 例3一般的な開始コマンド
ms.assetid: a0e8580d-b841-4077-82f5-6aaef57b0ff7
keywords:
- トレースセッション WDK、開始
- start コマンド
- -start コマンド
- トレースセッションの開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13b2de453c55b01d3b42f3a826c587f02b61ecbf
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769706"
---
# <a name="example-3-typical-start-command"></a>例 3: 一般的な開始コマンド

## <span id="ddk_typical_start_command_tools"></span><span id="DDK_TYPICAL_START_COMMAND_TOOLS"></span>

次のコマンド形式は、通常、トレースセッションを開始するために使用されます。

```
tracelog -start MyTrace -guid MyProvider.guid -f d:\traces\testtrace.etl -flag 2 -level 0xFFFF
```

このコマンドは、"MyTrace" という名前のトレースセッションを開始します。

この例では、 **-guid**パラメーターを使用して、myprovider の guid ファイルを示しています。このファイルには、プロバイダーのコントロール guid だけを含む単純なテキストファイルが含まれています。 また、 **-guid**パラメーターを使用して、Tracedrv などの[コントロールの guid ファイル](control-guid-file.md)を使用することもできます。 Tracedrv は[tracedrv](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/tracedrv/)サンプルに含まれています。

このコマンドには、イベントトレースログファイルの名前と場所を指定する **-f**パラメーターが含まれています。 フラグの設定を指定する **-flag**パラメーターと、レベルの設定を指定する **-level**パラメーターが含まれています。 これらのパラメーターは省略できますが、フラグまたはレベルを設定しない限り、トレースプロバイダーによってはトレースメッセージが生成されません。
