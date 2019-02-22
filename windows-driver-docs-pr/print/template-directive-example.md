---
title: テンプレート ディレクティブの例
description: テンプレート ディレクティブの例
ms.assetid: ae8fe5e6-ee79-424d-80b3-fd6300257977
keywords:
- 実稼働ディレクティブ WDK GDL
- WDK GDL、例のテンプレート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3eac1e8b9dbb3de2b258738552d21c040a2755
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537170"
---
# <a name="template-directive-example"></a>テンプレート ディレクティブの例


次の例では、単純な運用環境を示します。

```cpp
  *Production: EXACTLY_ONE
  {
        *Production: SATISFY_ALL
        {
            *Member: GENERIC_OPTION {*Occurs: [1-*] }
            *Member: DEFAULT_OPT {*Occurs: [0-*] }
        }
        *Production: SATISFY_ALL
        {
            *Member: GENERIC_OPTION {*Occurs: [0] }
            *Member: DEFAULT_OPT {*Occurs: [0] }
        }
  }
```

この運用環境でホスト テンプレートにバインドされているコンス トラクターのインスタンスには、次のいずれかを含めることができます。

-   いずれかの既定のインスタンスがない\_OPT またはジェネリック\_オプション。

-   1 つまたは複数のジェネリック インスタンス\_オプションと既定のインスタンスがない\_オプトインします。

-   ジェネリックの 1 つまたは複数のインスタンス\_オプションと既定のインスタンスを 1 つまたは複数\_オプトインします。

-   コンス トラクターのインスタンスが既定の 1 つまたは複数のインスタンスを含めることはできません\_ジェネリックの少なくとも 1 つのインスタンスを指定しないで OPT\_オプション。

継承されたテンプレートで定義されている生産も評価され、必要もありますホスト テンプレートは、他のテンプレートから継承している場合**TRUE**に評価されるホスト テンプレートを運用環境の**TRUE**.

 

 




