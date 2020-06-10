---
title: C++ でテストを作成する
description: C++ でテストを作成する
ms.assetid: ECADDDD6-5BD4-4c43-803F-47AE44467342
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdef10d80c0a251f870749cf8fc20698a9c2eba3
ms.sourcegitcommit: 546cc69e970e16f4e226c189da54c4fe012ae855
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84629730"
---
# <a name="authoring-tests-in-c"></a>C++ でテストを作成する


次のコード例は、2つのテストメソッドを含む単一のテストクラスを含むネイティブ C++ ファイルを示しています。

```cpp
1   #include "WexTestClass.h"
2
3   class SimpleTests   {
4      // Declare this class as a TestClass, and supply metadata if necessary.
5      TEST_CLASS(SimpleTests);
6
7      // Declare the tests within this class.
8      TEST_METHOD(FirstTest);
9      TEST_METHOD(SecondTest);
10  };
11
12  void SimpleTests::FirstTest()
13  {
14      VERIFY_ARE_EQUAL(1, 1);
15  }
16
17  void SimpleTests::SecondTest()
18  {
19      VERIFY_IS_TRUE(true);
20  }
```

**行 1**には、フレームワークの WexTestClass に必要な1つのヘッダーファイルが含まれてい**ます。** このファイルは、 **% \ Program Files (x86) \windows Kits\10\Testing\Development\inc**にあります。インクルードされるヘッダーファイルには、ロガーの**ログ .h**ファイルと、検証ケースを定義するための **.h**ファイルも含まれています。 これらのヘッダーファイルについては後で説明します。

**3 行目**では、テストクラスである**simpletests**を定義します。 テストクラスは、特別なクラスから継承する必要はありません。 また、そのコンテンツはパブリックである必要はありません。

**行 5**は、このクラスをテストクラスとして定義します。

**行8と 9**は、クラス**firsttest**と2つのテストメソッドを**宣言して**います。 これらは12行目から20行目に定義されています。 **テスト \_ メソッド**マクロは、必要なメソッド宣言をクラスに追加します。 このマークアップスキームでは、すべてのテストのプロトタイプが同じである必要があります。 これらは**void**を返す必要があり、パラメーターを受け取る必要はありません。

クラス宣言内でテストをインラインで定義する場合は、プリプロセッサで**インライン \_ テスト \_ メソッド \_ マークアップ**が定義されている間は、"WexTestClass" をインクルードする必要があります。

```cpp
1   #define INLINE_TEST_METHOD_MARKUP
2   #include "WexTestClass.h"
3
4   class InlineTests
5   {
6       TEST_CLASS(InlineTests);
7 
8       TEST_METHOD(FirstTest)
9       {
10          VERIFY_ARE_EQUAL(1, 1);
11      }
12
13      TEST_METHOD(SecondTest)
14      {
15          VERIFY_IS_TRUE(true);
16      }
17  };
```

**行10および 15**には、テストメソッドの定義が含まれるようになりました。

**メモ**   テストクラスの宣言をヘッダーファイルに配置する場合は、そのヘッダーファイルを1つの cpp ファイルにのみ含めることをお勧めします。 テストクラスの宣言を複数の CPP ファイルに含めると、extratraneous データがテスト DLL にコンパイルされます。

 

## <a name="span-idadvanced_authoring_tests_in_c__spanspan-idadvanced_authoring_tests_in_c__spanspan-idadvanced_authoring_tests_in_c__spanadvanced-authoring-tests-in-c"></a><span id="Advanced_Authoring_Tests_in_C__"></span><span id="advanced_authoring_tests_in_c__"></span><span id="ADVANCED_AUTHORING_TESTS_IN_C__"></span>C++ での高度な作成テスト


次の例では、セットアップメソッドとクリーンアップメソッドを使用して、テストクラスとテストメソッドの宣言と共にメタデータを宣言します。 この例には、2つのテストメソッドを含む単一のクラス (**Metadataandfixturestests**) も含まれています。

```cpp
 1  #define INLINE_TEST_METHOD_MARKUP
 2  #include "WexTestClass.h"
 3
 4  BEGIN_MODULE()
 5      MODULE_PROPERTY(L"Feature", L"TAEF")
 6  END_MODULE()
 7
 8  MODULE_SETUP(ModuleSetup)
 9  {
10      return true;
11  }
12
13  MODULE_CLEANUP(ModuleCleanup)
14  {
15      return true;
16  }
17
18  class MetadataAndFixturesTests
19  {
20      BEGIN_TEST_CLASS(MetadataAndFixturesTests)
21          TEST_CLASS_PROPERTY(L"Component", L"Verify")
22      END_TEST_CLASS()
23
24      TEST_CLASS_SETUP(ClassSetup)
25      {
26          return true;
27      }
28
29      TEST_CLASS_CLEANUP(ClassCleanup)
30      {
31          return true;
32      }
33
34      TEST_METHOD_SETUP(TestSetup)
35      {
36          return true;
37      }
38
39      TEST_METHOD_CLEANUP(TestCleanup)
40      {
41          return true;
42      }
43
44      // If you use this syntax, you will have to define the test outside of the test class.
45      BEGIN_TEST_METHOD(FirstTest)
46          TEST_METHOD_PROPERTY(L"Owner", L"Contoso")
47      END_TEST_METHOD()
48
49      // You can still have metadata even if you define your test inside the test class.
50      TEST_METHOD(SecondTest)
51      {
52          BEGIN_TEST_METHOD_PROPERTIES()
53              TEST_METHOD_PROPERTY(L"Owner", L"Contoso")
54          END_TEST_METHOD_PROPERTIES()
55
56          VERIFY_IS_TRUE(true);
57      }
58  };
59
60  void MetadataAndFixturesTests::FirstTest()
61  {
62      VERIFY_ARE_EQUAL(1, 1);
63  }
```

**4 行目**では、グローバルメタデータの宣言を開始します。これは、このヘッダーがコンパイルされるテストバイナリに適用される一連のプロパティです。

**行 5**では、name**機能**と値**taef**を使用してプロパティを宣言します。 BEGIN... の間には、1つ以上のプロパティがあります。終了...マクロ. 同様のプロパティ宣言は、20-24 行 (クラスレベルのメタデータ)、45-47 (メソッドレベルのメタデータ)、および 52-54 (定義されているテストのテストレベルのメタデータ) に存在します。

**行 45-47 と60– 63**では、メタデータを追加するためのこれらのテストマクロもテストメソッドを宣言しています。 **行 50-57**は、同じ場所でテストを宣言して定義する場合でもメタデータを保持できることを示しています。

**8 行目**では、モジュールのセットアップ関数 (モジュールのテストクラスの作成前に実行される関数) を宣言します。

**行 13**は、すべてのテストとクラスのクリーンアップメソッドおよびデストラクターが終了した後に実行される関数であるモジュールクリーンアップ関数を宣言します。 24時間32の場合、クラスには同様のセットアップメソッドとクリーンアップメソッドがあります。 これらのメソッドは、クラスコンストラクターの後、クラスのデストラクターの前に実行されます。

**行 34 ~ 42**は、テストメソッドに類似した関数を宣言します。 テストのセットアップメソッドとクリーンアップメソッドは、各テストの実行の前後に実行されます。

TAEF のセットアップメソッドとクリーンアップメソッドは、ブール値を返し、パラメーターを受け入れません。 戻り値は、特定のテスト単位のテストの実行を継続できるかどうかをフレームワークに通知します。 たとえば、クラスのセットアップメソッドでエラーが発生し、false が返された場合、フレームワークはクラスのテストメソッドを実行しません。

 

 





