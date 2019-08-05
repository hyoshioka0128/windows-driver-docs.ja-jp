---
title: GDL 演習 3 を作成するルート レベルのコンストラクト
description: GDL 演習 3 を作成するルート レベルのコンストラクト
ms.assetid: 3c7ad284-b77c-4ad3-8334-2fe5b026e340
keywords:
- GDL WDK、例
- WDK GDL の例
- WDK GDL のチュートリアル
- GDL WDK、チュートリアル
- WDK GDL、構造の作成を構築します。
- WDK を構築します GDL を作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acd075821593522ea53e5aefc061c59afb183815
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388114"
---
# <a name="gdl-exercise-3-creating-root-level-constructs"></a>GDL 演習 3:ルート レベル コンストラクトを作成する


### <a href="" id="exercise"></a> 演習

スキーマを変更する[演習 1](gdl-exercise-1--implementing-a-gdl-schema.md)という名前のコンストラクトを導入する\*PFeature ルート レベルでのみ検出できます。

次の条件を使用します。

-   \*PFeature には、任意のインスタンスの名前を持つことができます。

-   \*PFeature メンバーは、属性の名前付き **\*名前**と **\*DefaultOption**します。

-   \*PFeature がという名前のコンス トラクター メンバー  **\*Poption**仮想化を宣言する必要があります。

### <a href="" id="solution"></a> ソリューション

次のテンプレートは、上記の条件を満たします。

```cpp
*Template:  POPTION
{
    *Name:  "*POption"
    *Type: CONSTRUCT
    *Virtual:  TRUE
}

*Template:  NAME
{
    *Name:  "*Name"
    *Type:  ATTRIBUTE
    *ValueType:  NORMAL_STRING
}

*Template:  SYMBOL
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_STRING
    *FilterTypeName: "SYMBOLNAME"
}
*Template:  DEFAULT_OPT
{
    *Name: "*DefaultOption"
    *Type:  ATTRIBUTE
    *ValueType:  SYMBOL
}

*Template:  PFEATURE 
{
    *Name:  "*PFeature"
    *Type: CONSTRUCT
    *Members:  (POPTION, NAME, DEFAULT_OPT)
    *Instances:  <ANY>
}
*Template:  ROOT2
{
    *Inherits: ROOT
    *Members:  (PFEATURE)
}
```

 

 




