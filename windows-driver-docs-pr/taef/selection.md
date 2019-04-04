---
title: 選択
description: 選択
ms.assetid: 5DFE5B52-4D58-491c-9363-95E4A2FD680C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c427c3fac66724743d68d6096cf0423eed5566
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579448"
---
# <a name="selection"></a>選択


テストの作成と実行フレームワーク (TAEF) は、選択的に実行または指定したメタデータ情報に基づいて特定のテストを省略するためのメカニズムを提供します。 次のセクションでは、TE.exe でこの選択メカニズムを使用する方法のさまざまな例について説明します。

コマンド プロンプト ウィンドウから TE.exe を行うことができます。

``` syntax
TE <test_binaries> [/select:<selection criteria>]
```

このセクションの説明、TE.exe**選択/:**<em>選択基準</em>オプション。 TE.exe の詳細については、[TE.exe コマンド オプション](te-exe-command-line-parameters.md)を参照してください。

選択基準は、コマンド プロンプトで説明したすべてのテスト バイナリをグローバルに適用されます。 2 つのテストについて考えてみましょう\_バイナリ。**例\\CPP します。SelectionCriteria1.Example.dll**と**例\\CPP します。SelectionCriteria2.Example.dll**します。 次の例は、プロパティ、またはこれらのテストでさまざまなレベルで指定されたメタデータ\_バイナリ。 指定することで取得することもできます、 **/listproperties**コマンド プロンプト ウィンドウでオプションです。

```cpp
CPP.SelectionCriteria1.Example.dll (Owner="C1", Priority=3)
class11 (Owner="C2")
method111(Priority=1)

method112 (BackwardsCompatibility="Windows 2000")
class12
method121
CPP.SelectionCriteria2.Example.dll (Owner="WEX")
class21 (Owner="C1", Priority=2, BackwardsCompatibility="Windows XP")
method211 (Owner="C2")
class22 (Owner="U3")
method221
```

つまり、これらの 1 つずつ/listproperties を使用してテスト\_バイナリとは別に、表示します。

``` syntax
F:\fsd1.binaries.x86chk\WexTest\C1\TestExecution>te Examples\CPP.SelectionCriteria1.Example.dll /listproperties
Test Authoring and Execution Framework v2.2 Build 6.1.7689.0 (release.091218-1251) for x86

F:\fsd1.binaries.x86chk\WexTest\C1\TestExecution\Examples\CPP.SelectionCriteria1.Example.dll
        Property[Owner] = C1
        Property[Priority] = 3
    WEX::TestExecution::Examples::Class11
            Property[Owner] = C2
        WEX::TestExecution::Examples::Class11::Method111
                Property[Priority] = 1
        WEX::TestExecution::Examples::Class11::Method112
                Property[BackwardsCompatibility] = Windows2000

    WEX::TestExecution::Examples::Class12
        WEX::TestExecution::Examples::Class12::Method121
```

および:

``` syntax
F:\fsd1.binaries.x86chk\WexTest\C1\TestExecution>te Examples\CPP.SelectionCriteria2.Example.dll /listproperties
Test Authoring and Execution Framework v2.2 Build 6.1.7689.0 (release.091218-1251) for x86

F:\fsd1.binaries.x86chk\WexTest\C1\TestExecution\Examples\CPP.SelectionCriteria2.Example.dll
        Property[Owner] = WEX
    WEX::TestExecution::Examples::Class21
            Property[BackwardsCompatibility] = Windows XP
            Property[Owner] = C1
            Property[Priority] = 2
        WEX::TestExecution::Examples::Class21::Method211
                Property[Owner] = C2

    WEX::TestExecution::Examples::Class22
            Property[Owner] = U3
        WEX::TestExecution::Examples::Class22::Method221
```

この時点でそのテストを確認することが重要\_のフル パスと共にバイナリが一覧表示され、クラス名として一覧表示されます"&lt;Namespace&gt;::&lt;ClassName&gt;"ネイティブのテストの場合\_バイナリと"&lt;Namespace&gt;.&lt;ClassName&gt;"管理対象のテストの場合\_バイナリ。 同様に、テスト メソッド名として一覧表示されます"&lt;Namespace&gt;::&lt;ClassName&gt;::&lt;TestMethodName&gt;"の場合はネイティブのテスト\_バイナリと"&lt;Namespace&gt;.&lt;ClassName&gt;.&lt;TestMethodName&gt;"管理対象のテストの場合\_バイナリ。

つまり、任意の名前または関数の完全修飾名は、te で保存されている内容にします。 これは、任意のメソッドを一意に識別できるようにするのには。 例 2 つのクラスは、同じメソッド名、クラスの修飾がやすくを一意にいる場合は選択をしているメソッドでは、その関心があります。 この選択基準は、特定のテスト条件に一致するテストのみを実行するのに役立ちます。\_バイナリ。

上記の例では、例で言う\\Cpp.SelectionCriteria1.Example.dll、次の選択条件のいずれかで"Method111"を選択することができます。

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll /select:"@Name='WEX::TestExecution::Examples::Class11::Method111'"
```

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll /select:"@Name='*Class11::Method111'"
```

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll /select:"@Name='*Method111'"
```

実行して"Priority"2 未満でマークされているすべてのテストを実行することができます。

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /select:"@Priority < 2"
```

これは、例のみを実行するは\\CPP します。SelectionCriteria1.Example.dll - この例では、"class11::method111"。

Class11 ですべてのテストを実行する場合は、次のように選択するワイルドカードのマッチングと修飾"Name"プロパティを使用できます。

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll
                                                               /select:"@Name='*::class11::*'"
```

選択条件を使用する場合は、点に留意すると便利ですがあります。

-   "**と**「,」**いない**"、および"**または**"は**予約**単語とは**大文字と小文字を区別しない**。
-   **メタデータのプロパティ名と値は大文字と小文字を区別しない**例では、"C2"の例は、"c2"と"C2"と一致します。 そのため場合"property"メタデータを持つ 1 つの関数があるし、"Property"と、選択条件を使用した異なるは"PROPERTY"を探してと一致することがこれらの両方。
-   **選択範囲のクエリ文字列内の文字列値は、単一引用符に含める必要があります。選択クエリ内の文字列値内で"?"は 1 つのワイルドカード文字と"\*"が 0 またはワイルドカード文字。**
-   コマンド プロンプトで引用符の使用中に**選択クエリをコピーする場合の引用符に注意してください**します。 Outlook 電子メールから選択クエリをコピーする場合、引用符を必要に応じて誤ってと TAEF がそれを解析することがない可能性があります。 代わりに、引用符を入力します。

複合的な選択条件がどのような実行の簡単な例をいくつか見てみましょう。

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='C2' AND @Priority=2"
```

実行されます。

-   例\\CPP します。SelectionCriteria2.Example.dll - class21::method211

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='C2' AND @Priority=3"
```

実行されます。

-   例\\CPP します。SelectionCriteria1.Example.dll - class11::method112

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='U3' oR @Priority=1"
```

実行されます。

-   例\\CPP します。SelectionCriteria1.Example.dll - class11::method111
-   例\\CPP します。SelectionCriteria2.Example.dll - class22::method221

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"not(@BackwardsCompatibility=*)"
```

実行のすべてのテスト BackwardsCompatibility 値が指定されません。 (詳しくは、次の項目を参照してください)。

-   例\\CPP します。SelectionCriteria1.Example.dll - class11::method111、class12::method121
-   例\\CPP します。SelectionCriteria2.Example.dll - class22::method221

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='C*'"
```

実行のすべてのテストの所有者の値の開始位置に"C"(大文字と小文字は区別されません)。 前のコマンド例ではすべてのテストを実行できるため、\\CPP します。SelectionCriteria1.Example.dll とすべてのテストの例に\\CPP します。Class21 SelectionCriteria2.Example.dll (つまり、method211)

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"not(@BackwardsCompatibility=*) OR (@Owner='C*' AND @BackwardsCompatibility='*XP*')"
```

すべてのテスト場所か、BackwardsCompatibility が指定されていないか、所有者名が"C"で始まるし、backwardsCompatibilty 値を格納 XP が実行されます。 注方法かっこ「("および」)"の優先順位の順序を指定するために使用します。

例では、これは選択的に実行します。

-   例\\CPP します。SelectionCriteria1.Example.dll - class11::method111、class12::method121、
-   例\\CPP します。SelectionCriteria2.Example.dll - class21::method211、class22::method221

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /select:"@Owner='???'"
```

3 個の文字を含むプロパティの所有者の値を持つテストのみ実行されます。

例では、"C"と一致し、実行時にだけこれは。

-   例\\CPP します。SelectionCriteria1.Example.dll - class12::method121

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /select:"@Priority>=1"
```

注: これを使用する方法の良い例は、"&gt;=「,」&lt;=「,」&gt;「と」&lt;"propertyvalues が floatvalues をされます。

この例では、例を除くすべてのメソッドを実行この\\CPP します。SelectionCriteria2.Example.dll - class22::method221、場所 prority が指定されていません。 つまり、これは実行します。

-   例\\CPP します。SelectionCriteria1.Example.dll - class11::method111、class11::method112、class12::method121
-   例\\CPP します。SelectionCriteria2.Example.dll - class21::method211 します。

使用して、「/選択」ことができますので注意が他のコマンドのようなオプション「/を一覧表示」"/list プロパティ"など。

## <a name="span-idsmartquotesspanspan-idsmartquotesspanspan-idsmartquotesspansmart-quotes"></a><span id="Smart_Quotes"></span><span id="smart_quotes"></span><span id="SMART_QUOTES"></span>スマート クォート


コピーする場合の選択条件を Outlook または Word ドキュメントから経由でコマンド プロンプトには、選択基準での引用符があります。 どのようなスマート クォートの詳細についてを見つけることができます:<http://en.wikipedia.org/wiki/Smart_quotes>と[スマート引用符。コンピューターの消費するためのもののテキストの非表示の災禍](https://blogs.msdn.microsoft.com/oldnewthing/20090225-00/?p=19033/)

スマート クォートを回避する簡単な方法はありません - 最良のアプローチがすべて削除するには、"二重引用符と ' コピー経由でコマンド プロンプトにして、クエリの見積もりの一部を再入力した後の単一引用符の選択基準。

Outlook でメッセージを作成するときに、それらをオフにする設定、オプションがあります。 これを特定する Outlook ヘルプのボックスに「スマート クォート」を入力します。

## <a name="span-idquicknamebasedselectionspanspan-idquicknamebasedselectionspanspan-idquicknamebasedselectionspanquick-name-based-selection"></a><span id="Quick_Name_based_selection"></span><span id="quick_name_based_selection"></span><span id="QUICK_NAME_BASED_SELECTION"></span>クイック ベース名の選択


TAEF は、'/name' コマンド ライン パラメーターを使用してコマンド プロンプトでの名前に基づく簡単な選択を使用できます。

``` syntax
/name:<test name with wildcards>
```

等価です。

``` syntax
/select:@Name='<test name with wildcards>'
```

つまりなどの名前に基づいて選択クエリを指定することができますようになりました。

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Name='*::class11::*'"
```

使用してより迅速に **/name**ようになります。

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /name=*::class11::*
```

場合は、両方 **/name**と**選択/** /name は無視され、リンクを優先し、コマンド プロンプトで提供されます。

 

 





