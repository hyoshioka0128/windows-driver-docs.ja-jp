---
title: デバッガーのデータ モデルの C++ インターフェイスの概要
description: このトピックでは、デバッガー データ モデルの C++ インターフェイスを拡張し、デバッガーの機能をカスタマイズの概要を示します。
ms.date: 04/09/2019
ms.openlocfilehash: de9859083d6ede03b0f9cd6a82e0beeca961eda4
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903354"
---
# <a name="debugger-data-model-c-overview"></a>Debugger Data Model C++ の概要

このトピックでは、デバッガーのデータ モデルの C++ インターフェイスを使用して拡張およびデバッガーの機能をカスタマイズする方法の概要を示します。

このトピックでは、C、C++ ベースのデバッガーの拡張機能の構築に使用する方法および作成する方法からアクセスできるインターフェイスについて説明するシリーズのパートの他のデータ モデルの構成要素を使用して (例。JavaScript または NatVis) C データ モデルの拡張機能から。

[デバッガー データ モデルの C++ の概要](data-model-cpp-overview.md)

[デバッガーのデータ モデルの C++ インターフェイス](data-model-cpp-interfaces.md)

[デバッガーのデータ モデルの C++ オブジェクト](data-model-cpp-objects.md)

[デバッガーのデータ モデルの C++ の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーのデータ モデルの C の概念](data-model-cpp-concepts.md)

[デバッガー データ モデルの C++ のスクリプト](data-model-cpp-scripting.md)

---

## <a name="topic-sections"></a>トピックのセクション

このトピックは次のセクションで構成されます。

[デバッガー データ モデルの C++ インターフェイスの概要](#overview)

[デバッガー データのモデル インターフェイスの概要](#summary)

[DbgModelClientEx ライブラリを使用します。](#dbgmodelclientex)


---

## <a name="span-idoverview-overview-of-the-debugger-data-model-c-interface"></a><span id="overview"> デバッガー データ モデルの C++ インターフェイスの概要

このデバッガー データ モデルは、新しいデバッガー拡張機能 (JavaScript、NatVis、C++ で記述されたものを含む) でデバッガーからの情報を利用したり、デバッガーや他の拡張機能からアクセスできる情報を生成したりするしくみの中心となる、拡張可能なオブジェクト モデルです。 データ モデルの Api に書き込まれるコンストラクトでは、拡張機能の JavaScript または C++ の拡張機能から、デバッガーの新しい (dx) 式エバリュエーターでも使用できます。 

デバッガーのデータ モデルの目的を示すためには、この従来のデバッガー コマンドを検討してください。

```console
0: kd> !process 0 0 
PROCESS ffffe0007e6a7780
    SessionId: 1  Cid: 0f68    Peb: 7ff7cfe7a000  ParentCid: 0f34
    DirBase: 1f7fb9000  ObjectTable: ffffc001cec82780  HandleCount:  34.
    Image: echoapp.exe
...
```
デバッガー コマンドがバイナリ マスクを使用して、非標準の方法でのみ出力テキストを提供します。 テキスト出力が消費する、書式設定、または拡張が困難とレイアウトはこのコマンドを特定します。

これをデバッガーのデータ モデルに対し[dx (表示デバッガー オブジェクト モデルの式)](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)コマンド。

```console
dx @$cursession.Processes.Where(p => p.Threads.Count() > 5)
```
このコマンドは、探索可能な拡張性および統一された方法でコンポーザブルである標準的なデータ モデルを使用します。

論理的にモ ノの間隔と、特定のオブジェクトに対する拡張名は、デバッガーの拡張機能の検出できます。  

> [!TIP]
> ため、データ モデルC++オブジェクト インターフェイスを完全に実装するために非常に冗長になることができますC++データ モデルを完全に使用するためのヘルパー ライブラリC++例外とプログラミング パラダイムでテンプレートをお勧めします。 詳細については、次を参照してください。 [DbgModelClientEx ライブラリを使用して](#dbgmodelclientex)このトピックで後述します。
>

データ モデルは、方法を新しい[WinDbg プレビュー](debugging-using-windbg-preview.md)デバッガー、ほとんどの機能が表示されます。 新しい UI の多くの要素のクエリを実行、拡張、またはデータ モデルで電源が入っているため、スクリプト化します。 詳細については、次を参照してください。 [WinDbg Preview - データ モデル](windbg-data-model-preview.md)します。

![データ モデルの詳細 ウィンドウが表示されたプロセスとスレッド](images/windbgx-data-model-process-threads.png)


### <a name="data-model-architectural-view"></a>データ モデルのアーキテクチャの表示

次の図は、デバッガーのデータ モデルのアーキテクチャの主要な要素をまとめたものです。

- 左側にあるには、オブジェクトへのアクセスを提供して、LINQ クエリとは、このような機能をサポート、UI 要素が表示されます。  
- 図の右側にある、デバッガーのデータ モデルにデータを提供するコンポーネントです。 これには、カスタム NatVis、JavaScript および C++ デバッガー データ モデルの拡張機能が含まれます。 

![データ モデルのアーキテクチャの表示](images/data-model-simple-architectural-view.png)


### <a name="object-model"></a>オブジェクト モデル

デバッガーのデータ モデルの中心は IModelObject インターフェイスのインスタンスのすべての uniform オブジェクト表現です。  このようなオブジェクトを表すことがあります組み込み中 (例:: 整数値) と、別のデータ モデル インターフェイスでは、多くの場合を表すメタデータ/キー/値のタプルのディクショナリと一連の抽象の動作を説明する概念 – 動的オブジェクトです。   

この図は、IModelObject で、プロバイダーは、作成、登録、および操作する値を含むキー ストアを使用する方法を示します。

- 表示、*プロバイダー*、オブジェクト モデルへの情報を提供します。
- 左側の表示、 *IModelObject*オブジェクトを操作するために使用される共通のオブジェクト モデルは。
- 中央には、*キー ストア*保存し、値のアクセスに使用されます。
- 下部に表示*概念*表示可能な文字列に変換したり、インデックスを作成する機能などの機能を持つオブジェクトをサポートします。

![データ モデルのアーキテクチャの表示](images/data-model-object-model.png)


### <a name="the-data-model-a-consumer-view"></a>データ モデル:コンシューマー ビュー

次の図は、データ モデルのコンシューマー全体を表示します。 例では、 [dx (表示デバッガー オブジェクト モデルの式)](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)コマンドは、情報の照会に使用されています。 

- Dx コマンドは、シリアライザーにオブジェクトの列挙体インターフェイスを介して通信します。 
- IDebugHost * オブジェクトは、デバッガー エンジンから情報を収集するために使用されます。 
- 式は、セマンティックの評価者は、デバッガー エンジンに要求を送信に使用されます。

![データ モデルのアーキテクチャの表示](images/data-model-consumer-view.png)


### <a name="the-data-model-a-producer-view"></a>データ モデル:プロデューサー ビュー

この図は、データ モデルのプロデューサー ビューを示しています。

- NatVis プロバイダーは、追加の機能を定義する XML を使用する左側に表示されます。
- JavaScript のプロバイダーが利用できます*動的プロバイダーの概念*リアルタイムで情報を操作します。
- 下部には、追加の機能を定義することもをネイティブ コード プロバイダーが表示されます。

![データ モデルのアーキテクチャの表示](images/data-model-producer-view.png)


### <a name="data-model-manager"></a>データ モデルのマネージャー 

この図では、データ モデルのマネージャーは、オブジェクトの管理が再生される中心的役割を示します。

- データ モデルのマネージャーは、すべてのオブジェクトのサーバーの全体のレジストラーとして機能します。 
- 左側の要素を示しています標準デバッガー セッションとプロセスが登録されているようです。
- 名前空間ブロックには、集中登録一覧が表示されます。
- 図の右側にあるは、下部にある 2 つのプロバイダーが一番上に、NatVis および C と C++ の拡張機能のいずれかを示します。

![データ モデルのアーキテクチャの表示](images/data-model-manager.png)


## <a name="span-idsummary-summary-of-debugger-data-model-interfaces"></a><span id="summary"> デバッガー データのモデル インターフェイスの概要

多数のさまざまなデータ モデルの配置を構成するための C++ インターフェイスがあります。 これらのインターフェイスを実現するには、一貫性のある簡単な方法で、するには [全般] カテゴリで分類がされます。 ここで、メインの領域は、: 

**一般的なオブジェクト モデル**

最初、最も重要な一連のインターフェイスは、コア データ モデルへのアクセスを取得する方法とアクセスし、オブジェクトを操作する方法を定義します。 IModelObject はデータ モデルのすべてのオブジェクトを表すインターフェイス (よく似たC#'s オブジェクト)。 これは、メインのコンシューマーとプロデューサーがデータ モデルへの関心のあるインターフェイスです。 その他のインターフェイスは、オブジェクトのさまざまな側面にアクセスするための機構です。 このカテゴリには、次のインターフェイスが定義されています。 


*DbgEng とデータ モデルの間のブリッジ*

[IHostDataModelAccess](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ihostdatamodelaccess) 

*メイン インターフェイス* 

[IModelObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelobject) 

[IKeyStore](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ikeystore) 

[IModelIterator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodeliterator) 

[IModelPropertyAccessor](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelpropertyaccessor) 

[IModelMethod](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelmethod) 

[IKeyEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ikeyenumerator) 

[IRawEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-irawenumerator) 

[IModelKeyReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelkeyreference)  / [IModelKeyReference2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelkeyreference2) 

*インターフェイスの概念*

[IStringDisplayableConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-istringdisplayableconcept) 

[IIterableConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-iiterableconcept) 

[IIndexableConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-iindexableconcept) 

[IPreferredRuntimeTypeConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ipreferredruntimetypeconcept) 

[IDataModelConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelconcept) 

[IDynamicKeyProviderConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idynamickeyproviderconcept) 

[IDynamicConceptProviderConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idynamicconceptproviderconcept) 


**データの管理モデルと機能拡張**

データ モデルのマネージャーを管理するコア コンポーネントは、すべての機能拡張が実行されます。 これは、一連の拡張ポイントと拡張機能ポイントに代理の構成要素に両方のネイティブ型をマップするテーブルの中央のリポジトリ。 さらに、オブジェクト (IModelObject への序数値または文字列の変換) のボックス化の原因となっているエンティティになります。 

このカテゴリには、次のインターフェイスが定義されています。 

*一般的なデータ モデルのマネージャーへのアクセス* 

[IDataModelManager](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelmanager)  / [IDataModelManager2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelmanager2) 

*スクリプトの管理* 

[IDataModelScriptManager](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptmanager) 

[IDataModelScriptProviderEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptproviderenumerator) 


**デバッガーの型システムとのメモリ領域へのアクセス**

デバッガーの基になる型システム、メモリ スペースがさせる拡張機能の詳細で公開されるを使用します。 このカテゴリには、次のインターフェイスが定義されています。 

*全般的なホスト (デバッガー) インターフェイス*

[IDebugHost](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughost) 

[IDebugHostStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughoststatus) 

[IDebugHostContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostcontext) 

[IDebugHostMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmemory)  / [IDebugHostMemory2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmemory2) 

[IDebugHostErrorSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughosterrorsink) 

[IDebugHostEvaluator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostevaluator)  / [IDebugHostEvaluator2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostevaluator2) 

[IDebugHostExtensibility](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostextensibility) 

*ホスト (デバッガー) の型システムのインターフェイス* 

[IDebugHostSymbols](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostsymbols) 

[IDebugHostSymbol](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostsymbol)  / [IDebugHostSymbol2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostsymbol2) 

[IDebugHostModule](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmodule) 

[IDebugHostType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughosttype)  / [IDebugHostType2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughosttype2) 

[IDebugHostConstant](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostconstant) 

[IDebugHostField](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostfield) 

[IDebugHostData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostdata) 

[IDebugHostBaseClass](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostbaseclass) 
[IDebugHostPublic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostpublic) 

[IDebugHostModuleSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmodulesignature) 

[IDebugHostTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughosttypesignature) 

*スクリプトのホスト (デバッガー) のサポート* 

[IDebugHostScriptHost](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostscripthost) 


**作成とスクリプトを利用**

データ モデルでは、どのようなスクリプトは、いずれかをデバッグする方法の一般的な概念もあります。 デバッガー拡張が登場し、データ モデルと別の動的言語 (通常はスクリプト環境) 間の一般的なブリッジを定義することが可能になります。 この一連のインターフェイスを実現する方法も UI と、デバッガーがこのようなスクリプトの使用方法です。 

このカテゴリには、次のインターフェイスが定義されています。 

*全般スクリプト インターフェイス* 

[IDataModelScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscript) 

[IDataModelScript](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscript) 

[IDataModelScriptClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptclient) 

[IDataModelScriptHostContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscripthostcontext) 

[IDataModelScriptTemplate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscripttemplate) 

[IDataModelScriptTemplateEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscripttemplateenumerator) 

[IDataModelNameBinder](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelnamebinder) 


*スクリプト デバッガー インターフェイス* 

[IDataModelScriptDebug](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebug) 

[IDataModelScriptDebugClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugclient) 

[IDataModelScriptDebugStack](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugstack) 

[IDataModelScriptDebugStackFrame](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugstackframe) 

[IDataModelScriptDebugVariableSetEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugvariablesetenumerator) 

[IDataModelScriptDebugBreakpoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugbreakpoint) 

[IDataModelScriptDebugBreakpointEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugbreakpointenumerator) 


## <a name="span-iddbgmodelclientex-using-the-dbgmodelclientex-library"></a><span id="dbgmodelclientex"> DbgModelClientEx ライブラリを使用します。

**概要**

データ モデルC++データ モデルにオブジェクトのインターフェイスを実装するために非常に冗長になることができます。 さまざまなデータ モデルを拡張する小規模なインターフェイスの実装に必要なデータ モデルの完全な操作は、許可、(例:: IModelPropertyAccessor 追加される各動的 fetchable プロパティの実装)。 さらに、HRESULT ベースのプログラミング モデルは、大量のエラー チェックに使用されるボイラー プレート コードを追加します。

この作業の一部を最小限に抑えるためには、完全なC++データ モデルを完全に使用するためのヘルパー ライブラリC++例外とテンプレートのプログラミング パラダイムです。 このライブラリの使用を消費したり、データ モデルを拡張するときより簡潔なコードをできるようにお勧めします。

ヘルパー ライブラリには、2 つの重要な名前空間があります。

Debugger::DataModel::ClientEx - データ モデルの使用量のヘルパー

Debugger::DataModel::ProviderEx - データ モデルを拡張するためのヘルパー

DbgModelClientEx ライブラリを使用する方法については、この github サイトで readme ファイルを参照してください。

https://github.com/Microsoft/WinDbg-Libraries/tree/master/DbgModelCppLib


**HelloWorldC++サンプル**

DbgModelClientEx ライブラリの使用方法を表示するには、データ モデルの HelloWorld を参照してください。C++こちらのサンプルです。

https://github.com/Microsoft/WinDbg-Samples/tree/master/DataModelHelloWorld

このサンプルは次のとおりです。

- HelloProvider.cpp - これは、追加する新しいプロパティの例「こんにちは」に、デバッガーの概念、プロセスのプロバイダー クラスの実装です。

- SimpleIntroExtension.cpp - これは、新しいプロパティを追加の例「こんにちは」に、デバッガーの概念、プロセスの簡単なデバッガー拡張機能です。 この拡張機能は、データ モデル c++ 17 ヘルパー ライブラリに対して書き込まれます。  生の COM ABI に必要なグルー コードの量 (および複雑さ) ではなく、このライブラリに対して拡張機能を記述することをお勧めまでになります。


**JavaScript と COM のサンプル**

データ モデルとデバッガー拡張機能を記述するさまざまな方法を理解するためにあるはデータ モデルの HelloWorld 拡張機能の 3 つのバージョン。

https://github.com/Microsoft/WinDbg-Samples/tree/master/DataModelHelloWorld

- JavaScript の JavaScript で記述されたバージョン

- C++ 17 - 17 のクライアント ライブラリ、データ モデルでは c++ に対して記述されたバージョン

- COM の (WRL を使用して、COM ヘルパー) のみ、生の COM ABI に対して記述されたバージョン

---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[デバッガー データ モデルの C++ の概要](data-model-cpp-overview.md)

[デバッガーのデータ モデルの C++ インターフェイス](data-model-cpp-interfaces.md)

[デバッガーのデータ モデルの C++ オブジェクト](data-model-cpp-objects.md)

[デバッガーのデータ モデルの C++ の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーのデータ モデルの C の概念](data-model-cpp-concepts.md)

[デバッガー データ モデルの C++ のスクリプト](data-model-cpp-scripting.md)
