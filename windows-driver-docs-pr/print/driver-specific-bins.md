---
title: ドライバー固有のビン
description: ドライバー固有のビン
ms.assetid: 4c014e64-9e82-4058-9ec9-51769102f815
keywords:
- デバイスに固有のビンの WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ec7f2cbce3af3486ec01fefea5f1820c54510d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360572"
---
# <a name="driver-specific-bins"></a>ドライバー固有のビン


ドライバー固有の箱の名前を持つ双方向通信のスキーマを拡張するかまいません。 この場合、ドライバーのみは追加の箱の名前を認識することになります。

```cpp
<InputBin name="AAA" mibName="TRAY A"/>
```

上記のコード例は、次の 4 つのクエリの結果します。 InputBin のコンス トラクターが 4 つの新しいクエリを生成することを思い出してください。

```cpp
\Printer.Layout.InputBins.AAA:Installed
\Printer.Layout.InputBins.AAA:Level
\Printer.Layout.InputBins.AAA:MediaType
\Printer.Layout.InputBins.AAA:MediaSize

<OutputBin name="BBB" mibName="BIN B"/>
```

上記のコード例は、次の 2 つのクエリの結果します。 OutputBin のコンス トラクターに 2 つの新しいクエリが生成されることを思い出してください。

```cpp
\Printer.Finishing.OutputBins.BBB:Installed
\Printer.Finishing.OutputBins.BBB:Level
```

 

 




