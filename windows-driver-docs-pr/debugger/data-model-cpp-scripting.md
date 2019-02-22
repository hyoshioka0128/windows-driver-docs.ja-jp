---
title: デバッガー データ モデルの C++ のスクリプト
description: このトピックでは、デバッガーのデータ モデルの C++ デバッガー エンジンとオートメーションをサポートするためにスクリプトを使用する方法について説明します。
ms.date: 10/08/2018
ms.openlocfilehash: 7860ee5a0f36c9f03eadc028f0c92cc10fc99e16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531217"
---
# <a name="debugger-data-model-c-scripting"></a>デバッガー データ モデルの C++ のスクリプト

このトピックでは、デバッガーのデータ モデル C++ デバッガー データ モデル C++ スクリプトを使用するデバッガー エンジンとオートメーションをサポートするためにスクリプトを使用する方法について説明します。

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

[デバッガー データ モデルのスクリプトの管理](#scriptmanangement)

[デバッガーのスクリプトを実行してデータ モデルの C++ ホスト インターフェイス](#hostinterfacesscript)

[デバッガーのデータ モデルの C++ スクリプト インターフェイス](#scriptinterface)

[デバッガーのデータ モデルの C++ スクリプト デバッグのインターフェイス](#debugscript)

---

## <a name="span-idscriptmanangement-script-management-in-the-debugger-data-model"></a><span id="scriptmanangement"> デバッガー データ モデルのスクリプトの管理 

オブジェクトの作成と拡張機能で中央機関として、データ モデルのマネージャーの役割だけでなく、スクリプトの抽象的な概念の管理を担当はもします。 スクリプト マネージャー部分のデータ モデル マネージャーの観点から、スクリプトには動的に読み込まれた、アンロード、および拡張したり、データ モデルに新しい機能を提供するために、プロバイダーでは、デバッグ可能性があることができます。 

スクリプトのプロバイダーは、言語をブリッジするコンポーネント (例。NatVis、JavaScript など.)。データ モデル。 1 つまたは複数のファイル拡張子を登録します (例:"です。NatVis"、".js") は、デバッガーのクライアントまたはプロバイダーへの委任でその特定の拡張子を持つスクリプト ファイルの読み込みを許可するユーザー インターフェイスを許可するプロバイダーによって処理されます。 


**コア スクリプト マネージャー:IDataModelScriptManager**

コア スクリプト マネージャーのインターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptManager, IUnknown)
{
    STDMETHOD(GetDefaultNameBinder)(_COM_Outptr_ IDataModelNameBinder **ppNameBinder) PURE;
    STDMETHOD(RegisterScriptProvider)(_In_ IDataModelScriptProvider *provider) PURE;
    STDMETHOD(UnregisterScriptProvider)(_In_ IDataModelScriptProvider *provider) PURE;
    STDMETHOD(FindProviderForScriptType)(_In_ PCWSTR scriptType, _COM_Outptr_ IDataModelScriptProvider **provider) PURE;
    STDMETHOD(FindProviderForScriptExtension)(_In_ PCWSTR scriptExtension, _COM_Outptr_ IDataModelScriptProvider **provider) PURE;
    STDMETHOD(EnumerateScriptProviders)(_COM_Outptr_ IDataModelScriptProviderEnumerator **enumerator) PURE;
}
```

[GetDefaultNameBinder](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-getdefaultnamebinder)

GetDefaultNameBinder メソッドは、データ モデルの既定のスクリプト名のバインダーを返します。 名前のバインダーは、オブジェクトのコンテキスト内での名前を解決するコンポーネントです。 たとえば、"foo.bar"式を指定するには、名前バインダー転位 foo をオブジェクトのコンテキストで、名前のバーを解決するのには。 ここで返される binder では、一連のデータ モデルの既定のルールに従います。 スクリプトのプロバイダーは、このバインダーを使用して、プロバイダー間で名前解決の一貫性を提供することができます。 


[RegisterScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-registerscriptprovider)

RegisterScriptProvider メソッドは、新しいスクリプト プロバイダーがデータ モデルに新しい言語のブリッジの対応が存在するデータ モデルを通知します。 このメソッドが呼び出されると、スクリプト マネージャーはすぐに、指定されたスクリプトのプロバイダーのコールバックし、管理スクリプトのプロパティの照会します。 指定されたスクリプトのプロバイダーを示すファイル名または拡張子の下に登録プロバイダーは既に、このメソッドは失敗します。 特定のファイル名または拡張子のハンドラーとしては、1 つのスクリプトのプロバイダーのみを登録できます。 


[UnregisterScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-unregisterscriptprovider)

UnregisterScriptProvider メソッドでは、RegisterScriptProvider メソッドの呼び出し元に戻します。 Inpassed スクリプト プロバイダーによって指定された名前とファイルの拡張子は、それに関連付けられたされなくなります。 あることを非常に多くのスクリプトのプロバイダーへの未解決の COM 参照の登録を解除した後でもに注意してください。 重要です。 このメソッドは、指定されたスクリプトのプロバイダーを管理する型のスクリプトの読み込み/作成のみを防ぎます。 そのプロバイダーによって読み込まれたスクリプトは、読み込まれたまままたはデバッガー (またはデータ モデル) のオブジェクト モデルを操作が、これらの操作は、スクリプトに参照があります。 データ モデル、メソッド、またはスクリプトの構成要素を直接参照するオブジェクトの可能性があります。 スクリプトのプロバイダーを処理できる準備済みである必要があります。 


[FindProviderForScriptType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-findproviderforscripttype)

FindProviderForScriptType メソッドは、このメソッドに記載されているスクリプトの種類の文字列を持つプロバイダー、スクリプト マネージャーを検索します。 見つかると、このメソッドは失敗します。 できない場合それ以外の場合、このようなスクリプトのプロバイダーが、呼び出し元に返されます。 


[EnumerateScriptProviders](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-enumeratescriptproviders)

EnumerateScriptProviders メソッドでは、RegisterScriptProvider メソッドを呼び出す前を使用して、スクリプト マネージャーに登録されているすべてのスクリプトのプロバイダーを列挙する列挙子を返します。 



**スクリプトのプロバイダーの列挙体。IDataModelScriptProviderEnumerator**

EnumerateScriptProviders メソッドでは、次の形式の列挙子を返します。

```cpp 
DECLARE_INTERFACE_(IDataModelScriptProviderEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptProvider **provider) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptproviderenumerator-reset)

Reset メソッドでは、列挙子を最初の要素を返す前にある位置に移動します。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptproviderenumerator-getnext)

GetNext メソッドは列挙子の要素を前方に 1 つを移動しはその要素にあるスクリプトのプロバイダーを返します。 列挙子が列挙体の末尾に達する E_BOUNDS が返されます。 このエラーを受信した後のメソッドは、GetNext の呼び出しを E_BOUNDS を無期限に返し続けますは。 



## <a name="span-idhostinterfacesscript-debugger-data-model-c-host-interfaces-for-scripting"></a><span id="hostinterfacesscript"> デバッガーのスクリプトを実行してデータ モデルの C++ ホスト インターフェイス

**スクリプトで、ホストの役割**

デバッグ ホストは、そのデバッグ ターゲットなどの言語で式を評価する一連のデバッグ ターゲットの型システムの性質を理解するための非常に低レベル インターフェイスを公開します.通常、スクリプトのような上位のコンストラクトに関心はありません。 このような左は、全体的なデバッガー アプリケーションをまたはこれらの機能を提供する拡張機能に。 ただし、この例外があります。 データ モデルによって全体的なスクリプトの操作性に参加するすべてのデバッグ ホストは、スクリプトのコンテキストを提供するいくつかの単純なインターフェイスを実装する必要があります。 実際には、デバッグ ホストは関数とデータ モデルの名前空間内の機能を提供するその他のスクリプトを配置するスクリプト環境が管理します。 (またはない) を許可するホストを許可されているこのプロセスに関連するのでは、その式エバリュエーターでは、このような機能が使用されます。 ここでのホストの観点から関連するインターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDebugHostScriptHost | 参加するために、スクリプト環境でのデバッグ ホストの機能を示すインターフェイスです。 このインターフェイスは、オブジェクトを配置する場所のスクリプト エンジンに通知するコンテキストを作成できます。
IDataModelScriptHostContext | スクリプトのプロバイダーによって、スクリプトの内容のコンテナーとして使用されるホスト インターフェイスを指定します。 どのデバッガー アプリケーションのオブジェクト モデルのために実行する操作以外のスクリプトの画面の内容は、特定のデバッグ ホスト責任です。 このインターフェイスは、その内容を配置する場所に関する情報を取得するスクリプトのプロバイダーを使用します。 参照してください[データ モデルの C++ スクリプト インターフェイス](#scriptinterface)詳細については、このトピックで後述します。


**デバッグ ホストのスクリプト ホスト:IDebugHostScriptHost**

IDebugHostScriptHost インターフェイスは、コンテキストを新しく作成したスクリプトのデバッグ ホストから取得するスクリプトのプロバイダーによって使用されるインターフェイスです。 このコンテキスト (デバッグ ホストによって提供される) オブジェクトには、スクリプトのプロバイダーがデータ モデルとスクリプト環境の間のブリッジを配置できます。 このようなブリッジでは、データ モデルのメソッド スクリプト関数が呼び出されますたとえば、ある場合があります。 これは、データ モデルにある IModelMethod インターフェイスの呼び出しメソッドの使用率でスクリプト メソッドを呼び出す、呼び出し元を使用できます。 

IDebugHostScriptHost インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDebugHostScriptHost, IUnknown)
{
    STDMETHOD(CreateContext)(_In_ IDataModelScript* script, _COM_Outptr_ IDataModelScriptHostContext** scriptContext) PURE;
}
```

[CreateContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostscripthost-createcontext)

CreateContext メソッドは、スクリプトの内容を配置する新しいコンテキストを作成するスクリプトのプロバイダーによって呼び出されます。 このようなコンテキストは、データ モデルの C++ スクリプト インターフェイスのページに詳しく説明されて IDataModelScriptHostContext インターフェイスによって表されます。 


## <a name="span-idscriptinterface-debugger-data-model-c-scripting-interfaces"></a><span id="scriptinterface"> デバッガーのデータ モデルの C++ スクリプト インターフェイス

**スクリプトとスクリプト インターフェイス**

データ モデルの全体的なアーキテクチャには、いくつかの言語とデータ モデルのオブジェクト モデル間のブリッジを定義するサード パーティができます。 通常、ブリッジされている言語は、データ モデルの環境は非常に動的なであるために、スクリプト言語です。 定義し、このブリッジの言語とデータ モデルのオブジェクト モデルを実装するコンポーネントは、スクリプトのプロバイダーに呼び出されます。 初期化されると、スクリプト プロバイダーは、データ モデルのマネージャーのマネージャー部分をスクリプトを登録し、機能拡張を管理する任意のインターフェイスは、その後、編集するための読み込みを許可、アンロード、および可能性のある、スクリプトのデバッグスクリプトのプロバイダーを管理する言語に書き込まれます。 

Windows のツールのデバッグは、スクリプトの 2 つのプロバイダーを現在定義に注意してください。

- NatVis プロバイダー。 このプロバイダーは、ネイティブ/言語のデータ型の視覚化を許可する DbgEng.dll および NatVis XML と、データ モデルの間のブリッジ内に埋め込まれます。
- JavaScript のプロバイダー。 このプロバイダーは、従来のデバッガーの拡張機能内に含まれています。JsProvider.dll します。 JavaScript 言語と、データ モデルのデバッガーの制御と拡張性の任意の形式で記述されたスクリプト間をブリッジします。

その他の言語をブリッジする、新しいプロバイダーを記述できます (例。Python など.)。データ モデル。 このようなは現在にカプセル化の目的を読み込むための従来のデバッガーの拡張機能。 スクリプト プロバイダー自体は、レガシ エンジンのインターフェイスと依存関係を最小限に抑える必要があり、可能であれば、データ モデルの Api を使用する必要があります。 これにより、移植できるその他の環境をより大幅に簡単にプロバイダーが許可されます。

スクリプトのプロバイダーに関連するインターフェイスの 2 つのクラスがあります。 インターフェイスの最初のクラスは、スクリプトのプロバイダーと管理スクリプトの全般的な管理です。 インターフェイスの 2 番目のクラスは、スクリプトのデバッグをサポートするためです。 最初のセットは必須ですが、サポートを while サポート、2 つ目は省略可能なすべてのプロバイダーの意味を成しません可能性があります。 


全般的な管理インターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDataModelScriptProvider | コア インターフェイスをスクリプトのプロバイダーを実装する必要があります。 これは、プロバイダーの特定の種類のスクリプトのサポートを提供し、特定のファイル拡張子に対して登録するには、データ モデルのマネージャーのスクリプト マネージャーの部分に登録されているインターフェイス
IDataModelScript | プロバイダーによって管理される特定のスクリプトの抽象化します。 読み込まれる各スクリプトを作成または編集されている別の IDataModelScript インスタンス
IDataModelScriptClient | ユーザー インターフェイスに情報を伝達するために、スクリプトのプロバイダーで使用されるクライアント インターフェイスを指定します。 スクリプトのプロバイダーは、このインターフェイスを実装していません。 行う、データ モデルをホストするアプリケーションのスクリプトのプロバイダーの使用は。 スクリプトのプロバイダーは、状態、エラーなどを報告するスクリプトのクライアントのメソッドを呼び出す.
IDataModelScriptHostContext | スクリプトのプロバイダーによって、スクリプトの内容のコンテナーとして使用されるホスト インターフェイスを指定します。 どのデバッガー アプリケーションのオブジェクト モデルのために実行する操作以外のスクリプトの画面の内容は、特定のデバッグ ホスト責任です。 このインターフェイスは、その内容を配置する場所に関する情報を取得するスクリプトのプロバイダーを使用します。
IDataModelScriptTemplate | スクリプトのプロバイダーは、スクリプトを作成するユーザーの開始点として機能する 1 つまたは複数のテンプレートを提供できます。 組み込みエディターを提供するデバッガー アプリケーションには、このインターフェイスを通じてプロバイダーによってアドバタイズされるテンプレート コンテンツを含む新しいスクリプトが事前入力できます。
IDataModelScriptTemplateEnumerator | すべてのさまざまなテンプレートを提供するために、スクリプトのプロバイダーを実装する列挙子インターフェイスをサポートします。
IDataModelNameBinder | 名前バインダー--オブジェクトの値を持つコンテキストでの名前を関連付けることができます。 "Foo.bar"などの指定された式の名前のバインダーが"foo"のオブジェクトのコンテキストで"bar"という名前をバインドし、値またはへの参照を生成すること。 名前のバインダーが通常; スクリプト プロバイダーによって実装されていません既定のバインダーをデータ モデルから取得したし、スクリプトのプロバイダーで使用ではなく、

デバッグのインターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDataModelScriptDebug | コア インターフェイスをスクリプト プロバイダーは、スクリプトをデバッグできるようにするために提供する必要があります。 IDataModelScript インターフェイスの実装クラスでは、スクリプトがデバッグ可能な場合、IDataModelScriptDebug の QueryInterface がなければなりません。
IDataModelScriptDebugClient | スクリプトのデバッグの機能を提供することを希望するユーザー インターフェイスでは、IDataModelScriptDebugClient インターフェイスを実装します。 スクリプトのプロバイダーをデバッグ情報を前後へ渡すには、このインターフェイスを使用して (例:: 発生したイベントやブレークポイントなど.)。
IDataModelScriptDebugStack | スクリプトのプロバイダーは、スクリプト デバッガーに呼び出し履歴の概念を公開するには、このインターフェイスを実装します。
IDataModelScriptDebugStackFrame | スクリプトのプロバイダーは、呼び出し履歴内の特定のスタック フレームの概念を公開するには、このインターフェイスを実装します。
IDataModelScriptDebugVariableSetEnumerator | スクリプトのプロバイダーは、一連の変数を公開するには、このインターフェイスを実装します。 このセットは、関数、一連のローカル変数、または特定のスコープ内の変数のセットをパラメーターのセットを表す可能性があります。 厳密な意味は、インターフェイスの取得方法によって異なります。
IDataModelScriptDebugBreakpoint | スクリプトのプロバイダーは、このインターフェイスの概念を公開して、スクリプト内で、特定のブレークポイントの制御を実装します。
IDataModelScriptDebugBreakpointEnumerator | スクリプトのプロバイダーは、列挙のすべてのブレークポイント (有効または無効) かどうか、スクリプト内で現在存在するためにこれを実装します。

**コア スクリプト プロバイダー:IDataModelScriptProvider**

スクリプトのプロバイダーである必要がある拡張機能は IDataModelScriptProvider インターフェイスの実装を提供し、RegisterScriptProvider メソッドを使用して、データ モデルのマネージャーのスクリプト マネージャー部分など登録する必要があります。 これを実装する必要があります、このコア インターフェイスの定義は以下のとおりです。

```cpp 
DECLARE_INTERFACE_(IDataModelScriptProvider, IUnknown)
{
    STDMETHOD(GetName)(_Out_ BSTR *name) PURE;
    STDMETHOD(GetExtension)(_Out_ BSTR *extension) PURE;
    STDMETHOD(CreateScript)(_COM_Outptr_ IDataModelScript **script) PURE;
    STDMETHOD(GetDefaultTemplateContent)(_COM_Outptr_ IDataModelScriptTemplate **templateContent) PURE;
    STDMETHOD(EnumerateTemplates)(_COM_Outptr_ IDataModelScriptTemplateEnumerator **enumerator) PURE;
}
```

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getname)

GetName メソッドは、SysAllocString メソッドを使用して割り当てられた文字列として、プロバイダーを管理するスクリプトの種類の (またはの言語) の名前を返します。 呼び出し元は SysFreeString を使用して、返される文字列を解放します。 このメソッドから返される可能性があります文字列の例は、"JavaScript"または"NatVis"です。 返される文字列は、データ モデルをホストしているデバッガー アプリケーションのユーザー インターフェイスに表示される可能性があります。 2 つのスクリプトのプロバイダーがありません同じ名前を (大文字と小文字を区別しない) 返すことがあります。 

[GetExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getextension)

GetExtension メソッドは、SysAllocString メソッドを使用して割り当てられた文字列としてのスクリプト (ドット) なしには、このプロバイダーによって管理されるファイル拡張子を返します。 (スクリプトのサポート) を含むデータ モデルをホストしているデバッガー アプリケーションでは、スクリプトのプロバイダーにこの拡張機能を持つスクリプト ファイルの開始を委任します。 呼び出し元は SysFreeString を使用して、返される文字列を解放します。 このメソッドから返される可能性があります文字列の例は、"js"または"NatVis"です。 

[CreateScript](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-createscript)

CreateScript メソッドが新しいスクリプトを作成します。 スクリプトのプロバイダーは、このメソッドが呼び出されるたびに、返された IDataModelScript インターフェイスによって表される新しい、空のスクリプトを返す必要があります。 ユーザー インターフェイスが、ユーザーが編集の新しい空のスクリプトを作成するかどうかや、ディスクからスクリプトのデバッガーのアプリケーションの読み込みがかどうかに関係なく、このメソッドを呼び出すことに注意してください。 プロバイダーは、ファイル I/O に関連するならなければ。 単に IDataModelScript メソッドに渡されるストリームを使用して、ホスト アプリケーションからの要求を処理します。 

[GetDefaultTemplateContent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getdefaulttemplatecontent)

GetDefaultTemplateContent メソッドは、既定のテンプレート コンテンツ プロバイダーのインターフェイスを返します。 これは、新しく作成したスクリプトの編集ウィンドウで事前作成スクリプトのプロバイダーが希望コンテンツです。 スクリプト プロバイダー テンプレートを持たない (または既定のコンテンツとして指定されているテンプレートの内容がない) 場合、スクリプトのプロバイダーは、このメソッドから E_NOTIMPL を返す可能性があります。 

[EnumerateTemplates](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-enumeratetemplates)

EnumerateTemplates メソッドは、これは、さまざまなスクリプト プロバイダーによって提供されるテンプレートを列挙できる列挙子を返します。 テンプレートの内容は、新しいスクリプトを作成するときに編集ウィンドウに「指定済み」である必要があるスクリプト プロバイダーです。 これらのテンプレートの名前を指定できますサポートされている複数の異なるテンプレートがある場合 (例。「スクリプトの命令型」、「拡張機能のスクリプト」)、データ モデルをホストしているデバッガー アプリケーションがユーザーに「テンプレート」を表示する方法を選択できます。 


**コア スクリプト インターフェイス:IDataModelScript**

プロバイダーによって実装されている個別のスクリプトを管理するメイン インターフェイスは、IDataModelScript インターフェイスです。 このインターフェイスを実装するコンポーネントは、クライアントが新しい空のスクリプトを作成するときに返され、IDataModelScriptProvider で CreateScript メソッドを呼び出します。 

プロバイダーによって作成される各スクリプトは、独立したサイロでなければなりません。 1 つのスクリプトは、データ モデルを使用して外部のオブジェクトを明示的に操作を除く他のスクリプトに影響を与えることができません必要があります。 2 つのスクリプトがたとえばできる、いくつかの種類や概念を拡張両方 (例:: どのようなプロセスのデバッガーの概念)。 いずれかのスクリプトは、外部プロセス オブジェクトを使用して他のフィールドにアクセスできます。 

インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDataModelScript, IUnknown)
{
    STDMETHOD(GetName)(_Out_ BSTR *scriptName) PURE;
    STDMETHOD(Rename)(_In_ PCWSTR scriptName) PURE;
    STDMETHOD(Populate)(_In_ IStream *contentStream) PURE;
    STDMETHOD(Execute)(_In_ IDataModelScriptClient *client) PURE;
    STDMETHOD(Unlink)() PURE;
    STDMETHOD(IsInvocable)(_Out_ bool *isInvocable) PURE;
    STDMETHOD(InvokeMain)(_In_ IDataModelScriptClient *client) PURE; 
}
```

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-getname)

GetName メソッドは、割り当てられた文字列として SysAllocString 関数を使用して、スクリプトの名前を返します。 スクリプトが名前をまだ持っていない場合、メソッドは null の BSTR を返す必要があります。 このような状況で成功する必要があります。 スクリプトの名前の変更メソッドの呼び出しを使用して明示的に名前を変更 GetName メソッドは、新しく割り当てられた名前を返す必要があります。 

[名前の変更](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-rename)

Rename メソッドでは、スクリプトに新しい名前を割り当てます。 この名前を保存し、GetName メソッドへの呼び出し時に返すことをスクリプトの実装の役目です。 スクリプトを新しい名前を付けて保存するユーザー インターフェイスを選択すると、これは多くの場合に呼び出されます。 スクリプトの名前を変更すると、ホスト アプリケーションが、スクリプトの内容をプロジェクトには選択に影響する可能性に注意してください。 

[設定](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-populate)

Populate メソッドは、変更、またはスクリプトの"content"を同期するためにクライアントによって呼び出されます。 スクリプトのコードを変更したスクリプトのプロバイダーに通知することをお勧めします。 このメソッドがスクリプトまたは任意のスクリプトを操作するオブジェクトへの変更の実行が発生しないことに注意してください。 重要です。 これは、独自の内部状態を同期ができるように、スクリプトの内容が変更されたスクリプト プロバイダーへの通知だけです。 

[実行](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-execute)

Execute メソッドでは、正常に作成の最後の呼び出しで指定されているとおり、スクリプトの内容を実行し、そのコンテンツに応じて、デバッガーのオブジェクト モデルを変更します。 言語 (またはスクリプト プロバイダー)--ユーザー インターフェイスで、虚数部の「スクリプトの実行」ボタンをクリックすると、作成者が必要とする呼び出される--「メイン関数」を定義している場合、Execute 操作中にこのような「main 関数」は呼び出されません。 のみの初期化とオブジェクトのモデル操作を実行する実行操作と見なすことができます (例: ルートのコードを実行して、機能拡張ポイントの設定)。 

[リンクを解除します。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-unlink)

リンク解除メソッドでは、実行操作を元に戻します。 任意のオブジェクト モデルの操作またはスクリプトの実行中に確立されている機能拡張ポイントは取り消されます。 リンクの解除操作の後、スクリプトは、Execute の呼び出しを使用して再実行される可能性があります。 または解放する場合があります。 

[IsInvocable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-isinvocable)

IsInvocable メソッドでは、その言語またはプロバイダーで定義されている"main"関数があるかどうか、スクリプトが、呼び出し可能な--かどうかを返します。 このような"主な機能"は概念的には、スクリプトの作成者は、ユーザー インターフェイスで、虚数部「スクリプトの実行」ボタンが押された場合に呼び出されますたいものです。 

[InvokeMain](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-invokemain)

スクリプトには、UI の呼び出しからを実行するためのものでは、「メイン関数」が場合などは IsInvocable メソッドから真の戻り値を使用して示します。 ユーザー インターフェイスは、実際には、スクリプトを「起動」InvokeMain メソッドを呼び出すことができます。 これは異なることに注意してください。 *Execute*を実行するすべてのルート コードとブリッジ、スクリプトを基になるホストの名前空間。 


* *、スクリプト クライアント:IDataModelScriptClient **

スクリプトを管理し、ユーザー インターフェイスを持っている必要があるデータ モデルをホストするアプリケーション (グラフィカルなのかどうかまたはコンソール) この概念を IDataModelScriptClient インターフェイスを実装します。 このインターフェイスは、ユーザー インターフェイスにエラーおよびイベント情報を渡すために実行または、スクリプトを呼び出し中に、スクリプトのプロバイダーに渡されます。 

IDataModelScriptClient インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptClient, IUnknown)
{
   STDMETHOD(ReportError)(_In_ ErrorClass errClass, _In_ HRESULT hrFail, _In_opt_ PCWSTR message, _In_ ULONG line, _In_ ULONG position) PURE;
}
```

[ReportError](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptclient-reporterror)

スクリプトの呼び出しの実行中にエラーが発生した場合、スクリプト プロバイダーは、エラーのユーザー インターフェイスに通知する ReportError メソッドを呼び出します。 


**スクリプトのホスト コンテキスト。IDataModelScriptHostContext**

デバッグ ホストには、データ モデルのスクリプトの内容をプロジェクトにその方法と場所に対するいくつかの影響力があります。 配置先となるコンテキストをスクリプトにブリッジを各スクリプトは、ホストを求められます。 これが必要です (例:: 関数を呼び出すことができる、などのオブジェクト.)。このコンテキストは、IDebugHostScriptHost CreateContext メソッドを呼び出すと、IDataModelScriptHostContext の取得を使用して取得されます。 

IDataModelScriptHostContext インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptHostContext, IUnknown)
{
   STDMETHOD(NotifyScriptChange)(_In_ IDataModelScript* script, _In_ ScriptChangeKind changeKind) PURE;
   STDMETHOD(GetNamespaceObject)(_COM_Outptr_ IModelObject** namespaceObject) PURE;
}
```

[NotifyScriptChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripthostcontext-notifyscriptchange)

必要なスクリプトのプロバイダーが関連付けられているコンテキストで NotifyScriptChange メソッドのメソッド呼び出しで発生している特定の操作時にデバッグ ホストを通知します。 このような操作が ScriptChangeKind 列挙体のメンバーとして定義されています。

[GetNamespaceObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripthostcontext-getnamespaceobject)

GetNamespaceObject メソッドは、スクリプトのプロバイダーがデータ モデルとスクリプトの間のブリッジを配置できるオブジェクトを返します。 ここでは、たとえば、スクリプト プロバイダーが実装が呼び出すデータ モデル メソッド オブジェクト (IModelMethod インターフェイス IModelObject にボックス化) をかける場合がありますこれに応じて拡大縮小という名前に、スクリプト内の関数。 


**新しく作成したスクリプトのテンプレート:IDataModelScriptTemplate**

スクリプトを新しいスクリプトのコンテンツを自動的に入力を表示するプロバイダー (例: ユーザー インターフェイスをデバッガーでのスクリプトを作成するユーザーを支援するために) 1 つまたは複数のスクリプト テンプレートを提供することで実行できます。 このようなテンプレートは、IDataModelScriptTemplate インターフェイスを実装し、スクリプトのプロバイダーで GetDefaultTemplate メソッドまたは EnumerateTemplates メソッドを使用して返されるコンポーネントです。 

IDataModelScriptTemplate インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptTemplate, IUnknown)
{
   STDMETHOD(GetName)(_Out_ BSTR *templateName) PURE;
   STDMETHOD(GetDescription)(_Out_ BSTR *templateDescription) PURE;
   STDMETHOD(GetContent)(_COM_Outptr_ IStream **contentStream) PURE;
}
```


[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getname)

GetName メソッドは、テンプレートの名前を返します。 これは、テンプレートに名前がない場合、E_NOTIMPL を失敗可能性があります。 1 つの既定のテンプレート (場合などが存在する場合) 必要はありません、名前を付けます。 その他のすべてのテンプレートが。 これらの名前がテンプレートを選択するためのメニューの一部が作成されると、ユーザー インターフェイスに表示されます。 


[GetDescription](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getdescription)

GetDescription メソッドは、テンプレートの説明を返します。 このような説明は、テンプレートのわかりやすくわかりやすいインターフェイスでユーザーに提示されますが実行するように設計します。 テンプレートは、説明があるない場合、このメソッドから E_NOTIMPL を返す可能性があります。 

[GetContent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getcontent)

GetContent メソッドは、テンプレートのコンテンツ (またはコード) を返します。 これは、このテンプレートから新しいスクリプトを作成するユーザーが選択した場合、編集ウィンドウに自動的に入力となります。 テンプレートは作成を担当する (および返す)、クライアントを取得できるコンテンツを標準のストリーム。 

**プロバイダーのテンプレートのコンテンツの列挙体。IDataModelScriptTemplateEnumerator**

スクリプトのプロバイダーは、一部のユーザー インターフェイスで新しく作成したスクリプトに 1 つまたは複数のテンプレート前塗りつぶしコンテンツを提供できます。 これらのテンプレートのいずれかを指定しない場合、スクリプト プロバイダーは、上に EnumerateTemplates メソッドの呼び出し時に返される列挙子を実装する必要があります。 

このような列挙子 IDataModelScriptTemplateEnumerator インターフェイスの実装は、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptTemplateEnumerator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptTemplate **templateContent) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplateenumerator-reset)

Reset メソッドは、作成時にまず--最初のテンプレートを生成する前に位置する列挙子をリセットします。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplateenumerator-getnext)

GetNext メソッドは、次のテンプレートに、列挙子を移動し、返します。 列挙体の末尾には、列挙子は E_BOUNDS を返します。 E_BOUNDS マーカーがヒットすると、列挙子のリセットの呼び出しが行われるまで無期限に E_BOUNDS エラーを生成するために続行されます。 


**名前の意味を解決するには。IDataModelNameBinder**

データ モデルが特定のコンテキストで指定された名前の意味を判断するスクリプトのプロバイダーの標準的な方法を提供します (例:: foo.bar はどのようなバーを決定する) のさまざまなスクリプト プロバイダー間で動作します。 このメカニズムは名前バインダーと呼ばれ、IDataModelNameBinder インターフェイスとして表されます。 このようなバインダーは、一連の名前を解決する方法と、名前が定義されている複数回、オブジェクトの競合の解決を処理する方法に関する規則をカプセル化します。 これらの規則の一部には、射影された名前 (データ モデルによって追加されたもの) が (デバッグ中の言語の型システムで 1 つ) のネイティブ名が解決する方法などが含まれます。 

スクリプト プロバイダー間で一貫性の程度を提供するために、データ モデルのスクリプト マネージャーは、既定名バインダーを提供します '。 IDataModelScriptManager インターフェイスで GetDefaultNameBinder メソッドの呼び出しを使用して、この既定のバインダーで名前を取得できます。 名前のバインダー インターフェイスの定義は以下のとおりです。 

```cpp
DECLARE_INTERFACE_(IDataModelNameBinder, IUnknown)
{
   STDMETHOD(BindValue)(_In_ IModelObject* contextObject, _In_ PCWSTR name, _COM_Errorptr_ IModelObject** value, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(BindReference)(_In_ IModelObject* contextObject, _In_ PCWSTR name, _COM_Errorptr_ IModelObject** reference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(EnumerateValues)(_In_ IModelObject* contextObject, _COM_Outptr_ IKeyEnumerator** enumerator) PURE;
   STDMETHOD(EnumerateReferences)(_In_ IModelObject* contextObject, _COM_Outptr_ IKeyEnumerator** enumerator) PURE;
}
```

[BindValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelnamebinder-bindvalue)

BindValue メソッドでは、バインディング規則のセットに応じて、指定したオブジェクトに対して contextObject.name のと同じを実行します。 このバインディングの結果は、値です。 値として、基になるスクリプトのプロバイダー名に割り当てを実行するのに値は使用できません。

[BindReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelnamebinder-bindreference)

ContextObject.name のと同じバインディング規則のセットに応じて指定したオブジェクトを実行するには、BindReference メソッドを BindValue に似ています。 このメソッドからのバインドの結果は、ただし、値の代わりに参照します。 参考として、スクリプトのプロバイダーは、名に割り当てを実行する参照を利用できます。 

[EnumerateValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelnamebinder-enumeratevalues)

EnumerateValues メソッドは、名前と BindValue メソッドの規則に従ってオブジェクトに対してバインドが値のセットを列挙します。 異なり EnumerateKeys、EnumerateValues、および同様の方法で IModelObject (基本クラス、親モデル、およびなど) の同じ値を持つ複数の名前を返す可能性がありますが、この列挙子はのみ返すにはバインド名の特定のセットBindValue BindReference. 名前は重複していることはありません。 IModelObject メソッドの呼び出しよりも名前バインダーを使用してオブジェクトを列挙するのに非常に高いコストがあることに注意してください。 

[EnumerateReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelnamebinder-enumeratereferences)

EnumerateReferences メソッドは、名前と BindReference メソッドの規則に従ってオブジェクトに対してバインドが、それらへの参照のセットを列挙します。 異なり EnumerateKeys、EnumerateValues、および同様の方法で IModelObject (基本クラス、親モデル、およびなど) の同じ値を持つ複数の名前を返す可能性がありますが、この列挙子はのみ返すにはバインド名の特定のセットBindValue BindReference. 名前は重複していることはありません。 IModelObject メソッドの呼び出しよりも名前バインダーを使用してオブジェクトを列挙するのに非常に高いコストがあることに注意してください。 


## <a name="span-iddebugscript-debugger-data-model-c-script-debugging-interfaces"></a><span id="debugscript"> デバッガーのデータ モデルの C++ スクリプト デバッグのインターフェイス

データ モデルのスクリプトのプロバイダーのインフラストラクチャには、スクリプトをデバッグに関する概念も提供します。 デバッグ ホストとデータ モデルをホストしているデバッガー アプリケーションのデバッグ機能を公開することを希望する任意のスクリプトは、デバッグ可能なスクリプトが IDataModelScript インターフェイスだけでなく IDataModelScriptDebug インターフェイスを実装することでこれを実行できます。 スクリプトでは、このインターフェイスの存在はインフラストラクチャにデバッグ可能であることを示します。 

IDataModelScriptDebug インターフェイスには、スクリプトのプロバイダーのデバッグ機能へのアクセスを取得する開始点が、全体的なデバッグ機能を提供するために他のインターフェイスのセットによって参加しています。 

デバッグのインターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDataModelScriptDebug | コア インターフェイスをスクリプト プロバイダーは、スクリプトをデバッグできるようにするために提供する必要があります。 IDataModelScript インターフェイスの実装クラスでは、スクリプトがデバッグ可能な場合、IDataModelScriptDebug の QueryInterface がなければなりません。
IDataModelScriptDebugClient | スクリプトのデバッグの機能を提供することを希望するユーザー インターフェイスでは、IDataModelScriptDebugClient インターフェイスを実装します。 スクリプトのプロバイダーをデバッグ情報を前後へ渡すには、このインターフェイスを使用して (例:: 発生したイベントやブレークポイントなど.)。
IDataModelScriptDebugStack | スクリプトのプロバイダーは、スクリプト デバッガーに呼び出し履歴の概念を公開するには、このインターフェイスを実装します。
IDataModelScriptDebugStackFrame | スクリプトのプロバイダーは、呼び出し履歴内の特定のスタック フレームの概念を公開するには、このインターフェイスを実装します。
IDataModelScriptDebugVariableSetEnumerator | スクリプトのプロバイダーは、一連の変数を公開するには、このインターフェイスを実装します。 このセットは、関数、一連のローカル変数、または特定のスコープ内の変数のセットをパラメーターのセットを表す可能性があります。 厳密な意味は、インターフェイスの取得方法によって異なります。
IDataModelScriptDebugBreakpoint | スクリプトのプロバイダーは、このインターフェイスの概念を公開して、スクリプト内で、特定のブレークポイントの制御を実装します。
IDataModelScriptDebugBreakpointEnumerator | スクリプトのプロバイダーは、列挙のすべてのブレークポイント (有効または無効) かどうか、スクリプト内で現在存在するためにこれを実装します。

全般的な管理インターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDataModelScriptProvider | コア インターフェイスをスクリプトのプロバイダーを実装する必要があります。 これは、プロバイダーの特定の種類のスクリプトのサポートを提供し、特定のファイル拡張子に対して登録するには、データ モデルのマネージャーのスクリプト マネージャーの部分に登録されているインターフェイス
IDataModelScript | プロバイダーによって管理される特定のスクリプトの抽象化します。 読み込まれる各スクリプトを作成または編集されている別の IDataModelScript インスタンス
IDataModelScriptClient | ユーザー インターフェイスに情報を伝達するために、スクリプトのプロバイダーで使用されるクライアント インターフェイスを指定します。 スクリプトのプロバイダーは、このインターフェイスを実装していません。 行う、データ モデルをホストするアプリケーションのスクリプトのプロバイダーの使用は。 スクリプトのプロバイダーは、状態、エラーなどを報告するスクリプトのクライアントのメソッドを呼び出す.
IDataModelScriptHostContext | スクリプトのプロバイダーによって、スクリプトの内容のコンテナーとして使用されるホスト インターフェイスを指定します。 どのデバッガー アプリケーションのオブジェクト モデルのために実行する操作以外のスクリプトの画面の内容は、特定のデバッグ ホスト責任です。 このインターフェイスは、その内容を配置する場所に関する情報を取得するスクリプトのプロバイダーを使用します。
IDataModelScriptTemplate | スクリプトのプロバイダーは、スクリプトを作成するユーザーの開始点として機能する 1 つまたは複数のテンプレートを提供できます。 組み込みエディターを提供するデバッガー アプリケーションには、このインターフェイスを通じてプロバイダーによってアドバタイズされるテンプレート コンテンツを含む新しいスクリプトが事前入力できます。
IDataModelScriptTemplateEnumerator | すべてのさまざまなテンプレートを提供するために、スクリプトのプロバイダーを実装する列挙子インターフェイスをサポートします。
IDataModelNameBinder | 名前バインダー--オブジェクトの値を持つコンテキストでの名前を関連付けることができます。 "Foo.bar"などの指定された式の名前のバインダーが"foo"のオブジェクトのコンテキストで"bar"という名前をバインドし、値またはへの参照を生成すること。 名前のバインダーが通常; スクリプト プロバイダーによって実装されていません代わりに、既定のバインダーをデータ モデルから取得したし、スクリプト プロバイダーで使用します。


**スクリプトをデバッグ可能にするには。IDataModelScriptDebug**

これはデバッグ可能な任意のスクリプトでは、IDataModelScript を実装するのと同じコンポーネントの IDataModelScriptDebug インターフェイスの存在を使用してこの機能を示します。 デバッグ ホストまたはデータ モデルをホストしているデバッガー アプリケーションによっては、このインターフェイスのクエリは、デバッグ機能のプレゼンスを示すものです。 

IDataModelScriptDebug インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebug, IUnknown)
{
   STDMETHOD_(ScriptDebugState, GetDebugState)() PURE;
   STDMETHOD(GetCurrentPosition)(_Out_ ScriptDebugPosition *currentPosition, _Out_opt_ ScriptDebugPosition *positionSpanEnd, _Out_opt_ BSTR *lineText) PURE;
   STDMETHOD(GetStack)(_COM_Outptr_ IDataModelScriptDebugStack **stack) PURE;
   STDMETHOD(SetBreakpoint)(_In_ ULONG linePosition, _In_ ULONG columnPosition, _COM_Outptr_ IDataModelScriptDebugBreakpoint **breakpoint) PURE;
   STDMETHOD(FindBreakpointById)(_In_ ULONG64 breakpointId, _COM_Outptr_ IDataModelScriptDebugBreakpoint **breakpoint) PURE;
   STDMETHOD(EnumerateBreakpoints)(_COM_Outptr_ IDataModelScriptDebugBreakpointEnumerator **breakpointEnum) PURE;
   STDMETHOD(GetEventFilter)(_In_ ScriptDebugEventFilter eventFilter, _Out_ bool *isBreakEnabled) PURE;
   STDMETHOD(SetEventFilter)(_In_ ScriptDebugEventFilter eventFilter, _In_ bool isBreakEnabled) PURE;
   STDMETHOD(StartDebugging)(_In_ IDataModelScriptDebugClient *debugClient) PURE;
   STDMETHOD(StopDebugging)(_In_ IDataModelScriptDebugClient *debugClient) PURE;
}
```

[GetDebugState](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getdebugstate)

GetDebugState メソッドは、スクリプトの現在の状態を返します (例:: かどうかの実行するかどうか)。 状態は、ScriptDebugState 列挙内の値によって定義されます。

[GetCurrentPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getcurrentposition)

GetCurrentPosition' メソッドは、スクリプト内の現在位置を返します。 これだけを呼び出すこと、デバッガーに、スクリプトが壊れている GetScriptState への呼び出しが ScriptDebugBreak を返す場合します。 このメソッドにその他の呼び出しは有効でないため、失敗します。 

[GetStack](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getstack)

GetStack メソッドは、区切り位置にある現在の呼び出し履歴を取得します。 このメソッドは、スクリプトは、デバッガーに分割時にのみ呼び出す可能性があります。 

[SetBreakpoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-setbreakpoint)

SetBreakpoint メソッドは、スクリプト内でブレークポイントを設定します。 実装が自由に、適切なコードの位置を前方に移動する inpassed 行と列の位置を調整することに注意してください。 返された IDataModelScriptDebugBreakpoint インターフェイスに対するメソッド呼び出しでは、実際の行と列番号が、ブレークポイントが配置された場所を取得できます。 

[FindBreakpointById](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-findbreakpointbyid)

SetBreakpoint メソッドを使用してスクリプト内で作成される各ブレークポイントでは、実装によって、一意の識別子 (64 ビット符号なし整数) を割り当てられます。 FindBreakpointById メソッドを使用して、指定された識別子からブレークポイントにインターフェイスを取得できます。 

[EnumerateBreakpoints](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-enumeratebreakpoints)

EnumerateBreakpoints メソッドは、特定のスクリプト内で設定されているすべてのブレークポイントを列挙できる列挙子を返します。 

[GetEventFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-geteventfilter)

GetEventFilter メソッドは、特定のイベントの「中断イベント」が有効になっているかどうかを返します。 "Break イベントで"可能性があるイベントは ScriptDebugEventFilter 列挙体のメンバーについて説明します。 

[SetEventFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-seteventfilter)

SetEventFilter メソッドは、ScriptDebugEventFilter 列挙体のメンバーで定義されている特定のイベントの"break イベントで"動作を変更します。 GetEventFilter メソッドのドキュメントで使用可能なイベント (と、この列挙体の説明) の完全な一覧が見つかります。 

[StartDebugging](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-startdebugging)

StartDebugging メソッド「オン」の特定のスクリプト デバッガー。 デバッグの開始の act がいずれかの実行を積極的に発生しません区切りまたはステップ実行します。 だけ、により、スクリプトをデバッグできると、デバッグのインターフェイスと通信するクライアント用のインターフェイスのセットを提供します。 

[StopDebugging](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-stopdebugging)

StopDebugging メソッドは、デバッグを停止しようとするクライアントによって呼び出されます。 StartDebugging が正常に行われた後、任意の時点でこのメソッドの呼び出しを行った可能性があります (例: スクリプトの実行中に、中断などの中に.)。呼び出しはすぐに、すべてのデバッグ アクティビティと StartDebugging が呼び出される前に、状態がバックアップのリセットしなくなります。 


**デバッグのインターフェイス。IDataModelScriptDebugClient**

スクリプトのデバッグに関するインターフェイスを提供することを希望するデバッグ ホストまたはデバッガーのアプリケーションが StartDebugging メソッドのデバッグのインターフェイスを使用して、スクリプト デバッガー IDataModelScriptDebugClient インターフェイスの実装を提供する必要があります、スクリプトです。 

IDataModelScriptDebugClient は、するデバッグ イベントが渡され、コントロールがスクリプトの実行エンジンからデバッガー インターフェイスには、通信チャネルです。 これは、次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugClient, IUnknown)
{
   STDMETHOD(NotifyDebugEvent)(_In_ ScriptDebugEventInformation *pEventInfo, _In_ IDataModelScript *pScript, _In_opt_ IModelObject *pEventDataObject, _Inout_ ScriptExecutionKind *resumeEventKind) PURE;
}
```

[NotifyDebugEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugclient-notifydebugevent)

任意のイベントを発生すると、スクリプト デバッガーを中断する、デバッグ コード自体は NotifyDebugEvent メソッドを使用してインターフェイスへの呼び出しになります。 このメソッドは同期です。 インターフェイスは、イベントから戻るまで、スクリプトの実行は再開できなくします。 簡単なスクリプト デバッガーの定義が対象としています: 処理を必要とする完全になく入れ子になったイベントがあります。 デバッグ イベントは、ScriptDebugEventInformation と呼ばれるバリアント レコードによって定義されます。 DebugEvent メンバーによって、イベント情報が有効にするフィールドが定義されている大きくします。 ScriptDebugEvent 列挙体のメンバーによる記述で発生したイベントの種類を定義します。

**コール スタック:IDataModelScriptDebugStack**

スクリプト デバッガーを中断するイベントの発生時にデバッグのインターフェイスは中断場所の呼び出し履歴を取得するとします。 これは、GetStack メソッドを通じて実行されます。 このようなスタックは、次に示すように定義されている IDataModelScriptDebugStack を使用して表されます。 

複数のスクリプトやスクリプトの複数のプロバイダーに、全体的なスタックをまたがる可能性がありますに注意してください。 特定のスクリプトのデバッグのインターフェイスで GetStack メソッドに 1 回の呼び出しから返される呼び出し履歴では、そのスクリプトの境界内に呼び出し履歴のセグメントを返す必要がありますのみです。 スクリプトのデバッグ エンジンが、同じプロバイダーの 2 つのスクリプトの操作と複数のスクリプト コンテキストにまたがるように呼び出し履歴を取得できますがまったくことができます。 GetStack メソッドには、別のスクリプトでは、スタックの一部は返しません。 代わりに、このような状況を検出できる場合はスクリプトに境界フレームはスタック フレームする必要があります自体をスタック フレームの IsTransitionPoint と GetTransition メソッドの実装を使用して遷移フレームとしてマークします。 デバッガー インターフェイスはパノラマが存在する複数のスタック セグメントからの全体的なスタックが期待されます。 

遷移は、この方法で実装する必要がデバッグ インターフェイスに関しては、ローカル変数、パラメーター、ブレークポイント、示されている場合や不適切なスクリプト コンテキストに固有の他のスクリプトを構築します。 これにより、デバッガーのインターフェイスで未定義の動作が発生します。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugStack, IUnknown)
{
   STDMETHOD_(ULONG64, GetFrameCount)() PURE;
   STDMETHOD(GetStackFrame)(_In_ ULONG64 frameNumber, _COM_Outptr_ IDataModelScriptDebugStackFrame **stackFrame) PURE;
}
```

[GetFrameCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstack-getframecount)

GetFrameCount メソッドは、コール スタックのこのセグメントでは、スタック フレームの数を返します。 プロバイダーが別のスクリプト コンテキストで、または別のプロバイダーのフレームを検出できる場合をこのスタック セグメントのエントリのフレームの IsTransitionPoint と GetTransition メソッドの実装によって、呼び出し元に示してこのください。 

[GetStackFrame](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstack-getstackframe)

GetStackFrame は、履歴のセグメントから特定のスタック フレームを取得します。 コール スタックには、ゼロ ベースのインデックス作成システム: 中断イベントが発生した現在のスタック フレームは、フレーム 0。 現在のメソッドの呼び出し元は、(などの) フレーム 1 です。 


**発生した場合に状態を確認するには。IDataModelScriptDebugStackFrame**

ブレークが発生したスタック セグメントを表す IDataModelScriptDebugStack インターフェイスで GetStackFrame メソッドの呼び出しでは、スクリプト デバッガーに発生した場合に、コール スタックの特定のフレームを取得できます。 このフレームを表すために返される IDataModelScriptDebugStackFrame インターフェイスの定義は次のとおりです。

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugStackFrame, IUnknown)
{
   STDMETHOD(GetName)(_Out_ BSTR *name) PURE;
   STDMETHOD(GetPosition)(_Out_ ScriptDebugPosition *position, _Out_opt_ ScriptDebugPosition *positionSpanEnd, _Out_opt_ BSTR *lineText) PURE;
   STDMETHOD(IsTransitionPoint)(_Out_ bool *isTransitionPoint) PURE;
   STDMETHOD(GetTransition)(_COM_Outptr_ IDataModelScript **transitionScript, _Out_ bool *isTransitionContiguous) PURE;
   STDMETHOD(Evaluate)(_In_ PCWSTR pwszExpression, _COM_Outptr_ IModelObject **ppResult) PURE;
   STDMETHOD(EnumerateLocals)(_COM_Outptr_ IDataModelScriptDebugVariableSetEnumerator **variablesEnum) PURE;
   STDMETHOD(EnumerateArguments)(_COM_Outptr_ IDataModelScriptDebugVariableSetEnumerator **variablesEnum) PURE;
}
```

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-getname)

GetName メソッドは、表示名を返します (例:: 関数名) のこのフレーム。 デバッガー インターフェイスでユーザーに表示される stack backtrace 内で、このような名前が表示されます。 

[GetPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-getposition)

GetPosition メソッドは、スタック フレームによって表されるスクリプト内の位置を返します。 このメソッドは、スクリプトがこのフレームが含まれているスタックによって表される中断中にある場合にのみ呼び出すことがあります。 このフレーム内の行と列の位置は常に返されます。 デバッガーが、スクリプト内で「実行位置」の範囲を返すことができる場合は、終了位置を positionSpanEnd 引数で返されることができます。 デバッガーがこの機能でない場合 (要求) 場合は、スパンの最後の行と列の値を 0 に設定する必要があります。 

[IsTransitionPoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-istransitionpoint)

IDataModelScriptDebugStack インターフェイスは、呼び出し履歴 - 1 つのスクリプトのコンテキスト内に含まれている呼び出し履歴の部分のセグメントを表します。 デバッガーが別の 1 つのスクリプト (または別のスクリプトを 1 つのプロバイダー) からの移行を検出できる場合は、IsTransitionPoint メソッドを実装し、true または false として適切なを返すことによってこの示している可能性があります。 スクリプトを入力したセグメントが適用されるコール スタック フレームは遷移ポイントを検討してください。 その他のすべてのフレームにはできません。 

[GetTransition](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-gettransition)

特定のスタック フレームは遷移ポイント IsTransition メソッドによって決定される場合 (移行ポイントの定義については文書を参照)、GetTransition メソッドは、移行に関する情報を返します。 具体的には、このメソッドでは前のスクリプトにこの IDataModelScriptDebugStackFrame を含むスタック セグメントによって表されるスクリプトへの呼び出しを行った 1 つが返されます。 

[評価](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-evaluate)

Evaluate メソッドは、このメソッドが呼び出された対象 IDataModelScriptDebugStackFrame インターフェイスによって表されるスタック フレームのコンテキストで (スクリプトのプロバイダーの言語) の式を評価します。 式の評価の結果は、IModelObject としてスクリプト プロバイダーからマーシャ リングする必要があります。 プロパティと、結果として得られる IModelObject の他のコンストラクトのすべてをデバッガーが中断状態を取得することにある必要があります。 

[EnumerateLocals](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-enumeratelocals)

EnumerateLocals メソッドは、IDataModelScriptDebugStackFrame によって表されるスタック フレームのコンテキストでのスコープ内にあるすべてのローカル変数 (IDataModelScriptDebugVariableSetEnumerator インターフェイスによって表される) 変数セットを返しますこのメソッドが呼び出された対象インターフェイス。 

[EnumerateArguments](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-enumeratearguments)

EnumerateArguments メソッドは、IDataModelScriptDebugStackFrame によって表されるスタック フレームで呼び出される関数のすべての関数の引数 (IDataModelScriptDebugVariableSetEnumerator インターフェイスによって表される) 変数セットを返しますこのメソッドが呼び出された対象インターフェイス。 


**変数を見る。IDataModelScriptDebugVariableSetEnumerator**

デバッグ中のスクリプトで変数のセット (かどうかを特定のスコープ、関数のローカル変数、関数などの引数で) IDataModelScriptDebugVariableSetEnumerator インターフェイスを介して定義された変数のセットで表されます。

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugVariableSetEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_ BSTR *variableName, _COM_Outptr_opt_ IModelObject **variableValue, _COM_Outptr_opt_result_maybenull_ IKeyStore **variableMetadata) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugvariablesetenumerator-reset)

Reset メソッドに--作成後すぐには、セットの最初の要素の前に、列挙子の位置をリセットします。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugvariablesetenumerator-getnext)

GetNext メソッドは、列挙子をセットには、次の変数に移動し、変数の名前、値、およびそれに関連付けられたメタデータを返します。 列挙子には、セットの末尾がヒットした場合、エラー E_BOUNDS が返されます。 GetNext メソッドから返された E_BOUNDS マーカー E_BOUNDS リセットの中間の呼び出しが行われた場合を除き、もう一度呼び出されたときに生成するために続行されます。 


**ブレークポイント:IDataModelScriptDebugBreakpoint**

スクリプト ブレークポイントは、SetBreakpoint メソッドを使用して、指定されたスクリプトのデバッグのインターフェイスで設定されます。 このようなブレークポイントは、一意の id と次のように定義されている IDataModelScriptDebugBreakpoint インターフェイスの実装の両方によって表されます。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugBreakpoint, IUnknown)
{
    STDMETHOD_(ULONG64, GetId)() PURE;
    STDMETHOD_(bool, IsEnabled)() PURE;
    STDMETHOD_(void, Enable)() PURE;
    STDMETHOD_(void, Disable)() PURE;
    STDMETHOD_(void, Remove)() PURE;
    STDMETHOD(GetPosition)(_Out_ ScriptDebugPosition *position, _Out_opt_ ScriptDebugPosition *positionSpanEnd, _Out_opt_ BSTR *lineText) PURE;
}
```

[GetId](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-getid)

GetId メソッドは、ブレークポイントに、スクリプトのプロバイダーのデバッグ エンジンによって割り当てられた一意識別子を返します。 この識別子は、含んでいるスクリプトのコンテキスト内で一意である必要があります。 ブレークポイント識別子は、プロバイダーに一意である可能性があります。ただし、する必要はありません。 

[IsEnabled](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-isenabled)

IsEnabled メソッドは、ブレークポイントが有効になっているかどうかを返します。 無効なブレークポイントが存在し、スクリプト用のブレークポイントの一覧でも単なる「電源オフ、」一時的にします。 有効な状態ですべてのブレークポイントを作成する必要があります。 

[有効にします。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-enable)

有効にするメソッドでは、ブレークポイントを使用します。 ブレークポイントが無効になっている場合は、「このメソッドを呼び出した後、ブレークポイントに達する」と、デバッガーに中断が発生します。 

[無効にします。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-disable)

無効にするメソッドは、ブレークポイントを無効にします。 この呼び出しの後「このメソッドを呼び出した後、ブレークポイントに達する」がないデバッガーを中断します。 ブレークポイント、中に引き続き存在と見なされます「オフ」。 

[[削除]](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-remove)

Remove メソッドは、その一覧を含むからブレークポイントを削除します。 このメソッドが返された後に不要になった意味、ブレークポイントが存在します。 ブレークポイントを表さ IDataModelScriptDebugBreakpoint インターフェイスでは、呼び出しの後に孤立したと見なされます。 他に何も (法的に) 実行できますをリリースする以外には、この呼び出しの後。 

[GetPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-getposition)

GetPosition メソッドは、スクリプト内のブレークポイントの位置を返します。 スクリプト デバッガーは、行と列のソース コード内でブレークポイントがある場所を返す必要があります。 これを行う場合は、positionSpanEnd 引数によって定義されているように、終了位置情報を入力して、ブレークポイントによって表されるソースの範囲を返すこともできます。 場合は、デバッガーがこのスパンを生成できる、呼び出し元の要求は、0 とを示す値を提供することはできませんにスパンの終了位置の行と列のフィールドを入力する必要があります。 


**ブレークポイントの列挙体。IDataModelScriptDebugBreakpointEnumerator**

スクリプト プロバイダーでは、デバッグをサポートする場合、各スクリプトに関連付けられているすべてのブレークポイントの追跡し、デバッグ インターフェイスにこれらのブレークポイントの列挙に対応する必要があります。 ブレークポイントの列挙子は、指定されたスクリプトのデバッグのインターフェイスで EnumerateBreakpoints メソッド経由で取得され、次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugBreakpointEnumerator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptDebugBreakpoint **breakpoint) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpointenumerator-reset)

Reset メソッドは、列挙子--は、前に作成された最初の列挙されたブレークポイント直後後が、列挙子の位置をリセットします。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpointenumerator-getnext)

GetNext メソッドは、フォワードの列挙子を列挙するのには、次のブレークポイントに移動し、そのブレークポイントの IDataModelScriptDebugBreakpoint インターフェイスを返します。 列挙子は列挙体の末尾に達した、E_BOUNDS が返されます。 E_BOUNDS エラーが生成されて、GetNext メソッドの後続の呼び出しは、Reset メソッドを中間の呼び出しを行わない E_BOUNDS を生成するために続行されます。 





---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[デバッガー データ モデルの C++ の概要](data-model-cpp-overview.md)

[デバッガーのデータ モデルの C++ インターフェイス](data-model-cpp-interfaces.md)

[デバッガーのデータ モデルの C++ オブジェクト](data-model-cpp-objects.md)

[デバッガーのデータ モデルの C++ の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーのデータ モデルの C の概念](data-model-cpp-concepts.md)

[デバッガー データ モデルの C++ のスクリプト](data-model-cpp-scripting.md)
