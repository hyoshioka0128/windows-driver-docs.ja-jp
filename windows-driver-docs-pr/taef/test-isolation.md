---
title: テストの分離
description: テストの分離
ms.assetid: AC2A0060-45B9-45ff-87ED-69842F9A567D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76874e5c8a6c67f1a3ad8b1ff282bc665c86469d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558591"
---
# <a name="test-isolation"></a>テストの分離


TAEF を分離プロセスでテストの実行をサポートしています。 これらのプロセスが IsolationLevel メタデータとコマンド ライン オプションに置き換えられないときにを制御します。 これは、意図しないテストの依存関係を検出するため、またはリークしているテストの影響を減らすために役立ちます。 ことができます。

IsolationLevel メタデータとコマンド ライン オプションとその意味で使用できる値を次に示します。

<span id="None"></span><span id="none"></span><span id="NONE"></span>[なし]  
TAEF には、すべてのテストは分離されていません。

<span id="Module"></span><span id="module"></span><span id="MODULE"></span>モジュール  
TAEF は DLL をテストごとに個別のプロセス ホストを使用します。 **これは、既定値です。**

<span id="Assembly"></span><span id="assembly"></span><span id="ASSEMBLY"></span>アセンブリ  
モジュールと同じ

<span id="DLL"></span><span id="dll"></span>DLL  
モジュールと同じ

<span id="Class"></span><span id="class"></span><span id="CLASS"></span>クラス  
TAEF は各テスト クラスの別のプロセス ホストを使用します。

<span id="Method"></span><span id="method"></span><span id="METHOD"></span>メソッド  
TAEF はテストごとに個別のプロセス ホストを使用します。 テストが実行グループ内にある場合は、実行全体のグループの同じプロセス ホストが使用されます。

<span id="Test"></span><span id="test"></span><span id="TEST"></span>テスト  
メソッドと同じ

使用される IsolationLevel メタデータ値は、テスト レベルに最も近い位置に指定されたメタデータです。 コマンド ライン IsolationLevel オプションを設定すると、使用される値は、ほとんどの分離を提供する 1 つが。

```cpp
BEGIN_MODULE()
    MODULE_PROPERTY(L"IsolationLevel", L"Class")
END_MODULE()

class MyTestClass1
{
    TEST_CLASS(MyTestClass1);

    BEGIN_TEST_METHOD(MyTest1)
        TEST_METHOD_PROPERTY(L"IsolationLevel", L"Method")
    END_TEST_METHOD()

    TEST_METHOD(MyTest2);
    TEST_METHOD(MyTest3);
};

class MyTestClass2
{
    TEST_CLASS(MyTestClass2);

    TEST_METHOD(MyTest1);
    TEST_METHOD(MyTest2);
};
```

上記の例では、3 つの異なるプロセス ホストが使用: MyTestClass1::MyTest1 に 1 つずつ、MyTestClass1 でその他の 2 つのメソッドのいずれかおよび MyTestClass2 のいずれか。 5 つの異なるプロセス ホスト/IsolationLevel:Method を te.exe のコマンドラインに追加する場合、ユーザーは、使用される。 テストごとに 1 つ。

モジュールの場合、クラス、またはテストが[メタデータ拡張](light-weight-data-driven-testing.md)または[データ ドリブン](data-driven-testing.md)と分離するのには、それぞれのメタデータ、またはデータの拡張は分離されています。 これによって、テストのメンバーにするテスト レベルに回避できる、[グループ実行](execution-groups.md)します。

```cpp
class MyTestClass3 :
{
    BEGIN_TEST_CLASS(MyTestClass3)
        TEST_CLASS_PROPERTY(L"Data:MyParameter1", L"{1, 2, 3}")
        TEST_CLASS_PROPERTY(L"IsolationLevel", L"Class")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTest1)
        TEST_METHOD_PROPERTY(L"Data:MyParameter2", L"{1, 2, 3}")
        TEST_METHOD_PROPERTY(L"IsolationLevel", L"Method")
        TEST_METHOD_PROPERTY(L"ExecutionGroup", L"MyExecutionGroup")
    END_TEST_METHOD()

    TEST_METHOD(MyTest2);
    TEST_METHOD(MyTest3);
};
```

この例では、6 つの異なるプロセス ホストが使用されます。 MyParameter1 の 3 つの値のそれぞれが分離と MyTest1 は MyTest2 と MyTest3 から分離されます。 MyParameter2 の 3 つの値は、同じグループの実行であるために分離されていません。

 

 





