---
title: 条件付きのメタデータ
description: 条件付きのメタデータ
ms.assetid: A1C223AB-E9BB-480e-B9ED-75989FD34479
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f484fc7dcc6bb42489311c1f305b52c88d8455b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385070"
---
# <a name="conditional-metadata"></a>条件付きのメタデータ


場合によってはメタデータのランタイム値によって値が変化すると便利です。 条件付きのメタデータにより、モジュール、クラス、またはメソッドのメタデータに基づく特定の条件でのみ適用される[ランタイム パラメーター](runtime-parameters.md)します。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


メタデータ条件を作成するには、メタデータ名の後に角かっこで囲まれた条件を追加します。 条件がの形式である必要があります、[選択クエリ言語](selection.md)します。 変数の値に由来[ランタイム パラメーター](runtime-parameters.md)します。

たとえば、テストに、次のメタデータがあるとします。

```cpp
TEST_METHOD_PROPERTY(L"RunAs", L"Elevated")
TEST_METHOD_PROPERTY(L"Ignore[@NoElevation=true]", L"true")
```

DLL が読み込まれる TAEF が評価され、"@NoElevation= true"条件に基づくランタイム パラメーター。 その場合、ユーザーが"NoElevation"のランタイム パラメーターを true に設定すると、テスト「無視」の名前と値"true"を使用して適用されるメタデータがあります。

1 つのテストに複数の条件付きメタデータが表示されたら場合、それぞれが個別に評価、同様にします。 これは、ランタイム パラメーターの複数の可能な値を認識する、テストする場合に役立ちます。 ことができます。

```cpp
TEST_METHOD_PROPERTY(L"Data:MyTestData[@TestCaseLevel='Low']", L"{ Datum1, Datum2, Datum3 }")
TEST_METHOD_PROPERTY(L"DataSource[@TestCaseLevel='High']", L"Pict:FullDataSet.model?Order=3")
```

テストの前に示したメタデータ使用するユーザー TestCaseLevel を低に設定する場合は、テストのみ呼び出される 3 回ために、[軽量のデータ ソース](light-weight-data-driven-testing.md)します。 ユーザーは、[高] に TestCaseLevel を設定する場合、 [PICT データ ソース](pict-data-source.md)テストの多くのパラメーターの生成に使用されます。 TestCaseLevel が高または低に設定されていない場合のメタデータは追加されません。

## <a name="span-iddefaultspanspan-iddefaultspandefault-values"></a><span id="default"></span><span id="DEFAULT"></span>既定値


特定のメタデータ名の他の条件が true に評価されるない場合にのみ、メタデータを追加する場合とメタデータの名前を追加できます*\[既定\]* します。

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyTest.model")
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='Low']", L"1")
TEST_METHOD_PROPERTY(L"Pict:Order[default]", L"2")
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='High']", L"3")
```

テストに上記のメタデータがあり、ユーザーが、ユーザーが TestCaseLevel を設定していないを Low または高は、Pict: 順序が 2 に設定されます。 Low または高 TestCaseLevel を設定すると場合、Pict: 順序は設定を 1 または 3 では、それぞれ。 Pict: 注文を true に評価されるは、そのテストの条件を少なくとも 1 つあるために、2 の値は適用されません。

のままにしないように注意して、\[既定\]必要な場合。

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyTest.model")
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='Low']", L"1")
TEST_METHOD_PROPERTY(L"Pict:Order", L"2") // This should have [default]
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='High']", L"3")
```

TestCaseLevel が [低] に設定されている場合、上記の一連のメタデータは、次の一連のメタデータと同等です。

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyTest.model")
TEST_METHOD_PROPERTY(L"Pict:Order", L"1")
TEST_METHOD_PROPERTY(L"Pict:Order", L"2")
```

この場合、その使用はありません指定したかどうか PICT データ ソースは「1」または「2」PICT 注文の。

 

 





