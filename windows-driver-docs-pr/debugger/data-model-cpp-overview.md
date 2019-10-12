---
title: デバッガーデータモデルC++のインターフェイスの概要
description: このトピックでは、デバッガーの機能を拡張C++およびカスタマイズするためのデバッガーデータモデルインターフェイスの概要について説明します。
ms.date: 09/12/2019
ms.openlocfilehash: 1f92d9eb8b8095ccbe3d486b027e2c6259da810a
ms.sourcegitcommit: 3b7c8b3cb59031e0f4e39dac106c1598ad108828
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2019
ms.locfileid: "70930381"
---
# <a name="debugger-data-model-c-overview"></a>Debugger Data Model C++ の概要

このトピックでは、デバッガーのデータモデルC++インターフェイスを使用して、デバッガーの機能を拡張およびカスタマイズする方法の概要について説明します。

このトピックは、からC++アクセス可能なインターフェイス、それらを使用してC++ベースのデバッガー拡張機能を構築する方法、および他のデータモデル構造を使用する方法について説明したシリーズの一部です (例:JavaScript または NatVis) をC++データモデル拡張機能から。

[デバッガーデータモデルC++の概要](data-model-cpp-overview.md)

[デバッガーデータモデルC++のインターフェイス](data-model-cpp-interfaces.md)

[デバッガーデータモデルC++オブジェクト](data-model-cpp-objects.md)

[デバッガーデータモデルC++の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーデータモデルC++の概念](data-model-cpp-concepts.md)

[デバッガーデータモデルC++のスクリプト](data-model-cpp-scripting.md)

---

## <a name="span-idoverview-overview-of-the-debugger-data-model-c-interface"></a><span id="overview">デバッガーデータモデルC++インターフェイスの概要

このデバッガー データ モデルは、新しいデバッガー拡張機能 (JavaScript、NatVis、C++ で記述されたものを含む) でデバッガーからの情報を利用したり、デバッガーや他の拡張機能からアクセスできる情報を生成したりするしくみの中心となる、拡張可能なオブジェクト モデルです。 データモデル Api に書き込まれるコンストラクトは、デバッガーの新しい (dx) 式エバリュエーターだけでなく、JavaScript の拡張機能やC++拡張機能からも使用できます。 

デバッガーデータモデルの目標を示すために、この従来のデバッガーコマンドを考えてみましょう。

```console
0: kd> !process 0 0 
PROCESS ffffe0007e6a7780
    SessionId: 1  Cid: 0f68    Peb: 7ff7cfe7a000  ParentCid: 0f34
    DirBase: 1f7fb9000  ObjectTable: ffffc001cec82780  HandleCount:  34.
    Image: echoapp.exe
...
```
デバッガーコマンドはバイナリマスクを使用しており、標準以外の方法でテキストのみの出力を提供します。 テキスト出力は、使用、書式設定、または拡張が困難であり、レイアウトはこのコマンドに固有です。

デバッガーデータモデル[dx (Display Debugger Object Model Expression)](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)コマンドと比較します。

```console
dx @$cursession.Processes.Where(p => p.Threads.Count() > 5)
```
このコマンドは、単一の方法で、検出可能で拡張可能で、コンポーザブルな標準データモデルを使用します。

特定のオブジェクトに対して論理的な名前のスペーシングと拡張を行うと、デバッガー拡張機能の検出が可能になります。  

> [!TIP]
> データモデルC++オブジェクトインターフェイスは、完全C++ C++な例外とテンプレートのプログラミングパラダイムを使用するデータモデルの完全なヘルパーライブラリを実装するために、非常に冗長になる可能性があるため、お勧めします。 詳細については、このトピックで後述する「 [DbgModelClientEx ライブラリの使用](#dbgmodelclientex)」を参照してください。
>

データモデルは、新しい[WinDbg Preview](debugging-using-windbg-preview.md)デバッガーが最も多くのことを表示する方法です。 新しい UI の多くの要素は、データモデルが使用されているため、クエリ、拡張、またはスクリプト化が可能です。 詳細については、「 [WinDbg Preview-Data Model](windbg-data-model-preview.md)」を参照してください。

![プロセスとスレッドを示すデータモデルの探索ウィンドウ](images/windbgx-data-model-process-threads.png)


### <a name="data-model-architectural-view"></a>データモデルのアーキテクチャビュー

次の図は、デバッガーデータモデルアーキテクチャの主要な要素をまとめたものです。

- 左側には、オブジェクトへのアクセスを提供し、LINQ クエリなどの機能をサポートする UI 要素が表示されます。  
- 図の右側には、デバッガーデータモデルにデータを提供するコンポーネントがあります。 これには、カスタムの NatVis C++ 、JavaScript、およびデバッガーデータモデルの拡張機能が含まれます。 

![データモデルのアーキテクチャビュー](images/data-model-simple-architectural-view.png)


### <a name="object-model"></a>オブジェクト モデル

デバッガーデータモデルの中心にあるのは、すべてが IModelObject インターフェイスのインスタンスである、統一されたオブジェクト表現です。  このようなオブジェクトは、組み込み (たとえば、整数値) または別のデータモデルインターフェイスを表す場合がありますが、多くの場合、動的オブジェクト (キー/値/メタデータタプルのディクショナリ) と、抽象動作を記述する一連の概念を表します。   

この図は、IModelObject がキーストアを使用して、プロバイダーが作成、登録、および操作できる値を格納する方法を示しています。

- オブジェクトモデルに情報を提供する*プロバイダー*を示します。
- 左側には、オブジェクトの操作に使用される共通のオブジェクトモデルである*Imodelobject*が表示されます。
- センターは、値の格納とアクセスに使用される*キーストア*です。
- 下部には、表示可能な文字列への変換やインデックス作成などの機能を備えたオブジェクトをサポートする*概念*が示されています。

![データモデルのアーキテクチャビュー](images/data-model-object-model.png)


### <a name="the-data-model-a-consumer-view"></a>データモデル:コンシューマービュー

次の図は、データモデルのコンシューマービューを示しています。 この例では、 [dx (Display Debugger Object Model Expression)](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)コマンドを使用して情報を照会しています。 

- Dx コマンドは、シリアライザーを介してオブジェクト列挙インターフェイスに通信します。 
- IDebugHost * オブジェクトは、デバッガーエンジンから情報を収集するために使用されます。 
- 式とセマンティックエバリュエーターは、要求をデバッガーエンジンに送信するために使用されます。

![データモデルのアーキテクチャビュー](images/data-model-consumer-view.png)


### <a name="the-data-model-a-producer-view"></a>データモデル:プロデューサービュー

この図は、データモデルのプロデューサービューを示しています。

- 追加機能を定義する XML を使用する NatVis プロバイダーが左側に表示されます。
- JavaScript プロバイダーは*動的プロバイダーの概念*を利用して、リアルタイムで情報を操作できます。
- 下部には、追加の機能を定義できるネイティブコードプロバイダーが示されています。

![データモデルのアーキテクチャビュー](images/data-model-producer-view.png)


### <a name="data-model-manager"></a>データモデルマネージャー 

この図は、データモデルマネージャーがオブジェクトの管理において果たす中心的な役割を示しています。

- データモデルマネージャーは、すべてのオブジェクトの中央レジストラーとして機能します。 
- 左側には、セッションやプロセスなどの標準的なデバッガー要素がどのように登録されているかが示されます。
- 名前空間ブロックには、中央登録リストが表示されます。
- ダイアグラムの右側には、2つのプロバイダーが表示されます。1つは一番上C++に NatVis、もう1つは C/拡張です。

![データモデルのアーキテクチャビュー](images/data-model-manager.png)


## <a name="span-idsummary-summary-of-debugger-data-model-interfaces"></a><span id="summary">デバッガーデータモデルインターフェイスの概要

データモデルのさまざまなC++部分を構成するインターフェイスが多数あります。 これらのインターフェイスを一貫した簡単な方法で解決するために、一般的なカテゴリ別に分類されています。 主な領域は次のとおりです。 

**一般的なオブジェクトモデル**

最初の最も重要なインターフェイスセットは、コアデータモデルにアクセスする方法と、オブジェクトにアクセスして操作する方法を定義します。 IModelObject は、データモデル内のすべてのオブジェクト (のオブジェクトなどC#) を表すインターフェイスです。 これは、のコンシューマーとデータモデルに対するプロデューサーの両方にとって重要なインターフェイスです。 その他のインターフェイスは、オブジェクトのさまざまな側面にアクセスするための機構です。 このカテゴリには、次のインターフェイスが定義されています。 


*DbgEng とデータモデル間のブリッジ*

[IHostDataModelAccess](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ihostdatamodelaccess) 

*メインインターフェイス* 

[IModelObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelobject) 

[IKeyStore ストア](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ikeystore) 

[IModelIterator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodeliterator) 

[IModelPropertyAccessor](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelpropertyaccessor) 

[IModelMethod](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelmethod) 

[IKeyEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ikeyenumerator) 

[IRawEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-irawenumerator) 

[IModelKeyReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelkeyreference)  / [IModelKeyReference2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelkeyreference2) 

*概念インターフェイス*

[IStringDisplayableConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-istringdisplayableconcept) 

[IIterableConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-iiterableconcept) 

[IIndexableConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-iindexableconcept) 

[IPreferredRuntimeTypeConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ipreferredruntimetypeconcept) 

[IDataModelConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelconcept) 

[IDynamicKeyProviderConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idynamickeyproviderconcept) 

[IDynamicConceptProviderConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idynamicconceptproviderconcept) 


**データモデルと拡張性の管理**

データモデルマネージャーは、すべての機能拡張がどのように行われるかを管理する主要なコンポーネントです。 これは、ネイティブ型の両方を拡張ポイントにマップする一連のテーブルの中央リポジトリです。また、拡張ポイントへの合成コンストラクトでもあります。 また、オブジェクトのボックス化 (序数値または文字列の IModelObject への変換) を担当するエンティティです。 

このカテゴリには、次のインターフェイスが定義されています。 

*一般データモデルマネージャーへのアクセス* 

[IDataModelManager](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelmanager)  / [IDataModelManager2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelmanager2) 

*スクリプト管理* 

[IDataModelScriptManager](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptmanager) 

[IDataModelScriptProviderEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptproviderenumerator) 


**デバッガーの型システムとメモリスペースへのアクセス**

基になる型システムとデバッガーのメモリ領域は、を使用するための拡張機能について詳細に公開されています。 このカテゴリには、次のインターフェイスが定義されています。 

*汎用ホスト (デバッガー) インターフェイス*

[IDebugHost](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughost) 

[IDebugHostStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughoststatus) 

[IDebugHostContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostcontext) 

[IDebugHostMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmemory)  / [IDebugHostMemory2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmemory2) 

[IDebugHostErrorSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughosterrorsink) 

[IDebugHostEvaluator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostevaluator)  / [IDebugHostEvaluator2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostevaluator2) 

[IDebugHostExtensibility](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostextensibility) 

*ホスト (デバッガー) 型システムインターフェイス* 

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

*ホスト (デバッガー) でのスクリプトのサポート* 

[IDebugHostScriptHost](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostscripthost) 


**スクリプトの作成と使用**

データモデルには、スクリプトの概要とデバッグ方法に関する一般的な概念もあります。 デバッガー拡張機能を使用して、データモデルと別の動的言語 (通常はスクリプト環境) の間に一般的なブリッジを定義することは、まったく可能です。 この一連のインターフェイスは、デバッガーの UI がこのようなスクリプトをどのように活用できるかということです。 

このカテゴリには、次のインターフェイスが定義されています。 

*一般的なスクリプトインターフェイス* 

[IDataModelScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscript) 

[IDataModelScript](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscript) 

[IDataModelScriptClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptclient) 

[IDataModelScriptHostContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscripthostcontext) 

[IDataModelScriptTemplate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscripttemplate) 

[IDataModelScriptTemplateEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscripttemplateenumerator) 

[IDataModelNameBinder](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelnamebinder) 


*スクリプトデバッガーのインターフェイス* 

[IDataModelScriptDebug](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebug) 

[IDataModelScriptDebugClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugclient) 

[IDataModelScriptDebugStack](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugstack) 

[IDataModelScriptDebugStackFrame](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugstackframe) 

[IDataModelScriptDebugVariableSetEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugvariablesetenumerator) 

[IDataModelScriptDebugBreakpoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugbreakpoint) 

[IDataModelScriptDebugBreakpointEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugbreakpointenumerator) 


## <a name="span-iddbgmodelclientex-using-the-dbgmodelclientex-library"></a><span id="dbgmodelclientex">DbgModelClientEx ライブラリの使用

**概要**

データモデルへC++のデータモデルオブジェクトインターフェイスは、実装するには非常に詳細にすることができます。 データモデルの完全な操作は可能ですが、データモデルを拡張するには、いくつかの小さなインターフェイスを実装する必要があります (たとえば、追加される動的フェッチ可能なプロパティごとに IModelPropertyAccessor の実装を実装する必要があります)。 これに加えて、HRESULT ベースのプログラミングモデルでは、エラーチェックに使用される大量のボイラープレートコードが追加されています。

この作業の一部を最小限に抑えるために、完全C++ C++な例外とテンプレートのプログラミングパラダイムを使用するデータモデルの完全なヘルパーライブラリが用意されています。 このライブラリを使用すると、データモデルを使用したり拡張したりするときに、より簡潔なコードを使用することをお勧めします。

ヘルパーライブラリには、次の2つの重要な名前空間があります。

デバッガー::D ataModel:: ClientEx-データモデルの使用に関するヘルパー

デバッガー::D ataModel::P roviderEx-データモデルの拡張のヘルパー

DbgModelClientEx ライブラリの使用方法の詳細については、この github サイトの readme ファイルを参照してください。

https://github.com/Microsoft/WinDbg-Libraries/tree/master/DbgModelCppLib


**HelloWorld C++サンプル**

DbgModelClientEx ライブラリを使用する方法については、こちらのデータモデルC++の HelloWorld サンプルを参照してください。

https://github.com/Microsoft/WinDbg-Samples/tree/master/DataModelHelloWorld

このサンプルには次のものが含まれます。

- HelloProvider-これは、デバッガーのプロセスの概念に "Hello" という新しい例を追加するプロバイダークラスの実装です。

- SimpleIntroExtension-これは、デバッガーのプロセスの概念に "Hello" という新しい例を追加する単純なデバッガー拡張機能です。 この拡張機能は、データモデル C++ 17 ヘルパーライブラリに対して記述されています。  必要なグルーコードのボリューム (および複雑さ) のため、未加工の COM ABI ではなく、このライブラリに対して拡張機能を作成することをお勧めします。


**JavaScript と COM のサンプル**

データモデルを使用してデバッガー拡張機能を記述するさまざまな方法について理解を深めるために、次の3つのバージョンのデータモデル HelloWorld 拡張機能を使用できます。

https://github.com/Microsoft/WinDbg-Samples/tree/master/DataModelHelloWorld

- JavaScript-JavaScript で記述されたバージョン

- C++ 17-データモデル C++ 17 クライアントライブラリに対して作成されたバージョン

- COM-未加工の COM ABI に対して記述されたバージョン (COM ヘルパーに WRL を使用する場合のみ)

---

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[デバッガーデータモデルC++のインターフェイス](data-model-cpp-interfaces.md)

[デバッガーデータモデルC++オブジェクト](data-model-cpp-objects.md)

[デバッガーデータモデルC++の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーデータモデルC++の概念](data-model-cpp-concepts.md)

[デバッガーデータモデルC++のスクリプト](data-model-cpp-scripting.md)
