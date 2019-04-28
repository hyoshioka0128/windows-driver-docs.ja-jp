---
title: ミニドライバーで複数の GPD ファイルを使用する
description: ミニドライバーで複数の GPD ファイルを使用する
ms.assetid: 2ec08b46-a286-4af8-a5d4-e0306f731b3f
keywords:
- GPD ファイル WDK Unidrv, 複数
- 複数の GPD ファイル WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8527a64aa417c2409ad31cf78e843dc61127bf31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374240"
---
# <a name="using-multiple-gpd-files-in-a-minidriver"></a>ミニドライバーで複数の GPD ファイルを使用する





Unidrv ミニドライバーは、1 つ以上の GPD ファイルで構成できます。 これにより、1 つまたは複数の GPD ファイルでは、複数のプリンターに共通する配置特性をし、特定のプリンターの個々 の GPD ファイルのファイルにこれらの一般的な GPD を含めるします。

使用する追加の GPD ファイルを含める\*Include ディレクティブで、記載されて[プリプロセッサ ディレクティブ](preprocessor-directives.md)します。 複数を使用する\*の次の例で示すディレクティブを含めます。

```cpp
*Include: "common1.gpd"
*Include: "common2.gpd"
*Include: "common3.gpd"
```

\*Include ディレクティブの filename パラメーターが、マクロの参照にすることはできませんし、パスの指定を含めることはできません。

各インクルード ファイルが完全な GPD ファイルのエントリで終了する必要があり、ファイルと同じ数の左と右中かっこを含める必要があります。 インクルード ファイルに含めることができますも\*ディレクティブが含まれます。

GPD パーサーが最上位レベルの GPD ファイルを処理し、すべて場合 1 つの長いファイルと同様にファイルが含まれます。 そのため、1 つのファイルで定義されているマクロは、その後に含まれているファイルで参照できます。 GPD ファイルのエントリが重複している場合、最近に解析されたエントリには、前のものが置き換えられます。 重複していないエントリは、Unidrv のデータベースに追加されます。

 

 




