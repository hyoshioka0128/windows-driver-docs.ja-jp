---
title: データ ドリブン テスト
description: データ ドリブン テスト
ms.assetid: 409CC5FD-1632-4120-95C6-60574C9BAD32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18a48f8cccf8b59cfc499518f75ac46d4d4cff2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574904"
---
# <a name="data-driven-testing"></a>データ ドリブン テスト


データ ドリブン テストは、コードからテストの入力と出力値が区切られているテストの方法です。 この形式をテスト_ケースの数が多い単純に関連するデータを識別することによって書き込まれるため、もう少しより汎用的なテスト コードのために少し投資すれば通常意味します。

その動作を定義する入力値のセットを使用する領域をテストするための優れたデータ ドリブン テストは - たとえば、API をテストするには、入力と出力パラメーターは、データのソースとして定義でき、テスト コードは、データを使用、により、API を呼び出すし、結果を検証します。

## <a name="span-iddata-driventestingsupportintaefspanspan-iddata-driventestingsupportintaefspanspan-iddata-driventestingsupportintaefspandata-driven-testing-support-in-taef"></a><span id="Data-driven_Testing_support_in_TAEF"></span><span id="data-driven_testing_support_in_taef"></span><span id="DATA-DRIVEN_TESTING_SUPPORT_IN_TAEF"></span>TAEF でデータ ドリブン テストのサポート


TAEF はさまざまなデータ ドリブン テストを作成するためのオプションを提供します。 テストのシナリオに最も適したものを選択できるように、これらのオプションを理解しましょう。

**テーブル ベースのテスト データに基づく**微調整するデータのパラメーターのバリエーションで制御された粒度し、パラメーターの型を定義するソリューションを使用できます。 この場合、データ ソースは、XML ファイルで定義されているテーブルです。 パラメーターの型を指定することができます (int、unsigned int、サイズ\_t、bool、double、DWORD、 \_ \_int64 などと同種の配列がバリアント)、または WEX::Common::String (ネイティブ) を型の既定値や文字列 (マネージ)。 テーブル内の各行は、パラメーター値のバリエーションの 1 つのセットです。 テスト メソッドは、テーブル内のすべての行の再呼び出しになります。 次のテーブル ベースのデータ ドリブン テストでの XML データ ソースのスニペットに示します。

```cpp
1  <?xml version="1.0"?>
2   <Data>
3     <Table Id ="Table1">
4          <ParameterTypes>
5                  <ParameterType Name="Size">Int32</ParameterType>
6                  <ParameterType Name="Color">String</ParameterType>
7          </ParameterTypes>
8          <Row>
9                 <Parameter Name="Size">12</Parameter>
10                 <Parameter Name="Color">Blue</Parameter>
11         </Row>
12         <Row>
13                 <Parameter Name="Size">4</Parameter>
14                 <Parameter Name="Color">White</Parameter>
15         </Row>
16         <Row>
17                 <Parameter Name="Size">9</Parameter>
18                 <Parameter Name="Color">Black</Parameter>
19         </Row>
20    </Table>
21  </Data>
```

詳細については。[テーブル ベースのテスト データに基づく](table-data-source.md)します。

**軽量データ ドリブン テスト**テーブルがデータ ドリブン テスト ソリューションに基づいている完全な忠実度は、サポートを提供しません。 : を明確にするにはWEX::Common::String(native) するデータのパラメーターを制限軽量データ ドリブン テストまたはテーブルでサポートされるさまざまな型ではなく、String(managed) ベースのデータ駆動テスト ソリューションです。 しようとする (たとえば 1 つまたは 2 つのパラメーターの) データを低コストで簡単なバリエーションの 1 つのデータ ドリブン テスト メソッドを作成し、でした苦労する価値あるデータ ソースが表示される、XML ファイルを追加する、軽量データ ドリブン テストである正確にどのような場合は探しています。 好例です API say OpenThemeData(...) の単体テストを記述する開発者は、"Button"、"Listbox"および"ScrollBar"に対して API を確認したいとします。 ありますこれは、XML データ ソース ファイルを作成するオーバー ロードが多すぎるが、軽量データ ドリブン テストのサポートとそのでした効率的にソース コード自体にします。 1 つ以上のパラメーターが指定されている場合は、TAEF には、シーンの背後にあるパラメーターの組み合わせ n 方向拡張が生成され、組み合わせごとに、テスト メソッドが呼び出されます。 詳細については。[軽量データ ドリブン テスト](light-weight-data-driven-testing.md)します。

複雑な n 方法の組み合わせ拡張こと light データ ドリブン テスト プランの重み、でした高価なを取得し、逆効果として指定テスト シナリオを取得します。 このような複雑なテスト シナリオでは、によって提供される独立した組み合わせ Testing(PICT) ペアワイズ**PICT ベースのテスト データに基づく**お探しソリューションがあります。 PICT は、パラメーターより包括的なカバレッジを取得するパラメーターの結果のコンパクトなセットを生成することによって、多くの価値を提供します。 PICT およびでこのソリューションを使用する方法の詳細へのリンクを見つける[PICT ベースのテスト データに基づく](pict-data-source.md)ソリューション。

使用して、 **WMI ベースのテスト データに基づく**サポートを追加することも前提条件をテスト コンピューターで使用可能なリソースに基づいて情報 (データ) を取得およびテストにします。 など、マシンがある場合にのみ、テストを実行する場合は、ドメイン参加して、テストを実行するときにも、ドメイン名の情報が必要です。 データ ソースには、WQL クエリをここでは。 詳細を活用する方法については[WMI ベースのテスト データに基づく](wmi-data-source.md)テスト シナリオで。

上に示したすべてのオプションを考慮する、する可能性がありますもを思い付くに合わせてデザイン上のオプションの組み合わせが見えることがあります。 たとえば、WMI クエリを使用して、テスト マシンに接続されているすべてのプリンターに関する情報を取得したい場合がありますが、事前ベース テーブルのデータ ドリブン テスト コンストラクトを使用して定義するパラメーターのもう 1 つのセットがあります。 **複数の DataSource**仕様がテーブルごとにその他のテストの間で再利用可能なを許可するため、テストのデータを 2 つの別個のテーブルから取得する場合に役立ちます。 また場合があります。 テストの複数のデータ ソースを指定する方法、および制約の適用を行うときに詳細を確認するには。[複数のデータ ソースを指定します。](multiple-datasources.md)

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [スクリプト言語でデータ ドリブン テスト](data-driven-testing-in-scripting-languages.md)
-   [テーブルのデータ ソース](table-data-source.md)
-   [パラメーター テーブルのデータ ソースの型](parameter-types-in-table-data-sources.md)
-   [単純なデータ ドリブン テストの例](simple-data-driven-test-example.md)
-   [メタデータがデータ ドリブン テストの例をオーバーライドします。](metadata-overriding-data-driven-test-example.md)
-   [配列のサポート データ ドリブン テストの例](array-support-data-driven-test-example.md)
-   [データ ドリブン クラス](data-driven-class.md)
-   [PICT データ ソース](pict-data-source.md)
-   [WMI データ ソース](wmi-data-source.md)
-   [軽量データ ドリブン テスト](light-weight-data-driven-testing.md)
-   [データ ドリブン テストを実行します。](executing-data-driven-tests.md)
-   [複数のデータソース](multiple-datasources.md)

 

 





