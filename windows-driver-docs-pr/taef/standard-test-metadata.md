---
title: 標準的なテスト メタデータ
description: 標準的なテスト メタデータ
ms.assetid: A95FC176-B3A1-4bbf-833E-411CDE73C571
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e951d50c37e5dbe21fc741bc5ca7937cea40d15
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372992"
---
# <a name="standard-test-metadata"></a>標準的なテスト メタデータ


次のテスト 'マーク アップ' のメタデータは TAEF テストに適用できる標準のメタデータです。

## <a name="span-idimplicitmetadataspanspan-idimplicitmetadataspanspan-idimplicitmetadataspanimplicit-metadata"></a><span id="Implicit_Metadata"></span><span id="implicit_metadata"></span><span id="IMPLICIT_METADATA"></span>暗黙的なメタデータ


メタデータの特定の情報は、テストのマークアップから自動的に推論されます。

-   「名前」- テストの完全修飾名。
-   「アーキテクチャ」- DLL のプロセッサ アーキテクチャ。 この値は 'x86'、'x64' または 'arm' のいずれかになります。
-   "TestFile"- DLL のファイルで説明した、テストします。

## <a name="span-idselectionmetadataspanspan-idselectionmetadataspanspan-idselectionmetadataspanselection-metadata"></a><span id="Selection_Metadata"></span><span id="selection_metadata"></span><span id="SELECTION_METADATA"></span>選択範囲のメタデータ


選択範囲のメタデータは、単に '任意' の各チームを強化できるようにする、標準のように、メタデータは、いずれかに別のテストを使用します。 必要なメタデータがありません - メタデータの義務の自動化、コストが増加し、すべてのメタデータは、省略可能にする必要がありますまたは 'オプトイン' 動作を有効にする必要があります。

メタデータの値を複数の値を指定することができる場合、場合に、セミコロン区切りの一覧を使用してテストするために 'contains' のスタイルの選択クエリを使用する必要があります、。 たとえば、「所有者」のメタデータは、2 つの値を必要とする場合にする必要があります設定する"Someone; をSomeoneElse"。 だれかによってのみ所有されているテストを選択するクエリは次のようになります。

``` syntax
te Wex.Common.Tests.dll /select:@Owner='Someone'
```

一方、次のクエリは、所有または共同のユーザーが所有されているテストを選択します。

``` syntax
te Wex.Common.Tests.dll /select:@Owner='*Someone*'
```

自分の会社内で使用する独自のメタデータを定義できます。 次の推奨事項は、推奨事項を示します。 .

## <a name="span-idyoushouldmetadataspanspan-idyoushouldmetadataspanspan-idyoushouldmetadataspanyou-should-metadata"></a><span id="_You_should...__Metadata"></span><span id="_you_should...__metadata"></span><span id="_YOU_SHOULD...__METADATA"></span>「する必要があります...」メタデータ


これらのメタデータ プロパティの推奨事項は、明確な意味があります。 必要に応じて、これらのメタデータ プロパティを使用します。

<span id="_ActivationContext_"></span><span id="_activationcontext_"></span><span id="_ACTIVATIONCONTEXT_"></span>"ActivationContext"  
システムでは、さまざまなサイド バイ サイド アセンブリからのバイナリの特定のバージョンを指定します。 参照してください[アクティベーション コンテキスト](activation-context.md)詳細についてはします。

<span id="_BinaryUnderTest_"></span><span id="_binaryundertest_"></span><span id="_BINARYUNDERTEST_"></span>"BinaryUnderTest"  
指定されたテスト バイナリ\[単位\]テストします。 これにより、開発者は特定の DLL を確認します。 すべての単体テストをすばやく実行できます。

<span id="_DefaultTestResult_"></span><span id="_defaulttestresult_"></span><span id="_DEFAULTTESTRESULT_"></span>"DefaultTestResult"  
指定されたテストの「合格」の既定のテスト結果をオーバーライドします。 テストが成功した場合、ログに記録された結果は既定のテスト結果になります。 指定できる値は、「成功」、"Failed"、"NotRun"、「ブロック」、"Skipped"には。

<span id="_DeploymentItem_"></span><span id="_deploymentitem_"></span><span id="_DEPLOYMENTITEM_"></span>["DeploymentItem"](deploymentitem-metadata.md)  
テストの依存関係としてファイルとフォルダーを識別します。

<span id="_Description_"></span><span id="_description_"></span><span id="_DESCRIPTION_"></span>"Description"  
テストの実行内容の短い説明です。

<span id="_DpiAware_"></span><span id="_dpiaware_"></span><span id="_DPIAWARE_"></span>"DpiAware"  
"True"に TAEF セットは、DPI 対応としてマークされているプロセスでテストを実行するがと、を参照してください。[高 DPI](https://docs.microsoft.com/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)します。

<span id="_ExecutionGroup_"></span><span id="_executiongroup_"></span><span id="_EXECUTIONGROUP_"></span>"ExecutionGroup"  
一連の連続するテストの順序で実行する必要がある場合、グループの実行の前のテストがブロックされますクラス内が実行されないと、失敗します。 参照してください[実行グループ](execution-groups.md)詳細についてはします。

<span id="_Ignore_"></span><span id="_ignore_"></span><span id="_IGNORE_"></span>"Ignore"  
クラスまたはテスト メソッドの実行中にスキップは"true"に「無視」メタデータの設定をテストまたは TAEF によって一覧表示します。 この動作をオーバーライドし、実行または「無視」のメタデータを持つものを含むすべてのテストを一覧表示するには指定 **/runIgnoredTests**コマンドライン引数として。

<span id="_IsolationLevel_"></span><span id="_isolationlevel_"></span><span id="_ISOLATIONLEVEL_"></span>"IsolationLevel"  
最小 TAEF テストを実行するときに使用する分離レベルを指定します。 参照してください[テストの分離](test-isolation.md)の詳細。

<span id="_Parallel_"></span><span id="_parallel_"></span><span id="_PARALLEL_"></span>["Parallel"](parallel.md)  
複数のプロセッサ全体には、並列でテストを実行します。 詳細については、次を参照してください。[並列](parallel.md)します。

<span id="_Priority_"></span><span id="_priority_"></span><span id="_PRIORITY_"></span>"Priority"  
小さい整数として、テストの優先順位は、優先度の高いです。

<span id="_RebootPossible_"></span><span id="_rebootpossible_"></span><span id="_REBOOTPOSSIBLE_"></span>["RebootPossible"](reboot.md)  
設定した場合は true、有効 TAEF コンピューターの再起動を実施するか、間もなくのテストが開始した再起動 TAEF に通知を要求する再起動の Api を使用します。

<span id="_RunAs_"></span><span id="_runas_"></span><span id="_RUNAS_"></span>"RunAs"  
問題のテストを実行する必要がありますコンテキストを指定します。 参照してください[RunAs 実行](runas.md)詳細についてはします。

<span id="_RunFixtureAs_"></span><span id="_runfixtureas_"></span><span id="_RUNFIXTUREAS_"></span>["RunFixtureAs"](runfixtureas.md)  
問題のテスト フィクスチャを実行する必要がありますコンテキストを指定します。 参照してください[RunFixtureAs](runfixtureas.md)詳細についてはします。

<span id="_TestClassification_Scope_"></span><span id="_testclassification_scope_"></span><span id="_TESTCLASSIFICATION_SCOPE_"></span>"TestClassification:Scope"  
テストの分類"Scope"が「エンジニア リング プロセス イベント」を検証するために使用するテスト関連資料を識別する Windows で発生します。

<span id="_TestClassification_Type_"></span><span id="_testclassification_type_"></span><span id="_TESTCLASSIFICATION_TYPE_"></span>"TestClassification:Type"  
テストの分類"Type"は、識別する必要があるテストの種類を識別します。

<span id="_TestClassification_"></span><span id="_testclassification_"></span><span id="_TESTCLASSIFICATION_"></span>"TestClassification"  
プロパティの値"単位: WUTG"を使用して、Windows の単体テストのガイドライン (WUTG) に準拠している単体テストを示します。 プロパティの値"単位: WUTG:ChexGate"を使用すると、単体テストを Windows 単体テストのガイドライン (WUTG) に準拠しているし、Chex シナリオ (エラーの送信をブロック) のゲートのフェーズ中に実行する必要がありますを指定します。

<span id="_TestTimeout_"></span><span id="_testtimeout_"></span><span id="_TESTTIMEOUT_"></span>"TestTimeout"  
特定のテストまたはセットアップ/クリーンアップ メソッドにかかる時間の最大量を指定します。 参照してください[タイムアウト](taef-timeouts.md)詳細についてはします。

<span id="_ThreadingModel_"></span><span id="_threadingmodel_"></span><span id="_THREADINGMODEL_"></span>"ThreadingModel"  
スレッド モデルのテストで使用される事前構成済みの COM です。 参照してください[スレッド処理モデルを構成する](threading-models.md)詳細についてはします。

データ ドリブンの関連するテスト:

<span id="_DataSource_"></span><span id="_datasource_"></span><span id="_DATASOURCE_"></span>「データ ソース」  
メインのソースのデータを指定します[データ ドリブン テスト](data-driven-testing.md)します。

<span id="_TableId_"></span><span id="_tableid_"></span><span id="_TABLEID_"></span>"TableId"  
名前または「データ ソース」の場合とは別のテーブルの Id を指定します[テーブル ベースのデータ ドリブン テスト](table-data-source.md)します。

<span id="_Pict_Timeout___and_deprecated__PictTimeout__"></span><span id="_pict_timeout___and_deprecated__picttimeout__"></span><span id="_PICT_TIMEOUT___AND_DEPRECATED__PICTTIMEOUT__"></span>"Pict: Timeout"(および非推奨"PictTimeout")  
場合、ユーザーの指定されたモデル ファイルを処理する PICT.exe の許可されている 5 分間の既定のタイムアウトをオーバーライド[PICT ベースのデータ ドリブン テスト](pict-data-source.md)します。

<span id="_Pict_SeedingFile___and_deprecated__Seed__"></span><span id="_pict_seedingfile___and_deprecated__seed__"></span><span id="_PICT_SEEDINGFILE___AND_DEPRECATED__SEED__"></span>"Pict: SeedingFile"(および非推奨「シード」)  
「データ ソース」の場合とは別に、シード ファイルへの相対的な位置を指定した[PICT ベースのデータ ドリブン テスト](pict-data-source.md)します。

<span id="_Pict_Order_"></span><span id="_pict_order_"></span><span id="_PICT_ORDER_"></span>"Pict:Order"  
呼び出された場合の PICT.exe/o パラメーターの値を指定します[PICT ベースのデータ ドリブン テスト](pict-data-source.md)します。

<span id="_Pict_ValueSeparator_"></span><span id="_pict_valueseparator_"></span><span id="_PICT_VALUESEPARATOR_"></span>"Pict: ValueSeparator"  
呼び出された場合の PICT.exe/d パラメーターの値を指定します[PICT ベースのデータ ドリブン テスト](pict-data-source.md)します。

<span id="_Pict_AliasSeparator_"></span><span id="_pict_aliasseparator_"></span><span id="_PICT_ALIASSEPARATOR_"></span>"Pict:AliasSeparator"  
呼び出された場合の PICT.exe/a パラメーターの値を指定します[PICT ベースのデータ ドリブン テスト](pict-data-source.md)します。

<span id="_Pict_NegativeValuePrefix_"></span><span id="_pict_negativevalueprefix_"></span><span id="_PICT_NEGATIVEVALUEPREFIX_"></span>"Pict:NegativeValuePrefix"  
呼び出された場合の PICT.exe/n パラメーターの値を指定します[PICT ベースのデータ ドリブン テスト](pict-data-source.md)します。

<span id="_Pict_Random_"></span><span id="_pict_random_"></span><span id="_PICT_RANDOM_"></span>"Pict:Random"  
PICT.exe を呼び出すときに、ランダム性を使用するかどうかを指定します。 [PICT ベースのデータ ドリブン テスト](pict-data-source.md)します。 これが true の場合は、使用したランダム シードが TAEF によって記録されます。

<span id="_Pict_RandomSeed_"></span><span id="_pict_randomseed_"></span><span id="_PICT_RANDOMSEED_"></span>"Pict:RandomSeed"  
呼び出された場合の PICT.exe/r パラメーターの値を指定します[PICT ベースのデータ ドリブン テスト](pict-data-source.md)します。 これを設定すると変更の既定の"Pict: ランダムな"から false を true にします。

<span id="_Pict_CaseSensitive_"></span><span id="_pict_casesensitive_"></span><span id="_PICT_CASESENSITIVE_"></span>"Pict: CaseSensitive"  
呼び出された場合、PICT.exe の/c パラメーターを使用するかどうかを指定します。 [PICT ベースのデータ ドリブン テスト](pict-data-source.md)します。

関連するデバイスのサポート:

<span id="_TestResourceDependent_"></span><span id="_testresourcedependent_"></span><span id="_TESTRESOURCEDEPENDENT_"></span>"TestResourceDependent"  
現在のスコープ内のテストが TestResource と BuildResourceList(...) によって収集されたリソースの関数に依存していることを指定します。参照してください[デバイスのサポート](device-support.md)詳細についてはします。

<span id="_ResourceSelection_"></span><span id="_resourceselection_"></span><span id="_RESOURCESELECTION_"></span>"ResourceSelection"  
問題のテストに関連する BuildResourceList(...) によって収集された TestResources を照合するクエリを指定します。 参照してください[デバイスのサポート](device-support.md)詳細についてはします。

## <a name="span-idyoucanmetadataspanspan-idyoucanmetadataspanspan-idyoucanmetadataspanyou-can-metadata"></a><span id="_You_can...__Metadata"></span><span id="_you_can...__metadata"></span><span id="_YOU_CAN...__METADATA"></span>"することができます.."。メタデータ


これらのメタデータ プロパティを使用できますが、その解釈は保証されません。たい場合は、チームでそれらを使用できます。

<span id="_Owner_"></span><span id="_owner_"></span><span id="_OWNER_"></span>「所有者」  
テストの所有者のエイリアスです。

<span id="_ProcessUnderTest_"></span><span id="_processundertest_"></span><span id="_PROCESSUNDERTEST_"></span>"ProcessUnderTest"  
ランタイム分析のために便利です。 たとえば、テストを"Explorer.exe"のテストは場合、に対して実行してレーダー (ランタイム分析ツール)、プロセス。

<span id="_Feature_"></span><span id="_feature_"></span><span id="_FEATURE_"></span>「機能」  
特定の機能やテクノロジにテスト カテゴリに分類するための識別子です。 これは、'cookie' 識別子として扱う必要があるが解釈を定義しているチームには、します。

## <a name="span-idreservedmetadataspanspan-idreservedmetadataspanspan-idreservedmetadataspanreserved-metadata"></a><span id="_Reserved__Metadata"></span><span id="_reserved__metadata"></span><span id="_RESERVED__METADATA"></span>'Reserved' のメタデータ


次のメタデータを使用する可能性があります、将来のください使用しないでください。

-   ユーザー
-   IntegrityLevel
-   Timeout
-   HostType

 

 





