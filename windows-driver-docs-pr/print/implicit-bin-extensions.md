---
title: 暗示的なビン拡張機能
description: 暗示的なビン拡張機能
ms.assetid: 2aaa9e48-59f9-4c87-b592-ed60469cf747
keywords:
- 暗黙的な箱拡張機能の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bed3da789f12da3f0fb45c38316cc648b5ad800e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571203"
---
# <a name="implicit-bin-extensions"></a>暗示的なビン拡張機能


各 InputBin または OutputBin コンストラクトは、2 つまたは複数のクエリをスキーマを拡張します。 InputBin 拡張機能には、次の 4 つの新しいスキーマの値が生成されます。レベル、メディアの種類、および MediaSize は、インストールされます。 OutputBin 拡張機能には、スキーマの 2 つの新しい値が生成されます。インストールされているとレベルを設定します。

これらのスキーマは、Tcpbidi.xsd ファイルで定義されて、 **InputBins**と**OutputBins**プロパティ。

```cpp
<InputBin name="TopBin" mibName="TRAY 1"/>
```

前の InputBin では、次の 4 つのクエリで結果を作成します。

```cpp
\Printer.Layout.InputBins.TopBin:Installed
\Printer.Layout.InputBins.TopBin:Level
\Printer.Layout.InputBins.TopBin:MediaType
\Printer.Layout.InputBins.TopBin:MediaSize

<OutputBin name="TopBin" mibName="STANDARD BIN"/>
```

上記の OutputBin では、次の 2 つのクエリの結果を作成します。

```cpp
\Printer.Finishing.OutputBins.TopBin:Installed
\Printer.Finishing.OutputBins.TopBin:Level
```

 

 




