---
title: Debugger Data Model C++ のスクリプト
description: このトピックでは、デバッガーエンジンを使用C++したオートメーションをサポートするために、デバッガーデータモデルのスクリプトを使用する方法について説明します。
ms.date: 09/12/2019
ms.openlocfilehash: 01fc05ad1e38564ddc8bf3851e4ecb1a78995915
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837802"
---
# <a name="debugger-data-model-c-scripting"></a>Debugger Data Model C++ のスクリプト

このトピックでは、デバッガーデータモデルC++デバッガーのデータモデルC++スクリプトを使用して、スクリプトを使用したデバッガーエンジンでオートメーションをサポートする方法について説明します。

## <a name="span-idscriptmanangement-script-management-in-the-debugger-data-model"></a>デバッガーデータモデルでのスクリプト管理の <span id="scriptmanangement"> 

データモデルマネージャーのロールは、オブジェクトの作成および拡張の中央の権限に加えて、スクリプトの抽象概念を管理する役割も担います。 データモデルマネージャーのスクリプトマネージャー部分の観点からは、スクリプトは動的に読み込まれ、アンロードされ、データモデルに新しい機能を提供するためにプロバイダーによってデバッグできる可能性があります。 

スクリプトプロバイダーは、データモデルに言語 (例: NatVis、JavaScript など) をブリッジするコンポーネントです。 " 1つ以上のファイル拡張子を登録します (例: ")。NatVis "," .js ")。このプロバイダーによって処理されるので、デバッガークライアントまたはユーザーインターフェイスを使用して、プロバイダーに委任することによって、その特定の拡張機能を持つスクリプトファイルを読み込むことができます。 

**コアスクリプトマネージャー: IDataModelScriptManager**

コアスクリプトマネージャーのインターフェイスは、次のように定義されています。 

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

[GetDefaultNameBinder](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-getdefaultnamebinder)

GetDefaultNameBinder メソッドは、データモデルの既定のスクリプト名バインダーを返します。 名前バインダーは、オブジェクトのコンテキスト内で名前を解決するコンポーネントです。 たとえば、式 "foo. bar" を指定した場合、オブジェクト foo のコンテキストで名前バーを解決するために、名前バインダーが呼び出されます。 ここで返されるバインダーは、データモデルの既定の規則のセットに従います。 スクリプトプロバイダーは、このバインダーを使用して、プロバイダー間での名前解決に一貫性を持たせることができます。 


[RegisterScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-registerscriptprovider)

RegisterScriptProvider メソッドは、新しい言語をデータモデルにブリッジングできる新しいスクリプトプロバイダーが存在することをデータモデルに通知します。 このメソッドが呼び出されると、スクリプトマネージャーは、指定されたスクリプトプロバイダーを直ちに呼び出し、それが管理するスクリプトのプロパティを照会します。 指定されたスクリプトプロバイダーによって示された名前またはファイル拡張子で既にプロバイダーが登録されている場合、このメソッドは失敗します。 特定の名前またはファイル拡張子のハンドラーとして登録できるスクリプトプロバイダーは1つだけです。 


[UnregisterScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-unregisterscriptprovider)

UnregisterScriptProvider メソッドは、RegisterScriptProvider メソッドの呼び出しを元に戻します。 Inpassed れたスクリプトプロバイダーによって指定された名前とファイル拡張子が関連付けられなくなります。 登録を解除した後でも、スクリプトプロバイダーへの未解決の COM 参照の数が多くなる可能性があることに注意してください。 このメソッドは、指定されたスクリプトプロバイダーが管理する型のスクリプトの読み込み/作成のみを防止します。 そのプロバイダーによって読み込まれたスクリプトがまだ読み込まれていない場合、またはデバッガー (またはデータモデル) のオブジェクトモデルを操作している場合は、これらの操作によってまだスクリプトが参照されている可能性があります。 スクリプト内の構造を直接参照するデータモデル、メソッド、またはオブジェクトが存在する場合があります。 スクリプトプロバイダーは、それを処理できるように準備する必要があります。 


[FindProviderForScriptType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-findproviderforscripttype)

FindProviderForScriptType メソッドは、スクリプトマネージャーで、このメソッドに示されているようなスクリプトの種類の文字列を持つプロバイダーを検索します。 見つからない場合、このメソッドは失敗します。それ以外の場合は、このようなスクリプトプロバイダーが呼び出し元に返されます。 


[列挙の Atescriptproviders](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-enumeratescriptproviders)

Enumerate Atescriptproviders メソッドは列挙子を返します。これは、事前に RegisterScriptProvider メソッドを呼び出して、スクリプトマネージャーに登録されているすべてのスクリプトプロバイダーを列挙します。 



**スクリプトプロバイダーの列挙: IDataModelScriptProviderEnumerator**

列挙体 Atescriptproviders メソッドは、次の形式の列挙子を返します。

```cpp 
DECLARE_INTERFACE_(IDataModelScriptProviderEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptProvider **provider) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptproviderenumerator-reset)

Reset メソッドは、列挙子を、最初の要素を返す前の位置に移動します。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptproviderenumerator-getnext)

GetNext メソッドは、列挙子を1つ前の要素に移動し、その要素にあるスクリプトプロバイダーを返します。 列挙子が列挙体の末尾に達すると、E_BOUNDS が返されます。 このエラーを受け取った後に GetNext メソッドを呼び出すと、E_BOUNDS が無期限に返されます。 



## <a name="span-idhostinterfacesscript-debugger-data-model-c-host-interfaces-for-scripting"></a>スクリプト用のデバッガー C++データモデルホストインターフェイスの <span id="hostinterfacesscript">

**スクリプトにおけるホストの役割**

デバッグホストは、デバッグターゲットの型システムの性質を理解し、そのデバッグターゲットの言語で式を評価するために、非常に低いレベルのインターフェイスを公開しています。通常、スクリプト作成のような高いレベルのコンストラクトは考慮されません。 このような機能は、デバッガー全体のアプリケーション、またはこれらの機能を提供する拡張機能に残されています。 ただし、これには例外があります。 データモデルによって提供されるスクリプト全体に参加する必要があるデバッグホストは、スクリプトにコンテキストを提供するためのいくつかの簡単なインターフェイスを実装する必要があります。 実際には、デバッグホストは、スクリプト環境がデータモデルの名前空間内で関数やその他のスクリプトによって提供される機能を配置する場所を制御します。 このプロセスに関与することにより、ホストは、式エバリュエーターなどのの機能を使用できるようになります。 ホストの観点から見たインターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDebugHostScriptHost | スクリプト環境に参加するデバッグホストの機能を示すインターフェイスです。 このインターフェイスを使用すると、オブジェクトの配置場所をスクリプトエンジンに通知するコンテキストを作成できます。
IDataModelScriptHostContext | スクリプトプロバイダーによってスクリプトの内容のコンテナーとして使用されるホストインターフェイス。 デバッガーアプリケーションのオブジェクトモデルに対して実行される操作以外のスクリプトサーフェイスの内容は、特定のデバッグホストによって異なります。 このインターフェイスにより、スクリプトプロバイダーは、コンテンツの配置場所に関する情報を取得できます。 詳細については、このトピックの後半の「[データモデルC++スクリプトインターフェイス](#scriptinterface)」を参照してください。


**デバッグホストのスクリプトホスト: IDebugHostScriptHost**

IDebugHostScriptHost インターフェイスは、新しく作成されたスクリプトのデバッグホストからコンテキストを取得するためにスクリプトプロバイダーによって使用されるインターフェイスです。 このコンテキストには、スクリプトプロバイダーがデータモデルとスクリプト環境の間にブリッジを配置できるオブジェクト (デバッグホストによって提供される) が含まれます。 たとえば、このようなブリッジは、スクリプト関数を呼び出すデータモデルメソッドである場合があります。 これにより、データモデル側の呼び出し元は、IModelMethod インターフェイスでの呼び出しメソッドの使用率によってスクリプトメソッドを呼び出すことができます。 

IDebugHostScriptHost インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDebugHostScriptHost, IUnknown)
{
    STDMETHOD(CreateContext)(_In_ IDataModelScript* script, _COM_Outptr_ IDataModelScriptHostContext** scriptContext) PURE;
}
```

[CreateContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostscripthost-createcontext)

CreateContext メソッドは、スクリプトの内容を格納する新しいコンテキストを作成するために、スクリプトプロバイダーによって呼び出されます。 このようなコンテキストは、[データモデルC++スクリプト作成インターフェイス] ページで詳しく説明されている IDataModelScriptHostContext インターフェイスによって表されます。 


## <a name="span-idscriptinterface-debugger-data-model-c-scripting-interfaces"></a><span id="scriptinterface"> デバッガーデータモデルC++のスクリプトインターフェイス

**スクリプトとスクリプトインターフェイス**

データモデルの全体的なアーキテクチャにより、サードパーティは、ある言語とデータモデルのオブジェクトモデルの間のブリッジを定義できます。 通常、データモデルの環境は非常に動的であるため、ブリッジされる言語はスクリプト言語です。 データモデルの言語とオブジェクトモデルとの間でこのブリッジを定義および実装するコンポーネントは、スクリプトプロバイダーと呼ばれます。 初期化されると、スクリプトプロバイダーは、データモデルマネージャーのスクリプトマネージャーの部分に自身を登録します。また、拡張機能を管理するインターフェイスでは、スクリプトの編集、読み込み、アンロード、および可能性のあるデバッグを行うことができます。スクリプトプロバイダーによって管理される言語に書き込まれます。 

Windows 用のデバッグツールでは、現在、2つのスクリプトプロバイダーが定義されています。

- NatVis プロバイダーです。 このプロバイダーは、NatVis XML とデータモデルの間に埋め込まれ、ネイティブ/言語データ型を視覚化できます。
- JavaScript プロバイダー。 このプロバイダーは、レガシデバッガー拡張機能 (JsProvider) に含まれています。 JavaScript 言語とデータモデルで記述されたスクリプト間でブリッジされるため、任意の形式のデバッガー制御と拡張が可能になります。

新しいプロバイダーを作成して、他の言語 (Python など) をデータモデルに渡すことができます。 このような場合は、現在、読み込みのためにレガシデバッガー拡張機能にカプセル化されます。 スクリプトプロバイダー自体は、レガシエンジンインターフェイスとの依存関係を最小限に抑え、可能な限りデータモデル Api を利用する必要があります。 これにより、プロバイダーを他の環境に移植可能にし、はるかに簡単にすることができます。

スクリプトプロバイダーに関連するインターフェイスには、2つのクラスがあります。 最初のインターフェイスのクラスは、スクリプトプロバイダーとそれらが管理するスクリプトの一般的な管理に使用されます。 2番目のインターフェイスのクラスは、スクリプトのデバッグをサポートするためのものです。 最初のセットのサポートは必須ですが、2番目のセットのサポートは省略可能であり、すべてのプロバイダーにとって意味がない可能性があります。 


一般的な管理インターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDataModelScriptProvider | スクリプトプロバイダーが実装する必要のあるコアインターフェイス。 これは、プロバイダーの特定の種類のスクリプトのサポートを提供し、特定のファイル拡張子に対して登録するために、データモデルマネージャーのスクリプトマネージャー部分に登録されているインターフェイスです。
IDataModelScript | プロバイダーによって管理されている特定のスクリプトの抽象化。 読み込まれた、または編集されている各スクリプトには、個別の IDataModelScript インスタンスがあります
IDataModelScriptClient | クライアントインターフェイス。情報をユーザーインターフェイスに伝達するために、スクリプトプロバイダーによって使用されます。 スクリプトプロバイダーは、このインターフェイスを実装していません。 スクリプトプロバイダーを使用する必要があるデータモデルをホストするアプリケーションでは、 スクリプトプロバイダーは、スクリプトクライアントのメソッドを呼び出して、ステータスやエラーなどを報告します。
IDataModelScriptHostContext | スクリプトプロバイダーによってスクリプトの内容のコンテナーとして使用されるホストインターフェイス。 デバッガーアプリケーションのオブジェクトモデルに対して実行される操作以外のスクリプトサーフェイスの内容は、特定のデバッグホストによって異なります。 このインターフェイスにより、スクリプトプロバイダーは、コンテンツの配置場所に関する情報を取得できます。
IDataModelScriptTemplate | スクリプトプロバイダーは、ユーザーがスクリプトを作成するための開始点として機能する1つ以上のテンプレートを提供できます。 組み込みエディターを提供するデバッガーアプリケーションは、このインターフェイスを通じてプロバイダーによって提供されるテンプレートコンテンツを使用して、新しいスクリプトに事前に入力できます。
IDataModelScriptTemplateEnumerator | サポートされているさまざまなテンプレートをすべてアドバタイズするためにスクリプトプロバイダーが実装する列挙子インターフェイス。
IDataModelNameBinder | 名前バインダー-コンテキスト内の名前を値に関連付けることができるオブジェクト。 "Foo. bar" などの特定の式の場合、名前バインダーはオブジェクト "foo" のコンテキストで名前 "bar" をバインドし、値または参照を生成できます。 名前バインダーは、通常、スクリプトプロバイダーによって実装されるわけではありません。代わりに、既定のバインダーをデータモデルから取得し、スクリプトプロバイダーで使用することができます。

デバッグインターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDataModelScriptDebug | スクリプトをデバッグできるようにするためにスクリプトプロバイダーが提供する必要のあるコアインターフェイス。 スクリプトがデバッグ可能な場合、IDataModelScript インターフェイスの実装クラスは IDataModelScriptDebug の QueryInterface を必要とします。
IDataModelScriptDebugClient | スクリプトデバッグ機能を提供するユーザーインターフェイスには、IDataModelScriptDebugClient インターフェイスが実装されています。 スクリプトプロバイダーは、このインターフェイスを使用してデバッグ情報を (たとえば、発生するイベントやブレークポイントなどの) 相互に渡します。
IDataModelScriptDebugStack | スクリプトプロバイダーは、このインターフェイスを実装して、呼び出し履歴の概念をスクリプトデバッガーに公開します。
IDataModelScriptDebugStackFrame | スクリプトプロバイダーは、このインターフェイスを実装して、呼び出し履歴内の特定のスタックフレームの概念を公開します。
IDataModelScriptDebugVariableSetEnumerator | スクリプトプロバイダーは、一連の変数を公開するために、このインターフェイスを実装します。 このセットは、関数に対する一連のパラメーター、ローカル変数のセット、または特定のスコープ内の変数のセットを表すことができます。 正確な意味は、インターフェイスの取得方法によって異なります。
IDataModelScriptDebugBreakpoint | スクリプトプロバイダーは、スクリプト内の特定のブレークポイントの概念を公開するために、このインターフェイスを実装します。
IDataModelScriptDebugBreakpointEnumerator | スクリプトプロバイダーはこれを実装して、スクリプト内に現在存在するすべてのブレークポイント (有効かどうか) を列挙します。

**コアスクリプトプロバイダー: IDataModelScriptProvider**

スクリプトプロバイダーにする拡張機能では、IDataModelScriptProvider インターフェイスの実装を提供し、RegisterScriptProvider メソッドを介してデータモデルマネージャーのスクリプトマネージャー部分に登録する必要があります。 実装する必要があるこのコアインターフェイスは、次のように定義されています。

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

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getname)

GetName メソッドは、プロバイダーが SysAllocString メソッドを介して割り当てられた文字列として管理する、(または言語の) スクリプトの型の名前を返します。 呼び出し元は、返された文字列を SysFreeString を使用して解放する役割を担います。 このメソッドから返される可能性がある文字列の例としては、"JavaScript" または "NatVis" があります。 返される文字列は、データモデルをホストしているデバッガーアプリケーションのユーザーインターフェイスに表示される可能性があります。 2つのスクリプトプロバイダーが同じ名前を返すことはできません (大文字と小文字は区別されません)。 

[GetExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getextension)

GetExtension メソッドは、SysAllocString メソッドを使用して割り当てられた文字列として、このプロバイダーによって管理されるスクリプト (ドットなし) のファイル拡張子を返します。 (スクリプトサポートを使用して) データモデルをホストするデバッガーアプリケーションは、この拡張機能を持つスクリプトファイルをスクリプトプロバイダーに委任します。 呼び出し元は、返された文字列を SysFreeString を使用して解放する役割を担います。 このメソッドから返される可能性がある文字列の例としては、"js" または "NatVis" があります。 

[CreateScript](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-createscript)

CreateScript メソッドは、新しいスクリプトを作成するために呼び出されます。 スクリプトプロバイダーは、このメソッドが呼び出されるたびに、返された IDataModelScript インターフェイスによって表される新しい空のスクリプトを返す必要があります。 このメソッドは、ユーザーインターフェイスがユーザーによる編集用に新しい空のスクリプトを作成しているかどうか、またはデバッガーアプリケーションがディスクからスクリプトを読み込んでいるかどうかに関係なく呼び出されることに注意してください。 プロバイダーは、ファイル i/o には関与しません。 これは、IDataModelScript のメソッドに渡されたストリームを介してホストアプリケーションからの要求を処理するだけです。 

[GetDefaultTemplateContent](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getdefaulttemplatecontent)

GetDefaultTemplateContent メソッドは、プロバイダーの既定のテンプレートコンテンツのインターフェイスを返します。 これは、新しく作成されたスクリプトの編集ウィンドウにあらかじめ設定されているスクリプトプロバイダーのコンテンツです。 スクリプトプロバイダーにテンプレートがない場合 (または既定のコンテンツとして指定されているテンプレートコンテンツがない場合)、スクリプトプロバイダーはこのメソッドから E_NOTIMPL を返すことがあります。 

[EnumerateTemplates](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-enumeratetemplates)

EnumerateTemplates メソッドは、スクリプトプロバイダーによって提供されるさまざまなテンプレートを列挙できる列挙子を返します。 テンプレートコンテンツとは、新しいスクリプトを作成するときに、スクリプトプロバイダーが編集ウィンドウに "事前" することです。 複数の異なるテンプレートがサポートされている場合、それらのテンプレートに名前を付けることができます (例: "命令型スクリプト"、"拡張スクリプト")。また、データモデルをホストするデバッガーアプリケーションは、"テンプレート" をユーザーに提示する方法を選択できます。 


**コアスクリプトインターフェイス: IDataModelScript**

プロバイダーによって実装される個々のスクリプトを管理するメインインターフェイスは、IDataModelScript インターフェイスです。 このインターフェイスを実装するコンポーネントは、クライアントが新しい空のスクリプトを作成し、IDataModelScriptProvider で CreateScript メソッドを呼び出す場合に返されます。 

プロバイダーによって作成される各スクリプトは、独立したサイロに存在する必要があります。 1つのスクリプトが別のスクリプトに影響を与えないようにする必要があります。ただし、データモデルを介した外部オブジェクトとの明示的な相互作用は除きます。 たとえば、2つのスクリプトを使用すると、いくつかの型または概念を拡張できます (たとえば、デバッガーがプロセスの概念を示します)。 どちらのスクリプトも、外部プロセスオブジェクトを介して、互いのフィールドにアクセスできます。 

このインターフェイスは、次のように定義されています。 

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

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-getname)

GetName メソッドは、SysAllocString 関数を使用して、スクリプトの名前を割り当てられた文字列として返します。 スクリプトに名前がまだない場合、メソッドは null BSTR を返す必要があります。 この状況では失敗しません。 Rename メソッドの呼び出しによってスクリプトが明示的に名前変更された場合、GetName メソッドは、新しく割り当てられた名前を返す必要があります。 

[リネーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-rename)

Rename メソッドを指定すると、新しい名前がスクリプトに割り当てられます。 この名前を保存し、GetName メソッドの呼び出し時に返すのは、スクリプト実装の役割です。 これは、ユーザーインターフェイスが新しい名前にスクリプトとして保存することを選択したときにしばしば呼び出されます。 スクリプトの名前を変更すると、スクリプトの内容をホストするアプリケーションが選択する場所に影響することがあります。 

[事前](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-populate)

設定メソッドは、スクリプトの "コンテンツ" を変更または同期するために、クライアントによって呼び出されます。 スクリプトのコードが変更されたことをスクリプトプロバイダーに通知します。 このメソッドでは、スクリプトの実行や、スクリプトによって操作されるオブジェクトへの変更は行われないことに注意する必要があります。 これは、スクリプトの内容が変更され、独自の内部状態を同期できるように、スクリプトプロバイダーへの通知にすぎません。 

[おい](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-execute)

Execute メソッドは、最後に成功した設定呼び出しによって示されたとおりにスクリプトの内容を実行し、そのコンテンツに従ってデバッガーのオブジェクトモデルを変更します。 言語 (またはスクリプトプロバイダー) で "main 関数" が定義されている場合 (つまり、ユーザーインターフェイスの架空の "スクリプトの実行" ボタンをクリックしたときに作成者が呼び出す必要のある "main 関数") は、実行操作中に呼び出されません。 実行操作は、初期化とオブジェクトモデルの操作のみを実行することを検討できます (例: ルートコードの実行と拡張ポイントの設定)。 

[埋め](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-unlink)

Unlink メソッドは、実行操作を元に戻します。 スクリプトの実行中に確立されたオブジェクトモデルの操作または拡張ポイントは、すべて元に戻されます。 リンク解除操作の後、スクリプトは Execute を呼び出すことによって再実行されるか、または解放される可能性があります。 

[IsInvocable](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-isinvocable)

IsInvocable メソッドは、スクリプトが invocable であるかどうかを返します。つまり、言語またはプロバイダーによって定義された "main 関数" があるかどうかを示します。 このような "main 関数" は、ユーザーインターフェイスで "スクリプトを実行する" という架空のボタンが押された場合にスクリプト作成者が呼び出すものです。 

[InvokeMain](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-invokemain)

UI 呼び出しから実行することを意図した "main 関数" がスクリプトに含まれている場合は、IsInvocable メソッドからの真の戻り値を使用していることを示します。 ユーザーインターフェイスは、InvokeMain メソッドを呼び出してスクリプトを実際に "呼び出す" ことができます。 これは、すべてのルートコードを実行し、基になるホストの名前空間にスクリプトをブリッジする*Execute*とは異なります。 


\* * スクリプトクライアント: IDataModelScriptClient * *

スクリプトの管理を必要とするデータモデルをホストするアプリケーションが、この概念の周囲にユーザーインターフェイス (グラフィカルまたはコンソールであるかどうか) を持つアプリケーションは、IDataModelScriptClient インターフェイスを実装します。 このインターフェイスは、実行中または呼び出し中にスクリプトプロバイダーに渡されるか、またはエラーとイベントの情報をユーザーインターフェイスに渡すためにスクリプトで渡されます。 

IDataModelScriptClient インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptClient, IUnknown)
{
   STDMETHOD(ReportError)(_In_ ErrorClass errClass, _In_ HRESULT hrFail, _In_opt_ PCWSTR message, _In_ ULONG line, _In_ ULONG position) PURE;
}
```

[ReportError](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptclient-reporterror)

スクリプトの実行中または呼び出し中にエラーが発生した場合、スクリプトプロバイダーは ReportError メソッドを呼び出して、エラーのユーザーインターフェイスを通知します。 


**スクリプトのホストコンテキスト: IDataModelScriptHostContext**

デバッグホストは、データモデルのスクリプトコンテンツを射影する方法と場所に影響を与えます。 各スクリプトは、ブリッジをスクリプトに配置するコンテキスト (たとえば、呼び出すことができる関数オブジェクトなど) をホストに要求することが想定されています。このコンテキストは、IDebugHostScriptHost で CreateContext メソッドを呼び出し、IDataModelScriptHostContext を取得することによって取得します。 

IDataModelScriptHostContext インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptHostContext, IUnknown)
{
   STDMETHOD(NotifyScriptChange)(_In_ IDataModelScript* script, _In_ ScriptChangeKind changeKind) PURE;
   STDMETHOD(GetNamespaceObject)(_COM_Outptr_ IModelObject** namespaceObject) PURE;
}
```

[NotifyScriptChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripthostcontext-notifyscriptchange)

スクリプトプロバイダーは、関連付けられたコンテキストでの NotifyScriptChange メソッドへのメソッド呼び出しで発生する特定の操作について、デバッグホストに通知する必要があります。 このような操作は、ScriptChangeKind 列挙型のメンバーとして定義されます。

[GetNamespaceObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripthostcontext-getnamespaceobject)

GetNamespaceObject メソッドは、スクリプトプロバイダーがデータモデルとスクリプトの間にブリッジを配置できるオブジェクトを返します。 ここでは、スクリプトプロバイダーが、スクリプト内で対応する名前付き関数への呼び出しを行うデータモデルメソッドオブジェクト (IModelObject にボックス化された IModelMethod インターフェイス) を配置する場合があります。 


**新しく作成されたスクリプトのテンプレート: IDataModelScriptTemplate**

新しいスクリプトに対して事前に入力されたコンテンツを表示するスクリプトプロバイダー (例: デバッガーユーザーインターフェイスでスクリプトを記述するユーザーを支援するため) は、1つまたは複数のスクリプトテンプレートを指定することによってこれを行うことができます。 このようなテンプレートは、IDataModelScriptTemplate インターフェイスを実装するコンポーネントであり、スクリプトプロバイダーの GetDefaultTemplate メソッドまたは EnumerateTemplates メソッドを介して返されます。 

IDataModelScriptTemplate インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptTemplate, IUnknown)
{
   STDMETHOD(GetName)(_Out_ BSTR *templateName) PURE;
   STDMETHOD(GetDescription)(_Out_ BSTR *templateDescription) PURE;
   STDMETHOD(GetContent)(_COM_Outptr_ IStream **contentStream) PURE;
}
```


[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getname)

GetName メソッドは、テンプレートの名前を返します。 テンプレートに名前がない場合、この処理は E_NOTIMPL で失敗する可能性があります。 単一の既定のテンプレート (存在する場合) に名前を付ける必要はありません。 その他のテンプレートはすべてです。 これらの名前は、作成するテンプレートを選択するためのメニューの一部としてユーザーインターフェイスに表示される場合があります。 


[GetDescription](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getdescription)

GetDescription メソッドは、テンプレートの説明を返します。 このような説明は、ユーザーがテンプレートで実行するように設計されている内容を理解するのに役立つ、よりわかりやすいインターフェイスでユーザーに表示されます。 テンプレートに説明がない場合は、このメソッドから E_NOTIMPL が返されることがあります。 

[GetContent](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getcontent)

GetContent メソッドは、テンプレートのコンテンツ (またはコード) を返します。 これは、ユーザーがこのテンプレートから新しいスクリプトを作成することを選択した場合に、編集ウィンドウに事前に入力されます。 このテンプレートは、クライアントがプルできるコンテンツに対して標準ストリームを作成して返す役割を担います。 

**プロバイダーのテンプレートコンテンツの列挙体: IDataModelScriptTemplateEnumerator**

スクリプトプロバイダーは、いくつかのユーザーインターフェイスで、新しく作成されたスクリプトにコンテンツを事前に入力する1つ以上のテンプレートを提供できます。 これらのテンプレートのいずれかが指定されている場合、スクリプトプロバイダーは、EnumerateTemplates メソッドの呼び出し時に返される列挙子を実装する必要があります。 

この列挙子は、IDataModelScriptTemplateEnumerator インターフェイスの実装であり、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptTemplateEnumerator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptTemplate **templateContent) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplateenumerator-reset)

Reset メソッドは、最初に作成されたときの位置 (最初のテンプレートが生成される前) に列挙子をリセットします。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplateenumerator-getnext)

GetNext メソッドは、列挙子を次のテンプレートに移動し、それを返します。 列挙型の末尾で、列挙子は E_BOUNDS を返します。 E_BOUNDS マーカーがヒットすると、列挙子はリセット呼び出しが行われるまで、E_BOUNDS エラーを無期限に生成し続けます。 


**名前の意味の解決: IDataModelNameBinder**

データモデルは、さまざまなスクリプトプロバイダーで動作する特定のコンテキストでの特定の名前の意味をスクリプトプロバイダーが決定するための標準的な方法を提供します (例: foo. bar の棒の意味を特定する)。 このメカニズムは、名前バインダーと呼ばれ、IDataModelNameBinder インターフェイスによって表されます。 このようなバインダーは、名前がどのように解決されるか、および名前がオブジェクトに対して複数回定義されている競合解決を処理する方法に関する一連の規則をカプセル化します。 これらのルールの一部には、(データモデルによって追加された) 投影された名前がネイティブ名 (デバッグ対象の言語の型システムに含まれる) に対して解決される方法などが含まれます。 

スクリプトプロバイダー間で一貫性を確保するために、データモデルのスクリプトマネージャーには既定の名前バインダー ' が用意されています。 この既定の名前は、IDataModelScriptManager インターフェイスの GetDefaultNameBinder メソッドを呼び出すことによって取得できます。 Name binder インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDataModelNameBinder, IUnknown)
{
   STDMETHOD(BindValue)(_In_ IModelObject* contextObject, _In_ PCWSTR name, _COM_Errorptr_ IModelObject** value, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(BindReference)(_In_ IModelObject* contextObject, _In_ PCWSTR name, _COM_Errorptr_ IModelObject** reference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(EnumerateValues)(_In_ IModelObject* contextObject, _COM_Outptr_ IKeyEnumerator** enumerator) PURE;
   STDMETHOD(EnumerateReferences)(_In_ IModelObject* contextObject, _COM_Outptr_ IKeyEnumerator** enumerator) PURE;
}
```

[BindValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelnamebinder-bindvalue)

BindValue メソッドは、一連のバインド規則に従って、指定されたオブジェクトの contextObject.name に相当するものを実行します。 このバインディングの結果は値になります。 値として、基になるスクリプトプロバイダーは、値を使用して名前に割り当てを戻すことはできません。

[BindReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelnamebinder-bindreference)

BindReference メソッドは Bindreference に似ています。これは、一連のバインド規則に従って、指定されたオブジェクトで contextObject.name と同等のものを実行するという点です。 ただし、このメソッドからのバインディングの結果は、値ではなく参照になります。 参照として、スクリプトプロバイダーは参照を利用して、名前に割り当てを戻すことができます。 

[EnumerateValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelnamebinder-enumeratevalues)

EnumerateValues メソッドは、BindValue メソッドの規則に従ってオブジェクトにバインドされる名前と値のセットを列挙します。 IModelObject の EnumerateKeys、EnumerateValues、および類似のメソッドとは異なり、同じ値 (基底クラス、親モデル、および like) を持つ複数の名前を返すことがあります。この列挙子は、バインドされる名前の特定のセットのみを返します。BindValue と Bindvalue。 名前は複製されません。 IModelObject メソッドを呼び出すよりも、名前バインダーを使用してオブジェクトを列挙すると、非常に高いコストが発生することに注意してください。 

[EnumerateReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelnamebinder-enumeratereferences)

EnumerateReferences メソッドは、BindReference メソッドの規則に従ってオブジェクトにバインドする名前と参照のセットを列挙します。 IModelObject の EnumerateKeys、EnumerateValues、および類似のメソッドとは異なり、同じ値 (基底クラス、親モデル、および like) を持つ複数の名前を返すことがあります。この列挙子は、バインドされる名前の特定のセットのみを返します。BindValue と Bindvalue。 名前は複製されません。 IModelObject メソッドを呼び出すよりも、名前バインダーを使用してオブジェクトを列挙すると、非常に高いコストが発生することに注意してください。 


## <a name="span-iddebugscript-debugger-data-model-c-script-debugging-interfaces"></a><span id="debugscript"> デバッガーデータモデルC++スクリプトデバッグインターフェイス

データモデルのスクリプトプロバイダーのインフラストラクチャでは、スクリプトのデバッグに関する概念も提供されます。 デバッグ機能をデバッグホストおよびデータモデルをホストするデバッガーアプリケーションに公開するスクリプトでは、IDataModelScript インターフェイスに加えて、デバッグ可能なスクリプトによって IDataModelScriptDebug インターフェイスが実装されます。 このインターフェイスがスクリプトに存在することは、デバッグ可能であることをインフラストラクチャに示しています。 

IDataModelScriptDebug インターフェイスは、スクリプトプロバイダーのデバッグ機能にアクセスするための開始点ですが、デバッグ機能全体を提供する他のインターフェイスのセットによって結合されます。 

デバッグインターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDataModelScriptDebug | スクリプトをデバッグできるようにするためにスクリプトプロバイダーが提供する必要のあるコアインターフェイス。 スクリプトがデバッグ可能な場合、IDataModelScript インターフェイスの実装クラスは IDataModelScriptDebug の QueryInterface を必要とします。
IDataModelScriptDebugClient | スクリプトデバッグ機能を提供するユーザーインターフェイスには、IDataModelScriptDebugClient インターフェイスが実装されています。 スクリプトプロバイダーは、このインターフェイスを使用してデバッグ情報を (たとえば、発生するイベントやブレークポイントなどの) 相互に渡します。
IDataModelScriptDebugStack | スクリプトプロバイダーは、このインターフェイスを実装して、呼び出し履歴の概念をスクリプトデバッガーに公開します。
IDataModelScriptDebugStackFrame | スクリプトプロバイダーは、このインターフェイスを実装して、呼び出し履歴内の特定のスタックフレームの概念を公開します。
IDataModelScriptDebugVariableSetEnumerator | スクリプトプロバイダーは、一連の変数を公開するために、このインターフェイスを実装します。 このセットは、関数に対する一連のパラメーター、ローカル変数のセット、または特定のスコープ内の変数のセットを表すことができます。 正確な意味は、インターフェイスの取得方法によって異なります。
IDataModelScriptDebugBreakpoint | スクリプトプロバイダーは、スクリプト内の特定のブレークポイントの概念を公開するために、このインターフェイスを実装します。
IDataModelScriptDebugBreakpointEnumerator | スクリプトプロバイダーはこれを実装して、スクリプト内に現在存在するすべてのブレークポイント (有効かどうか) を列挙します。

一般的な管理インターフェイスは次のとおりです。 

インターフェイス | 説明
|---------|------------|
IDataModelScriptProvider | スクリプトプロバイダーが実装する必要のあるコアインターフェイス。 これは、プロバイダーの特定の種類のスクリプトのサポートを提供し、特定のファイル拡張子に対して登録するために、データモデルマネージャーのスクリプトマネージャー部分に登録されているインターフェイスです。
IDataModelScript | プロバイダーによって管理されている特定のスクリプトの抽象化。 読み込まれた、または編集されている各スクリプトには、個別の IDataModelScript インスタンスがあります
IDataModelScriptClient | クライアントインターフェイス。情報をユーザーインターフェイスに伝達するために、スクリプトプロバイダーによって使用されます。 スクリプトプロバイダーは、このインターフェイスを実装していません。 スクリプトプロバイダーを使用する必要があるデータモデルをホストするアプリケーションでは、 スクリプトプロバイダーは、スクリプトクライアントのメソッドを呼び出して、ステータスやエラーなどを報告します。
IDataModelScriptHostContext | スクリプトプロバイダーによってスクリプトの内容のコンテナーとして使用されるホストインターフェイス。 デバッガーアプリケーションのオブジェクトモデルに対して実行される操作以外のスクリプトサーフェイスの内容は、特定のデバッグホストによって異なります。 このインターフェイスにより、スクリプトプロバイダーは、コンテンツの配置場所に関する情報を取得できます。
IDataModelScriptTemplate | スクリプトプロバイダーは、ユーザーがスクリプトを作成するための開始点として機能する1つ以上のテンプレートを提供できます。 組み込みエディターを提供するデバッガーアプリケーションは、このインターフェイスを通じてプロバイダーによって提供されるテンプレートコンテンツを使用して、新しいスクリプトに事前に入力できます。
IDataModelScriptTemplateEnumerator | サポートされているさまざまなテンプレートをすべてアドバタイズするためにスクリプトプロバイダーが実装する列挙子インターフェイス。
IDataModelNameBinder | 名前バインダー-コンテキスト内の名前を値に関連付けることができるオブジェクト。 "Foo. bar" などの特定の式の場合、名前バインダーはオブジェクト "foo" のコンテキストで名前 "bar" をバインドし、値または参照を生成できます。 名前バインダーは、通常、スクリプトプロバイダーによって実装されるわけではありません。代わりに、既定のバインダーをデータモデルから取得し、スクリプトプロバイダーで使用することができます。


**スクリプトをデバッグ可能にする: IDataModelScriptDebug**

デバッグ可能なすべてのスクリプトは、IDataModelScript を実装する同じコンポーネントに IDataModelScriptDebug インターフェイスが存在することによってこの機能を示します。 デバッグホストまたはデータモデルをホストするデバッガーアプリケーションによるこのインターフェイスのクエリは、デバッグ機能の有無を示します。 

IDataModelScriptDebug インターフェイスは、次のように定義されています。 

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

[GetDebugState](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getdebugstate)

GetDebugState メソッドは、スクリプトの現在の状態 (実行中であるかどうかなど) を返します。 状態は、ScriptDebugState 列挙内の値によって定義されます。

[GetCurrentPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getcurrentposition)

GetCurrentPosition ' メソッドは、スクリプト内の現在位置を返します。 これは、GetScriptState の呼び出しが ScriptDebugBreak を返すデバッガーにスクリプトが分割されている場合にのみ呼び出すことができます。 このメソッドの他の呼び出しは無効であるため、失敗します。 

[GetStack](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getstack)

GetStack メソッドは、ブレーク位置で現在の呼び出し履歴を取得します。 このメソッドは、スクリプトがデバッガーに分割されている場合にのみ呼び出すことができます。 

[SetBreakpoint ポイント](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-setbreakpoint)

SetBreakpoint ポイントメソッドは、スクリプト内にブレークポイントを設定します。 実装では、inpassed れた行と列の位置を自由に調整して、適切なコード位置に移動することに注意してください。 ブレークポイントが配置された実際の行番号と列番号は、返された IDataModelScriptDebugBreakpoint インターフェイスのメソッド呼び出しによって取得できます。 

[FindBreakpointById](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-findbreakpointbyid)

SetBreakpoint ポイントメソッドを使用してスクリプト内に作成された各ブレークポイントには、実装によって一意の識別子 (64 ビット符号なし整数) が割り当てられます。 FindBreakpointById メソッドは、指定された識別子からブレークポイントへのインターフェイスを取得するために使用されます。 

[EnumerateBreakpoints](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-enumeratebreakpoints)

EnumerateBreakpoints メソッドは、特定のスクリプト内に設定されているすべてのブレークポイントを列挙できる列挙子を返します。 

[GetEventFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-geteventfilter)

GetEventFilter メソッドは、特定のイベントに対して "イベントの中断" が有効になっているかどうかを返します。 "イベントの中断" が発生する可能性のあるイベントは、ScriptDebugEventFilter 列挙体のメンバーによって記述されます。 

[SetEventFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-seteventfilter)

SetEventFilter メソッドは、ScriptDebugEventFilter 列挙体のメンバーによって定義された特定のイベントの "イベントの中断" 動作を変更します。 使用可能なイベント (およびこの列挙の説明) の完全な一覧については、GetEventFilter メソッドのドキュメントを参照してください。 

[StartDebugging](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-startdebugging)

StartDebugging メソッドは、特定のスクリプトに対してデバッガーを "オン" にします。 デバッグを開始する操作によって、実行の中断またはステップ実行がアクティブになることはありません。 スクリプトのデバッグが可能になるだけでなく、クライアントがデバッグインターフェイスと通信するための一連のインターフェイスが用意されています。 

[StopDebugging](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-stopdebugging)

StopDebugging メソッドは、デバッグを停止するクライアントによって呼び出されます。 このメソッドの呼び出しは、StartDebugging が正常に行われた後の任意の時点で実行できます (例: 中断中、スクリプトの実行中など)。この呼び出しは、すべてのデバッグアクティビティを直ちに停止し、StartDebugging が呼び出される前に状態をにリセットします。 


**デバッグインターフェイス: IDataModelScriptDebugClient**

スクリプトデバッグのためのインターフェイスを提供する必要があるデバッグホストまたはデバッガーアプリケーションは、デバッグインターフェイスの StartDebugging メソッドを使用してスクリプトデバッガーに IDataModelScriptDebugClient インターフェイスを実装する必要があります。小. 

IDataModelScriptDebugClient は、デバッグイベントが渡され、制御がスクリプト実行エンジンからデバッガーインターフェイスに送られる通信チャネルです。 これは次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugClient, IUnknown)
{
   STDMETHOD(NotifyDebugEvent)(_In_ ScriptDebugEventInformation *pEventInfo, _In_ IDataModelScript *pScript, _In_opt_ IModelObject *pEventDataObject, _Inout_ ScriptExecutionKind *resumeEventKind) PURE;
}
```

[NotifyDebugEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugclient-notifydebugevent)

スクリプトデバッガーに分割されたイベントが発生するたびに、デバッグコード自体が NotifyDebugEvent メソッドを使用してインターフェイスを呼び出します。 このメソッドは同期的です。 インターフェイスがイベントから戻るまで、スクリプトの実行は再開されません。 スクリプトデバッガーの定義は単純であることを意図しています。処理を必要とする入れ子になったイベントはまったく存在しません。 デバッグイベントは、ScriptDebugEventInformation と呼ばれるバリアントレコードによって定義されます。 イベント情報のどのフィールドが有効であるかは、DebugEvent メンバーによって主に定義されます。 これは、ScriptDebugEvent 列挙体のメンバーによって記述されたイベントの種類を定義します。

**呼び出し履歴: IDataModelScriptDebugStack**

スクリプトデバッガーに分割されたイベントが発生すると、デバッグインターフェイスは中断位置の呼び出し履歴を取得します。 これは、GetStack メソッドを使用して行います。 このようなスタックは、次に示すように定義されている IDataModelScriptDebugStack を使用して表されます。 

全体のスタックは複数のスクリプトまたは複数のスクリプトプロバイダーにまたがる場合があることに注意してください。 特定のスクリプトのデバッグインターフェイスで GetStack メソッドの1回の呼び出しから返される呼び出し履歴は、そのスクリプトの境界内の呼び出し履歴のセグメントのみを返す必要があります。 同じプロバイダーの2つのスクリプトが相互作用する場合、スクリプトデバッグエンジンは、複数のスクリプトコンテキストにわたって呼び出し履歴を取得できます。 GetStack メソッドは、別のスクリプト内のスタックの一部を返すことはできません。 このような状況が検出された場合、スクリプトの境界フレームであるスタックフレームは、そのスタックフレームの IsTransitionPoint メソッドと GetTransition メソッドの実装を通じて、そのスタックフレームを遷移フレームとしてマークする必要があります。 デバッガーインターフェイスは、存在する複数のスタックセグメントからスタック全体をつなぎ合わせることが想定されています。 

遷移はこのように実装する必要があります。または、デバッグインターフェイスがローカル変数、パラメーター、ブレークポイント、およびその他のスクリプト固有の構造に関する直接の問い合わせを間違ったスクリプトコンテキストに対して行う可能性があります。 これにより、デバッガーインターフェイスで未定義の動作が発生します。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugStack, IUnknown)
{
   STDMETHOD_(ULONG64, GetFrameCount)() PURE;
   STDMETHOD(GetStackFrame)(_In_ ULONG64 frameNumber, _COM_Outptr_ IDataModelScriptDebugStackFrame **stackFrame) PURE;
}
```

[GetFrameCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstack-getframecount)

GetFrameCount メソッドは、呼び出し履歴のこのセグメントに含まれるスタックフレームの数を返します。 プロバイダーが異なるスクリプトコンテキストまたは異なるプロバイダーのフレームを検出できる場合は、このスタックセグメントにエントリフレームの IsTransitionPoint メソッドと GetTransition メソッドを実装することによって、呼び出し元に対してこれを示す必要があります。 

[GetStackFrame](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstack-getstackframe)

GetStackFrame は、スタックセグメントから特定のスタックフレームを取得します。 呼び出し履歴には0から始まるインデックスシステムがあります。中断イベントが発生した現在のスタックフレームはフレーム0です。 現在のメソッドの呼び出し元は、フレーム 1 (など) です。 


**中断された状態の検査: IDataModelScriptDebugStackFrame**

スクリプトデバッガーに分割されたときのコールスタックの特定のフレームは、中断が発生したスタックセグメントを表す IDataModelScriptDebugStack インターフェイスの GetStackFrame メソッドを呼び出すことによって取得できます。 このフレームを表すために返される IDataModelScriptDebugStackFrame インターフェイスは、次のように定義されます。

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

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-getname)

GetName メソッドは、このフレームの表示名 (例: 関数名) を返します。 このような名前は、デバッガーインターフェイスでユーザーに表示されるスタックバックトレース内に表示されます。 

[GetPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-getposition)

GetPosition メソッドは、スタックフレームによって表されるスクリプト内の位置を返します。 このメソッドを呼び出すことができるのは、スクリプトがこのフレームが含まれているスタックで表された中断内にある場合のみです。 このフレーム内の行と列の位置は常に返されます。 デバッガーがスクリプト内の "実行位置" の範囲を返すことができる場合は、positionSpanEnd 引数で終了位置を返すことができます。 デバッガーがこの機能に対応していない場合は、スパンエンド内の行と列の値 (要求された場合) を0に設定する必要があります。 

[IsTransitionPoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-istransitionpoint)

IDataModelScriptDebugStack インターフェイスは、呼び出し履歴のセグメントを表します。この部分は、1つのスクリプトのコンテキスト内に含まれています。 デバッガーが、あるスクリプトから別のスクリプト (または1つのスクリプトプロバイダー) への遷移を検出できる場合は、IsTransitionPoint メソッドを実装し、必要に応じて true または false を返すことによってこれを示すことができます。 セグメントが適用されるスクリプトに入力された呼び出し履歴フレームは、遷移ポイントと見なす必要があります。 その他のすべてのフレームは、ではありません。 

[GetTransition](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-gettransition)

特定のスタックフレームが、IsTransition メソッドによって決定された遷移ポイント (遷移ポイントの定義のドキュメントを参照) である場合、GetTransition メソッドは遷移に関する情報を返します。 特に、このメソッドは、前のスクリプトを返します。このスクリプトは、この IDataModelScriptDebugStackFrame を含むスタックセグメントによって表されるスクリプトを呼び出しました。 

[ぜひ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-evaluate)

Evaluate メソッドは、このメソッドが呼び出された IDataModelScriptDebugStackFrame インターフェイスによって表されるスタックフレームのコンテキストで、式 (スクリプトプロバイダーの言語) を評価します。 式の評価の結果は、スクリプトプロバイダーから IModelObject としてマーシャリングする必要があります。 デバッガーが中断状態にある間は、結果として得られる IModelObject のプロパティとその他のコンストラクトをすべて取得できる必要があります。 

[EnumerateLocals](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-enumeratelocals)

EnumerateLocals メソッドは、IDataModelScriptDebugStackFrame によって表されるスタックフレームのコンテキストでスコープ内にあるすべてのローカル変数の変数セット (IDataModelScriptDebugVariableSetEnumerator インターフェイスによって表されます) を返します。このメソッドが呼び出されたインターフェイス。 

[EnumerateArguments](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-enumeratearguments)

EnumerateArguments メソッドは、IDataModelScriptDebugStackFrame によって表されるスタックフレームで呼び出される関数のすべての関数引数に対して、(IDataModelScriptDebugVariableSetEnumerator インターフェイスによって表される) 変数セットを返します。このメソッドが呼び出されたインターフェイス。 


**変数の確認: IDataModelScriptDebugVariableSetEnumerator**

デバッグ対象のスクリプト内の一連の変数 (特定のスコープ内の変数、関数のローカル変数、関数の引数など) は、IDataModelScriptDebugVariableSetEnumerator インターフェイスを使用して定義された変数セットによって表されます。

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugVariableSetEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_ BSTR *variableName, _COM_Outptr_opt_ IModelObject **variableValue, _COM_Outptr_opt_result_maybenull_ IKeyStore **variableMetadata) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugvariablesetenumerator-reset)

Reset メソッドは、列挙子の位置を、作成直後の位置 (つまり、セットの最初の要素の前) にリセットします。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugvariablesetenumerator-getnext)

GetNext メソッドは、列挙子をセット内の次の変数に移動し、変数の名前、値、およびそれに関連付けられているメタデータを返します。 列挙子がセットの末尾に達した場合は、エラー E_BOUNDS が返されます。 E_BOUNDS マーカーが GetNext メソッドから返されると、介在するリセット呼び出しが行われない限り、再度呼び出された場合は E_BOUNDS が引き続き生成されます。 


**ブレークポイント: IDataModelScriptDebugBreakpoint**

スクリプトブレークポイントは、特定のスクリプトのデバッグインターフェイスで SetBreakpoint ポイントメソッドを使用して設定します。 このようなブレークポイントは、一意の id と、次のように定義されている IDataModelScriptDebugBreakpoint インターフェイスの実装の両方によって表されます。 

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

[GetId](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-getid)

GetId メソッドは、スクリプトプロバイダーのデバッグエンジンによって割り当てられた一意の識別子をブレークポイントに返します。 この識別子は、含んでいるスクリプトのコンテキスト内で一意である必要があります。 ブレークポイント識別子は、プロバイダーに対して一意である場合があります。ただし、これは必須ではありません。 

[IsEnabled](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-isenabled)

IsEnabled メソッドは、ブレークポイントが有効になっているかどうかを返します。 無効なブレークポイントはまだ存在し、スクリプトのブレークポイントの一覧に含まれています。一時的に "オフ" になります。 すべてのブレークポイントを有効な状態で作成する必要があります。 

[Enable](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-enable)

Enable メソッドを使用すると、ブレークポイントが有効になります。 ブレークポイントが無効になっている場合、このメソッドを呼び出した後に "ブレークポイントをヒットする" と、デバッガーが中断されます。 

[切り替える](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-disable)

Disable メソッドは、ブレークポイントを無効にします。 この呼び出しの後、このメソッドを呼び出した後に "ブレークポイントをヒットする" と、デバッガーが中断されることはありません。 ブレークポイントは依然として存在しますが、"オフ" と見なされます。 

[[削除]](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-remove)

Remove メソッドは、ブレークポイントを含んでいるリストから削除します。 このメソッドから制御が戻った後、ブレークポイントはセマンティックに存在しなくなりました。 ブレークポイントを表す IDataModelScriptDebugBreakpoint インターフェイスは、呼び出しの後に孤立していると見なされます。 この呼び出しの後、この呼び出しの後で他に何も行うことはできません。 

[GetPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-getposition)

GetPosition メソッドは、スクリプト内のブレークポイントの位置を返します。 スクリプトデバッガーは、ブレークポイントが配置されているソースコード内の行と列を返す必要があります。 この操作が可能な場合は、positionSpanEnd 引数による定義に従って終了位置を入力することによって、ブレークポイントによって表されるソースの範囲を返すこともできます。 デバッガーがこのスパンを生成できず、呼び出し元が要求する場合は、スパンの終了位置の行と列のフィールドに、値を指定できないことを示すゼロとして入力する必要があります。 


**ブレークポイントの列挙: IDataModelScriptDebugBreakpointEnumerator**

スクリプトプロバイダーがデバッグをサポートしている場合は、各スクリプトに関連付けられているすべてのブレークポイントを追跡し、それらのブレークポイントをデバッグインターフェイスに列挙できる必要もあります。 ブレークポイントの列挙子は、特定のスクリプトのデバッグインターフェイスで EnumerateBreakpoints メソッドを使用して取得され、次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugBreakpointEnumerator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptDebugBreakpoint **breakpoint) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpointenumerator-reset)

Reset メソッドは、列挙子が作成された直後の位置 (つまり、最初に列挙されたブレークポイントの前) に、列挙子の位置をリセットします。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpointenumerator-getnext)

GetNext メソッドは、列挙される次のブレークポイントまで列挙子を前方に移動し、そのブレークポイントの IDataModelScriptDebugBreakpoint インターフェイスを返します。 列挙子が列挙体の末尾に達した場合は、E_BOUNDS を返します。 E_BOUNDS エラーが生成されると、その後に GetNext メソッドを呼び出すと、Reset メソッドへの介在する呼び出しが行われない限り、E_BOUNDS が引き続き生成されます。 

---

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

このトピックは、からC++アクセス可能なインターフェイス、それらを使用してC++ベースのデバッガー拡張機能を構築する方法、およびC++データモデル拡張機能から他のデータモデル構造 (JavaScript や NatVis など) を使用する方法について説明したシリーズの一部です.

[デバッガーデータモデルC++の概要](data-model-cpp-overview.md)

[デバッガーデータモデルC++のインターフェイス](data-model-cpp-interfaces.md)

[デバッガーデータモデルC++オブジェクト](data-model-cpp-objects.md)

[デバッガーデータモデルC++の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーデータモデルC++の概念](data-model-cpp-concepts.md)
