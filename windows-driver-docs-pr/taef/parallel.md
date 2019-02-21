---
title: Parallel
description: Parallel
ms.assetid: E2AF7B3A-B614-4fe1-9CFB-0860F68E895C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f3579444172825987cbde409823b564f3a8725d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529398"
---
# <a name="parallel"></a>Parallel


TAEF では、複数のプロセッサ間でテストを並列に実行するためのメカニズムを提供します。

## <a name="span-idparallelismguaranteesspanspan-idparallelismguaranteesspanspan-idparallelismguaranteesspanparallelism-guarantees"></a><span id="Parallelism_Guarantees"></span><span id="parallelism_guarantees"></span><span id="PARALLELISM_GUARANTEES"></span>並列処理の保証


-   2 つにテスト[並列化可能としてマークされている](#markingtestsasparallelizable)は同時に実行できることです。
-   並列テストは、その他の並列と並列でないテストの両方と同時実行できます。
-   すべてのモジュール/クラス/テストのセットアップとクリーンアップは実行直線的に同じプロセス内で関連するテストの前後に。
-   モジュール/クラスのセットアップは、モジュールまたはクラスに少なくとも 1 つの並列テストが含まれている場合、異なるプロセスで並列に実行可能性があります。
-   並列実行モードと互換性がない、 [ **"/inproc"** ](executing-tests.md)実行メカニズム。

## <a name="span-idmarkingtestsasparallelizablespanspan-idmarkingtestsasparallelizablespanspan-idmarkingtestsasparallelizablespanmarking-tests-as-parallelizable"></a><span id="MarkingTestsAsParallelizable"></span><span id="markingtestsasparallelizable"></span><span id="MARKINGTESTSASPARALLELIZABLE"></span>テストを並列化可能としてマークします。


例 (ネイティブ コード):

```cpp
class MyTests
{

    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(ParallelTest)
        TEST_METHOD_PROPERTY(L"Parallel", L"true")
    END_TEST_METHOD()
};
```

TAEF で一般的なその他のメタデータと同様はこのクラスまたはモジュール レベルで指定することができます &、そのクラスまたはモジュール内に含まれるすべてのテストによって継承されます。 たとえば、アセンブリ全体を並列化可能としてマークすることが以下を実行できます (外側のクラスまたはテストの仕様) cpp ファイルで、テスト DLL にコンパイルします。

```cpp
BEGIN_MODULE()
    MODULE_PROPERTY(L"Parallel", L"true");
END_MODULE()
```

このより広いスコープは、次のように、特定のテスト_ケースまたはクラスの並列処理を無効にするより小さなスコープでオーバーライドされた次できます。

```cpp
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(NonParallelTest)
        TEST_METHOD_PROPERTY(L"Parallel", L"false");
    END_TEST_METHOD()
};
```

どちらの設定は、テスト メソッドに最も近い (メソッドのメタデータは、最も近い、モジュール、クラス) と並行して他のテストでこのテストを実行するかどうかを決定するために使用されます。

## <a name="span-idenablingparallelismatthecommandlinespanspan-idenablingparallelismatthecommandlinespanspan-idenablingparallelismatthecommandlinespanenabling-parallelism-at-the-command-prompt"></a><span id="EnablingParallelismAtTheCommandLine"></span><span id="enablingparallelismatthecommandline"></span><span id="ENABLINGPARALLELISMATTHECOMMANDLINE"></span>コマンド プロンプトでの並列処理を有効にします。


並列実行は、オプトイン機能です。 テストは、並列としてマークする、TAEF は引き続き、コマンド プロンプトで並列実行モードが有効にしない限り、直線的にテストを実行します。

``` syntax
te unittests\* /parallel
```

 

 





