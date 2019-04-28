---
title: C++ でテストを作成する
description: C++ でテストを作成する
ms.assetid: ECADDDD6-5BD4-4c43-803F-47AE44467342
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09279d214edab919394e26c6e4e1f541d3876dd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372775"
---
# <a name="authoring-tests-in-c"></a>C++ でテストを作成する


次のコード例では、ネイティブの C++ ファイル 1 つのテスト クラスが含まれ、2 つのテストのメソッドを示します。

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

**1 行目**、フレームワークに必要な 1 つのヘッダー ファイルを含む**WexTestClass.h**します。 含まれるヘッダー ファイルにも含まれています、 **Log.h**ロガーのファイルと**Verify.h**検証ケースを定義するためのファイル。 これらのヘッダー ファイルについては、後ほど説明します。

**行 3**テスト クラスを定義します。 **SimpleTests**します。 テスト クラスは、特別なクラスから継承する必要はありません。 また、その内容は、パブリックにする必要はありません。

**5 行目**テスト クラスとしてこのクラスを定義します。

**8 ~ 9 行目**クラス - で、2 つのテスト メソッドを宣言**FirstTest**と**SecondTest**します。 12 ~ 20 の行に定義されています。 **テスト\_メソッド**マクロは、必要なメソッドの宣言をクラスに追加します。 マーク アップでは、すべてのテストに同じプロトタイプが必要です。 返す必要がある**void**を得る必要がありますいないパラメーターとします。

クラス宣言内でインライン テストを定義する場合は、行うことができます"WexTestClass.h"中に含める限り**インライン\_テスト\_メソッド\_マークアップ**で定義されているが、プリプロセッサします。

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

**10 ~ 15 行**テスト メソッドの定義が含まれています。

**注**  だけを 1 つの cpp ファイルにそのヘッダー ファイルを含めることをお勧めするヘッダー ファイルをテスト クラスの宣言を配置した場合。 CPP ファイルの複数の結果に、テスト クラスの宣言を含むテスト DLL にコンパイルされる extratraneous データ。

 

## <a name="span-idadvancedauthoringtestsincspanspan-idadvancedauthoringtestsincspanspan-idadvancedauthoringtestsincspanadvanced-authoring-tests-in-c"></a><span id="Advanced_Authoring_Tests_in_C__"></span><span id="advanced_authoring_tests_in_c__"></span><span id="ADVANCED_AUTHORING_TESTS_IN_C__"></span>C++ での高度なオーサリング テスト


次の例では、セットアップおよび後処理用のメソッドを使用し、メタデータと共に、テスト クラスとテスト メソッドの宣言を宣言します。 この例では、1 つのクラスも含まれます (**MetadataAndFixturesTests**) の 2 つの方法をテストします。

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

**4 行**グローバル メタデータを一連のテスト バイナリをこのヘッダーのコンパイルに適用されるプロパティの宣言を開始します。

**5 行目**名前のプロパティを宣言する**機能**値**TAEF**します。 ありますより開始の間で 1 つのプロパティ.終了しています.マクロ。 ようなプロパティの宣言は、行 20 ~ 24 (クラス レベルのメタデータ)、45 ~ 47 (メソッド レベルのメタデータ)、および 52 54 (で定義されているテスト インライン レベルのメタデータ テスト) に存在します。

**45 47 ~ 60 ~ 63 行目**これらのテストを追加するためのマクロを示すメタデータもテスト メソッドを宣言します。 **50 57 行**デモンストレーションすることができますのメタデータを宣言および定義する場合でも同じ場所でテストします。

**8 行**モジュールのセットアップ関数の任意のモジュールのテスト クラスを作成する前に実行される関数を宣言します。

**13 行目**クラス クリーンアップ メソッドおよびデストラクター完了して、テストをすべて実行する関数 - モジュールのクリーンアップ関数を宣言します。 ただし、32、同様の設定と 24 の行にクラスのクリーンアップ メソッドがあります。 これらのメソッドは、クラス コンス トラクターとクラスのデストラクターをそれぞれ実行します。

**行 42 から 34**のテスト メソッドのような関数を宣言します。 テストのセットアップおよび後処理用のメソッドは、各テストが実行される前後を実行します。

TAEF セットアップおよび後処理用のメソッドは、ブール値を返すし、パラメーターを受け入れません。 戻り値は、特定のテストの単体テストを実行するかどうかをでも、フレームワークに通知します。 たとえば、クラスのセットアップ メソッドが失敗して、false を返します、フレームワークは、クラスのテスト メソッドは実行されません。

 

 





