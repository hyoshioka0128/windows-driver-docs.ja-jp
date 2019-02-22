---
title: データ型のテンプレートの継承
description: データ型のテンプレートの継承
ms.assetid: c2ecc091-8fdc-4666-9cdf-629903f13f6f
keywords:
- WDK GDL、データ型のテンプレート
- データ型の WDK GDL、テンプレート継承
- WDK GDL、継承のテンプレート
- WDK GDL の継承
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6944f9d58e45413a84a02f5c71321fe492f665b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528185"
---
# <a name="data-type-template-inheritance"></a>データ型のテンプレートの継承


データ型のテンプレートは、定義済みのデータ型のテンプレートからプロパティを継承できます。 すべて認識は、基本テンプレートを適切なプロパティが継承されます。 継承されたプロパティは、派生テンプレートで再定義することはできません。

派生テンプレートは、他のテンプレートを任意のレベルに継承できます。 継承するためのテンプレートを指定するだけという名前を使用して、 \*Inherits ディレクティブ。 基本のテンプレートは、データ型のテンプレートである必要があります。

基本のテンプレートとして機能するテンプレートは、完全に定義する必要はありません。 \*仮想。**TRUE**ディレクティブのテンプレートを部分的に定義できることをパーサーに通知するために使用します。 (最もベースのテンプレートを含む、する必要がありますただし、、  **\*DataType**ディレクティブ。)。派生テンプレートは、データ型の定義を完了できます。 派生テンプレートでは、データ型の定義を完了できない場合にする必要がありますを明示的に宣言する自体**仮想**します。 **仮想**ディレクティブは継承されません。 使用して仮想テンプレートを参照することはできません、  **\*ElementType**または **\*ValueType**ディレクティブ。 を通してのみ参照できます、  **\*Inherits**ディレクティブ。

**注**  パーサー フィルターの既定値を自動的に作成する、  **\*ArraySize**ディレクティブがない場合がある場合、  **\*ElementType**ディレクティブは、複合データ型で指定されます。 その結果、  **\*ArraySize**前に定義できます **\*ElementType** (定義して **\*ArraySize**はテンプレートで定義するテンプレートによって、その後継承 **\*ElementType**)、逆は許可されていませんが、(つまり、  **\*ElementType**前に定義することはできません **\*ArraySize**)。

 

### <a name="schemas"></a>スキーマ

スキーマが不完全なデータの種類のテンプレートでは発生しません。 冗長なスキーマ定義を避けるためには、スキーマが既にいるテンプレートから派生したテンプレートのスキーマは発生しません。 この制限は、継承の助けなし、1 つのプリミティブ データ型の複数のバリエーションが定義されている場合に発生する同じプリミティブ データ型の複数の定義を排除します。 **仮想**ディレクティブでは、スキーマが出力されるかどうかは影響しません。 平均的なユーザーは、スキーマが出力されるときの詳細を理解する必要はありません。 このパーサー フィルターが自動的に処理されます。

### <a name="binding"></a>バインディング

定義またはによって参照される基本のテンプレートでは、継承されるプロパティ、  **\*Inherits:** ディレクティブは、派生テンプレートで直接継承されます。 によって派生または基本テンプレートを参照するときに、  **\*ElementType**別のデータ型のテンプレートからディレクティブまたは **\*ValueType**属性テンプレートからディレクティブ名前付きのテンプレートがバインドされています。 複合バインディングのアルゴリズムなどの構成要素テンプレートのメンバーにバインドするために使用することはありません。 このようなアルゴリズムは意味を成しません値名または間接のバインディングを実装するために必要なインスタンス名があるないためです。

### <a name="example"></a>例

データ型の継承の使用をいくつかのデータ型のテンプレートに共通するプロパティ。 次の例では、基本のテンプレートは、いくつかの配列のデータ型に共通するプロパティを定義します。 継承の 2 つのレベルが使用されることに注意してください。

```cpp
*Template:  GENERIC_ARRAY  *%  Basemost Template
{
    *Type:  DATATYPE
    *Virtual:  TRUE
    *DataType:   ARRAY
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
}
*Template:  LIST_OF_TYPE  *%  first level derived Template
{
    *Inherits:  GENERIC_ARRAY
    *ArrayLabel: "LIST"
    *ArraySize: [*]
    *Virtual:  TRUE
}

*Template:  DT_INT_ARRAY  *%  first level derived Template
{
    *Inherits:  GENERIC_ARRAY
    *ElementType:  INTEGER
    *Virtual:  TRUE
}

*% ===================
*%  Second-level templates derived from LIST_OF_TYPE
*% ===================

*Template:  COLORS_LIST  
{
    *Inherits:  LIST_OF_TYPE
    *ElementType:  COLORS
    *ElementTags: (colors)
}
*Template:  STD_VAR_LIST
{
    *Inherits:  LIST_OF_TYPE
    *ElementType:  STD_VAR
    *ElementTags: (Standard_Variable)
}

*% ===================
*%  Second-level templates derived from DT_INT_ARRAY
*% ===================

*Template:  DT_POINT
{
    *Inherits:  DT_INT_ARRAY
    *ArrayLabel: "POINT"          
    *ElementTags: (X_pos, Y_pos)
    *ArraySize: 2
}
*Template:  DT_PAIR_OF_INTS
{
    *Inherits:  DT_INT_ARRAY
    *ArrayLabel: "PAIR"
    *ElementTags: (width, height)
    *ArraySize: 2
}
*Template:  RECTANGLE
{
    *Inherits:  DT_INT_ARRAY
    *ArrayLabel: "rect"
    *ElementTags: (left, top, right, bottom)
    *ArraySize: 4
}
```

 

 




