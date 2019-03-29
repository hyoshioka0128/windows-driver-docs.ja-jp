---
title: 複合テンプレート データ型の問題
description: 複合テンプレート データ型の問題
ms.assetid: 61f26465-c79d-42e3-94c8-26c2c61ecb98
keywords:
- WDK GDL、データ型のテンプレート
- データ型の WDK GDL、テンプレートのデータ型に関する問題
- データ型、複合 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b54f141501b36833db2ead1b1da50e730b11931
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571129"
---
# <a name="compound-template-data-type-issues"></a>複合テンプレート データ型の問題


複合データ型は他のデータ型から作成され、データ型のいずれかを囲むかっこを使用、すると、すべてのデータ型を囲むかっこかっこで囲んでデータ型をかっこで囲まれてもする必要があります。

たとえば、次のテンプレートを使用して、GPD 整数のリストを定義することを想定しています。

```cpp
*Template:  LIST_OF_INTS
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  INTEGER
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (int)
    *ArraySize: *
}
*Template:  LIST_OF_LIST_OF_INTS
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  LIST_OF_INTS
    *RequiredDelimiter: ":"
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (IntList)
    *ArraySize: *
}
```

次の値のリストの有効なと同等の式を次に、\_の\_一覧\_の\_整数データ型。

```cpp
*ListList: 1,2,3:10,11,12:20,21,22 
*ListList: (1,2,3:10,11,12:20,21,22)
*ListList: ((1,2,3):(10,11,12):(20,21,22))
```

ただし、次の値には、ルールのかっこの入れ子に違反しています。

```cpp
*ListList: (1,2,3):(10,11,12):(20,21,22)
```

前の例の構文エラーが生成されると、[次へ] のコンテキストに [次へ] のかっこが属しているパーサー フィルターが仮定見つけた右かっこは、最も外側のコンテキストに属しているためです。

 

 




