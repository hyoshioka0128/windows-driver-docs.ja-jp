---
title: スレッド モデル
description: スレッド モデル
ms.assetid: 3BB0C01B-D82B-45dd-8AC8-EA2E2811CD24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 606f9b78d54a8cda3f6c02ae0eaef99967b25220
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348350"
---
# <a name="threading-models"></a>スレッド モデル


TAEF 機能を提供する COM の構成済みのスレッド モデルをテストする環境を実行します。 既定では、マネージ ©\#) と STA スレッドで実行されるテスト スクリプトの実行、ネイティブのスレッド モデル事前に構成されていません。

"ThreadingModel"メタデータ プロパティは、要求スレッド処理モデルに使用されます。 このプロパティの値を指定できます。

| プロパティ値 | 説明                                                                               |
|----------------|-------------------------------------------------------------------------------------------|
| STA            | シングル スレッド アパートメント (COINIT CoInitializeEx を呼び出すと\_APARTMENTTHREADED フラグ)。 |
| MTA            | マルチ スレッド アパートメント (COINIT CoInitializeEx を呼び出すと\_マルチ スレッドのフラグ)。       |
| なし           | スレッド モデルが指定されていません。                                                         |

 

## <a name="span-idconfiguringathreadingmodelspanspan-idconfiguringathreadingmodelspanspan-idconfiguringathreadingmodelspanconfiguring-a-threading-model"></a><span id="Configuring_a_threading_model"></span><span id="configuring_a_threading_model"></span><span id="CONFIGURING_A_THREADING_MODEL"></span>スレッド処理モデルの構成


以下に例を示します。MTA スレッド C++ マークアップからモデルを要求するには。

```cpp
class ThreadModelTests
{

    TEST_CLASS(ThreadModelTests);

    BEGIN_TEST_METHOD(MTAThreadingModelTest)
        TEST_METHOD_PROPERTY(L"ThreadingModel", L"STA")
    END_TEST_METHOD()
};
```

クラスまたはモジュールのスレッド処理モデルのプロパティを要求することもできます。 以下に例を示します。

```cpp
class ThreadModelTestsWithMTADefault
{

    BEGIN_TEST_CLASS(ThreadModelTestsWithMTADefault)
        TEST_CLASS_PROPERTY(L"ThreadingModel", L"Mta")
    END_TEST_CLASS()

    TEST_METHOD(DefaultWithMTASetByClass);
};
```

同様に、管理対象のテストのスレッド モデルを要求することもできます。

```cpp
[TestClass]

public class SimpleTests
{
    [TestMethod]
    [TestProperty("ThreadingModel", "MTA")]
    public void Test1()
    {
        Verify.IsTrue(true);
    }

    [TestMethod]
    [TestProperty("ThreadingModel", "STA")]
    public void Test2()
    {
        Verify.IsTrue(true);
    }

    [TestMethod]
    [TestProperty("ThreadingModel", "{STA; MTA}")]
    public void SetsOfMetadataTest()
    {
        Log.Comment("In CSharpThreadingModelExample.SetsOfMetadataTest");
        DisplayAppartmentState();
    }
}
```

上記の前回のテストに注意してください。SetsOfMetadataTest もメタデータのセットの使用し、同じテストを実行させることは不可能: STA スレッド モデルから開始し、MTA とします。

 

 





