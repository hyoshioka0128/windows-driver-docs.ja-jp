---
title: データ ドリブン テストを実行する
description: データ ドリブン テストを実行する
ms.assetid: E8E7A66A-6E39-442d-A195-AE4633B817FE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 745cc31388aa42be04e880c8e21e483d49b5a545
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378095"
---
# <a name="span-idtaefexecutingdata-driventestsspanexecuting-data-driven-tests"></a><span id="taef.executing_data-driven_tests"></span>データ ドリブン テストを実行します。


データ ドリブン テストを作成する方法と使用してテストを実行する方法を認識することを確認[TAEF](index.md)のヒントとテクニック DataDrivenTests TAEF での実行を開始する前にします。 方法上のメモリを更新すると便利[選択クエリ](selection.md)TAEF と同様に機能します。

このセクションでは、具体的には、ベース テーブルのデータ ドリブン テストの実行について説明がベース PICT に同じ基本原則を適用し、WMI ベースのデータ ドリブン テストにもします。

データ ドリブン テストを含むすべてのテストを実行する場合、方法は通常使用して実行する TAEF からの違いはありません。 実行中の例を考えてみましょう、 **CPP\\DataDrivenExample**と**CSharp\\DataDrivenExample** TAEF を使用しています。 既定で TAEF が実行されるテスト プロシージャの出力に注意してください。 Inproc に実行する場合を使用して、"/inproc"スイッチします。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll
```

Xml ファイルとメタデータを指定するヘッダー ファイルを見ておきます。 優先順位がデータ ドリブン テストを実行する次のように 1 を =。

``` syntax
TE.exe Examples\*.Tests.dll /select:"@DataSource=* And @Priority=1"
```

レベルのオーサリング TestMethod でメタデータが指定された xml ファイルの上書きに行レベルで指定されたメタデータを留意してください。

データ ドリブン テストの実行 TAEF の能力をもう少し見ていきましょう。 たとえば、する再現コード FirstTable() 関数の第 3 行のみです。 これは、2 (インデックスは 0 から開始) の行のインデックスを使用して行うことができます。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*FirstTable*' and @Data:index=2"
```

選択基準は、新しい名前空間をここでは"@Data:"データ ドリブン テストを具体的には使用できます。 上記のテストを実行すると表示になります、通常ではなく '\#インデックス' がある、データ ドリブン テストの場合、テスト名に付加する '\#黒' これは、指定された特殊な 'Name' メタデータ - テスト名に追加この行。 参照してください[行レベルのメタデータを指定する](metadata-overriding-data-driven-test-example.md)詳細についてはします。 この特別な名前に関係なく、名前を使用しても選択できます。 インデックスの選択は、非常に大きなデータ セットの行の範囲の選択的に移動できます。 たとえば (架空の例ではなく) データ ドリブン テストでは、100 行がある場合 (インデックスの最大 99) 10 より大きいインデックスを持つ行を実行して、20 未満、今すぐ簡単にこれを指定できますとして。

``` syntax
TE.exe Examples\*.Tests.dll /select:"@Name='*MyDataDrivenTest*' and @Data:index > 10 and @Data:index < 20"
```

多くの場合は、特定のデータ値に基づく再現コードをしてそのインデックスを検索する手間を経由する必要がありません。 ここで使用することができます、"@Data:"もう一度名前空間。 ネイティブ単体テストの例で言うようになりました (を参照してください[データ ドリブン テストをオーサリング](data-driven-testing.md))、「テーマ」が"AeroBasic"ケースのみを実行します。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll /select:"@Data:Theme='AeroBasic'"
```

次のようにコンソールに表示されます。

``` syntax
StartGroup: WEX::TestExecution::Examples::DataDrivenTests::SecondTable#2 [Process: 3588; Thread: 4584]
I am in second table.
Theme supplied as AeroBasic
EndGroup: WEX::TestExecution::Examples::DataDrivenTests::SecondTable#2 [Passed]
Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

データ ドリブン テスト データ セットとメタデータ (行レベル、テスト メソッドのレベルにある指定されたメタデータの組み合わせ) を表示するデータ ドリブン テストの/listproperties を活用することもできます。 だから

``` syntax
TE.exe Examples\CSharp.DataDriven.Examples.dll /listproperties
```

すべてのメソッドを一覧表示されます (データ ドリブンし、それ以外の場合)、メタデータとデータ値と共に使用できると指定したさまざまなレベルでします。

見て[、行レベルでメタデータをオーバーライド](metadata-overriding-data-driven-test-example.md)、[配列パラメーター型を指定する](array-support-data-driven-test-example.md)と[単純なデータに基づく例](data-driven-testing.md)などの詳細を提供するチュートリアル把握。

 

 





