---
title: GDL は、コンストラクトの 4 つの定義バリアントを練習します。
description: GDL は、コンストラクトの 4 つの定義バリアントを練習します。
ms.assetid: b923b5f8-6e60-44a0-a38e-8bfa315281c5
keywords:
- GDL WDK、例
- WDK GDL の例
- WDK GDL のチュートリアル
- GDL WDK、チュートリアル
- WDK GDL、構造の作成を構築します。
- WDK を構築します GDL を作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19a52c47e71acdf59224d7694e434f67094b30d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573557"
---
# <a name="gdl-exercise-4-defining-variants-of-constructs"></a>GDL 演習 4:コンストラクトのバリアントを定義する


### <a href="" id="exercise"></a> 演習

構造の変更\*から PFeature[演習 3](gdl-exercise-3--creating-root-level-constructs.md) 2 つのバリエーションを定義することで。\*PFeature:ここをクリックし、 \*PFeature InputTray します。

含まれている POption \*PFeature:用紙サイズには、次の属性があります。**\*名前**、 **\*コマンド**、  **\*Papersize**します。

含まれている POption \*PFeature:InputTray には、次の属性があります。**\*名前**、 **\*コマンド**、および**\*容量:**  *\#シートの*します。

これらの 2 種類の一般的なプロパティを抽象化するためのテンプレートを作成する\*POptions します。

### <a href="" id="solution"></a> ソリューション

次のテンプレートは、条件を満たします。

```cpp
*Template:  COMMAND_TYPE
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_STRING
    *FilterTypeName: "COMMAND_STRING"
}
*Template:  ACOMMAND
{
    *Name:  "*Command"
    *Type:  ATTRIBUTE
    *ValueType:  COMMAND_TYPE
}
```

さらに次のオプションの派生テンプレートでは、仮想テンプレート POPTION のプロパティを定義します。

```cpp
*Template:  GENERIC_OPTION
{
    *Inherits: POPTION
    *Members:  (NAME, ACOMMAND)
    *Instances:  <ANY>
}
*Template:  XML_INT4
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "int"
}
*Template:  INTEGER
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_INT4
    *FilterTypeName: "HEX_OR_INT"
}
*Template:  XML_FLOAT
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "float"
}
*Template:  PAIR_OF_FLOAT
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  XML_FLOAT
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
    *ArrayLabel: "PAIR"
    *ElementTags: (width, height)
    *ArraySize: 2
}
*Template:  LEN_UNITS
{
    *Type:  DATATYPE
    *DataType:   ENUMERATOR
    *XMLDataType: "LengthUnits"
    *EnumeratorList: (inches, mm, microns, pixels)
}
*Template:  PAGE_DIM
{
    *Type:  DATATYPE
    *DataType:   COMPOSITE
    *ElementType: (PAIR_OF_FLOAT, LEN_UNITS)
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (dimensions, units)
}
*Template:  PAPERDIMENSIONS
{
    *Name: "*PaperSize"
    *Type:  ATTRIBUTE
    *ValueType:  PAGE_DIM
}
```

次のオプションの派生テンプレートをさらにジェネリック テンプレートのプロパティを専門と\_オプション。

```cpp
*Template:  PAPERSIZE_OPTION
{
    *Name:  "*POption"  *%  Isolate branch from Base Templates
    *Inherits: GENERIC_OPTION
    *Members:  (PAPERDIMENSIONS)
    *Instances:  <ANY>
}


*Template:  PAPERSIZE_FEATURE
{
    *Inherits: PFEATURE
    *Members:  (PAPERSIZE_OPTION)
    *Instances:  PaperSize
}

*Template:  TRAY_CAPACITY
{
    *Name: "*Capacity"
    *Type:  ATTRIBUTE
    *ValueType:  INTEGER
}
```

次のオプションの派生テンプレートをさらにジェネリック テンプレートのプロパティを専門と\_オプション。

```cpp
*Template:  INPUTTRAY_OPTION
{
    *Name:  "*POption"   *%  Isolate branch from Base Templates
    *Inherits: GENERIC_OPTION
    *Members:  (TRAY_CAPACITY)
    *Instances:  <ANY>
}

*Template:  INPUTTRAY_FEATURE
{
    *Inherits: PFEATURE
    *Members:  (INPUTTRAY_OPTION)
    *Instances:  InputTray
}
```

 

 




