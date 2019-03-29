---
title: GDL 演習 GDL スキーマを実装する 1
description: GDL 演習 GDL スキーマを実装する 1
ms.assetid: 0adfef5a-4211-45e9-bb65-8174822efdc5
keywords:
- GDL WDK、例
- WDK GDL の例
- WDK GDL のチュートリアル
- GDL WDK、チュートリアル
- スキーマ WDK GDL、GDL スキーマを実装します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b806cbb9e93fef831741f0b4831ed9710374b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578257"
---
# <a name="gdl-exercise-1-implementing-a-gdl-schema"></a>GDL 演習 1:GDL スキーマを実装する


### <a href="" id="exercise"></a> 演習

属性の 3 つのカテゴリを作成し、構成要素を配置できるに関する制限事項に強制しませんスキーマを実装します。

これらの属性は、次のカテゴリに分類する必要があります。

-   ルート レベルで、構造内に表示できる属性。

-   ルート レベルでのみ表示できる属性。

-   コンストラクト内でのみ表示できる属性。

一切のキーワードは、スキーマで定義しないでください。将来のキーワードのフレームワークを含めるだけです。

**注**  テンプレートを使用すると、仮想スキーマ--GDL エントリを一切定義しません、スキーマを作成することができます。 この方法で定義されている基本スキーマは、このスキーマの将来の拡張関係なくその影響を行使します。

 

### <a href="" id="solution"></a> ソリューション

次のコード例では、この手順を完了する 1 つの方法を示します。

```cpp
*Template:  ATTRIBUTE
{
    *Type:  ATTRIBUTE
    *Virtual:  TRUE
}
*Template:  ROOT_ATTRIB
{
    *Inherits: ATTRIBUTE
    *Virtual:  TRUE
}
*Template:     CONSTRUCT_ATTRIB  *%  May not appear at Root level
{
    *Inherits: ATTRIBUTE
    *Virtual:  TRUE
}
*Template:     FREEFLOAT
{
    *Inherits: ATTRIBUTE
    *Virtual:  TRUE
}
*Template:  CONSTRUCTS
{
    *Type: CONSTRUCT
    *Members:  ( CONSTRUCTS, FREEFLOAT, CONSTRUCT_ATTRIB)
    *Virtual:  TRUE
}

*Template:  ROOT
{
            *Type: CONSTRUCT
            *AllowNewMembers: FALSE
            *Name:  "root"
            *Instances:  <ANY>
            *Members:  (ROOT_ATTRIB, FREEFLOAT, CONSTRUCTS)
}
```

**注**  次の手順で使用するための MasterTemplate.gdl ファイルでは、前の例で、テンプレートを配置できます。

 

 

 




