---
title: 既定の GDL 構成
description: 既定の GDL 構成
ms.assetid: 9963513b-52dc-4fb7-8f85-abca2975c36d
keywords:
- GDL WDK の構成
- パーサー WDK GDL、既定の構成を作成します。
- WDK GDL、既定の構成の構成
- WDK の既定の GDL 構成
- WDK GDL、例の構成
- DefaultOption ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88d88d518b890860cce0f1e05d614425fd19d636
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384953"
---
# <a name="default-gdl-configurations"></a>既定の GDL 構成


クライアントが特定の構成を持たない場合は、パーサーを作成して呼び出すことによって、既定の構成を返すを問わ**GetDefaultConfig()** します。 パーサーは、各パラメーターに既定値を割り当てることで、既定の構成を作成します。 使用して、既定値が指定されて、  **\*DefaultOption**ディレクティブ。 **\*DefaultOption**ディレクティブの子エントリを **\*機能**を構築します。 **\*DefaultOption**のいずれかで表示される構造タグのいずれかの値として指定する必要があります、 **\*オプション**を構築します。 詳細については **\*DefaultOption**、 **\*機能**、および **\*オプション**を参照してください[GDL構成ディレクティブ](gdl-directives-for-configurations.md)

たとえば、気象パラメーターの既定値が Sunny であるとします。 次に、既定値を定義するのに次のコード例を使用できます。

```cpp
*Feature: Weather
{
   *DefaultOption: Sunny
   *Option: Sunny{}
   *Option: Cloudy{}
}
```

場合、  **\*DefaultOption**ディレクティブがない場合、パーサーは仮定最初 **\*オプション**は既定値です。

できます[GDL の既定の構成を変更する](changing-the-default-gdl-configuration.md)します。

 

 




