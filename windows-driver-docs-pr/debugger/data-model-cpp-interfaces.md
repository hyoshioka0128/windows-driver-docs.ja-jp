---
title: Debugger Data Model C++ のインターフェイス
description: このトピックでは、デバッガーのデータ モデルの C++ インターフェイスを使用して拡張およびデバッガーの機能をカスタマイズする方法について説明します。
ms.date: 10/08/2018
ms.openlocfilehash: 831e11ba8d5bcb28bd7842a9653dfff4205aafe7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374376"
---
# <a name="debugger-data-model-c-interfaces"></a>Debugger Data Model C++ のインターフェイス 

このトピックでは、デバッガーのデータ モデルの C++ インターフェイスを使用して拡張およびデバッガーの機能をカスタマイズする方法の概要について説明します。

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

[デバッガーのデータ モデルの C++ ホスト インターフェイス](#hostinterface)

[データ モデルにアクセスします。](#accessdatamodel)

[デバッガーのデータ モデル システム インターフェイス](#systeminterfaces)

---

## <a name="span-idhostinterfacespan-debugger-data-model-c-host-interfaces"></a><span id="hostinterface"></span> デバッガーのデータ モデルの C++ ホスト インターフェイス

**デバッガー データ モデルのホスト**

デバッガーのデータ モデルは、さまざまな異なるコンテキストでホスト可能なコンポーネント化されたシステム設計されています。 通常、データ モデルは、デバッガーのアプリケーションのコンテキストでホストされます。 データ モデルのホストをするためにはインターフェイスの数は、デバッガーの主な側面を公開する実装する必要があります: その対象とする、そのメモリ領域、そのエバリュエーター、そのシンボリック システムなどの入力としています.データ モデルをホストしたい任意のアプリケーションでは、これらのインターフェイスが実装される、コア データ モデルとデータ モデルと相互運用を任意の拡張機能の両方によって利用されます。 

コア インターフェイスのセットは次のとおりです。 

インターフェイス名 | 説明
|--------------|---------------|
IDebugHost | デバッグ ホストするコア インターフェイスです。
IDebugHostStatus  | ホストの状態のクエリにクライアントを許可するインターフェイスです。
IDebugHostContext  | ホストでのコンテキストの抽象化 (例: 特定のターゲット、特定のプロセスと特定のアドレス空間など.)。
IDebugHostErrorSink  | ホストとデータ モデルの特定の部分からエラーを受信する呼び出し元によって実装されるインターフェイス
IDebugHostEvaluator/IDebugHostEvaluator2  | デバッグ ホストの式エバリュエーター。
IDebugHostExtensibility  | ホストの機能や、式エバリュエーター) などの部分を拡張するためのインターフェイスです。

型システムとシンボリック インターフェイスは。 

InterfaceName | 説明
|--------------|---------------|
IDebugHostSymbols | アクセスおよびのシンボルの解決を提供するコア インターフェイス
IDebugHostSymbol/IDebugHostSymbol2  | 任意の種類の 1 つのシンボルを表します。 特定のシンボルは、このインターフェイスの派生です。
IDebugHostModule | プロセス内で読み込まれたモジュールを表します。 これは、シンボルの一種です。
IDebugHostType/IDebugHostType2  | ネイティブ/言語の型を表します。
IDebugHostConstant  | シンボリック情報内の定数を表します (例: C++ での非型テンプレート引数を)
IDebugHostField  | 構造体またはクラス内のフィールドを表します。
IDebugHostData | モジュール内でデータを表します (構造体またはクラス、IDebugHostField なります内でしたこの)
IDebugHostBaseClass | 基本クラスを表します。
IDebugHostPublic  | PDB の publics テーブル内のシンボルを表します。 関連付けの種類の情報はありません。 名前とアドレスをお勧めします。
IDebugHostModuleSignature | モジュール署名 - これが一連のモジュール名やバージョンが一致する定義を表します
IDebugHostTypeSignature | 型シグネチャ--これモジュールや名前によって、一連の型が一致する定義を表します


**Core のホスト インターフェイス:IDebugHost**

IDebugHost インターフェイスは、任意のデータ モデルのホストのコア インターフェイスです。 次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IDebugHost, IUnknown)
{
    STDMETHOD(GetHostDefinedInterface)(_COM_Outptr_ IUnknown** hostUnk) PURE;
    STDMETHOD(GetCurrentContext)(_COM_Outptr_ IDebugHostContext** context) PURE;
    STDMETHOD(GetDefaultMetadata)(_COM_Outptr_ IKeyStore** defaultMetadataStore) PURE;
}
```

[GetHostDefinedInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughost-gethostdefinedinterface)

GetHostDefinedInterface メソッドは、このような特定のホストが存在する場合に、ホストの主要なプライベート インターフェイスを返します。 Windows のツールをデバッグ インターフェイスは、IDebugClient (IUnknown へのキャスト) は、ここで返されます。 

[GetCurrentContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughost-getcurrentcontext)

GetCurrentContext メソッドは、デバッガー ホストの現在の状態を表すインターフェイスを返します。 この厳密な意味は、ホストに委ねが、通常、セッション、プロセス、およびデバッグ ホストのユーザー インターフェイスでアクティブになっているアドレス空間などが含まれます。 返されるコンテキスト オブジェクトは、呼び出し元に大きく不透明が、重要なデバッグ ホストへの呼び出しの間で渡すオブジェクト。 呼び出し元は、メモリ、読み取り時に、メモリから読み取られているどのプロセスとアドレス空間を把握しておく。 その概念は、このメソッドから返されるコンテキスト オブジェクトの概念にカプセル化されます。 

[GetDefaultMetadata](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughost-getdefaultmetadata)

GetDefaultMetadata メソッドは、特定の操作に使用される可能性のある既定のメタデータ ストアを返します (例: 文字列変換) と明示的なメタデータが渡されていません。 これにより、デバッグ ホストをある程度の制御方法をいくつかのデータが表示されます。 たとえば、既定のメタデータは PreferredRadix キーを示すかどうか序数する必要がある 10 進数または 16 進数で表示されます。 それ以外の場合も指定しない場合、ホストがあるためを含めることができます。 

既定のメタデータ ストアのプロパティ値が手動で解決する必要があり、既定のメタデータのクエリ対象のオブジェクトを渡す必要がありますに注意してください。 GetKeyValue 代わり GetKey メソッドを使用する必要があります。 

**状態インターフェイス:IDebugHostStatus** 

IDebugHostStatus インターフェイスでは、クライアントは、データ モデルのデバッグ ホストの状態の特定の側面について照会するデバッグ ホストできます。 インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDebugHostStatus, IUnknown)
{
    STDMETHOD(PollUserInterrupt)(_Out_ bool* interruptRequested) PURE;
}
```

[PollUserInterrupt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughoststatus-polluserinterrupt)

デバッグ ホストのユーザーが現在の操作の中断を要求されたかどうかを照会する PollUserInterrupt メソッドが使用されます。 データ モデルのプロパティのアクセサーが任意のコードを呼び出すことがあります、たとえば、(例: JavaScript メソッド)。 そのコードは、任意の時間の長さをかかる場合があります。 デバッグ ホストの応答性を維持するためにこのメソッドの呼び出しを使用して、割り込み要求、任意の一定の時間がかかる場合がありますが、このようなコードを確認します。 InterruptRequested 値 true として戻す場合は、呼び出し元をすぐに中止し、E_ABORT の結果を返します。 


**コンテキスト インターフェイス:IDebugHostContext**

コンテキストでは、データ モデルと基になるデバッグ ホストの最も重要な側面の 1 つです。 オブジェクトを保持することがある重要です--からのオブジェクトの入手先を認識できるどのようなプロセスでは、どのようなアドレス空間がそれに関連付けられています。 ポインター値などの正しい解釈は、この情報を把握できます。 型のオブジェクト IDebugHostContext 渡す必要があります多くのメソッドをデバッグ ホスト。 このインターフェイスは、さまざまな方法で取得できます。

- デバッガーの現在のコンテキストを取得することによって: IDebugHost の GetCurrentContext メソッドを呼び出す
- オブジェクトのコンテキストを取得することによって: IModelObject の GetContext メソッドを呼び出す
- シンボルのコンテキストを取得することによって: IDebugHostSymbol の GetContext メソッドを呼び出す

さらに、またはいずれかから返されたデータ モデルまたはデバッグ ホストのメソッドに渡される IDebugHostContext インターフェイスのコンテキストで特別な意味のある値は 2 つです。 

*nullptr*: コンテキストがないことを示す値。 コンテキストがない一部のオブジェクトで完全に有効になります。 データ モデルのルート名前空間でデバッガー オブジェクトは、特定のプロセスまたはアドレス空間内のすべてには参照しません。 コンテキストがありません。

*USE_CURRENT_HOST_CONTEXT*: いずれかを示す sentinel 値がデバッグ ホストの現在の UI コンテキストを使用する必要があります。 この値は、デバッグ ホストから返されません。 あるで可能性があります、ただし、IDebugHost の GetCurrentContext メソッドを明示的に呼び出す代わりの入力の IDebugHostContext はデバッグ ホストのメソッドに渡されます。 USE_CURRENT_HOST_CONTEXT を明示的に渡すこと、現在のコンテキストを明示的に取得するよりもパフォーマンスが向上は、多くの場合に注意してください。 

ホスト コンテキストのコンテキストは呼び出し元に主に非透過的です。 コアのデバッグ ホストの外部の呼び出し元は、ホストのコンテキストで実行できる唯一の操作では、別のホスト コンテキストと比較します。 

IDebugHostContext インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDebugHostContext, IUnknown)
{
    STDMETHOD(IsEqualTo)(_In_ IDebugHostContext *pContext, _Out_ bool *pIsEqual) PURE;
}
```

[IsEqualTo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostcontext-isequalto)

IsEqualTo メソッドは、ホストのコンテキストを別のホスト コンテキストを比較します。 2 つのコンテキストと同じ場合は、これを示す値が返されます。 この比較がインターフェイスの等価性ではないことに注意してください。 これは、コンテキスト自体の基になる非透過の内容を比較します。 


**エラー シンク。IDebugHostErrorSink**

特定の操作中に発生して、これらのエラーのルーティング エラーの通知をクライアントから受信できる手段になります、IDebugHostErrorSink 必要な場所。 インターフェイスの定義は次のとおりです。 

```cpp
enum ErrorClass
{
    ErrorClassWarning,
    ErrorClassError
}
```

```cpp
DECLARE_INTERFACE_(IDebugHostErrorSink, IUnknown)
{
    STDMETHOD(ReportError)(_In_ ErrorClass errClass, _In_ HRESULT hrError, _In_ PCWSTR message) PURE;
}
```

[ReportError](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosterrorsink-reporterror)

ReportError メソッドは、エラーが発生したことを通知し、任意の UI またはメカニズムが適切なエラーにルーティングするシンク エラー シンク上でのコールバック。 


**ホスト エバリュエータ:IDebugHostEvaluator/IDebugHostEvaluator2**

デバッグ ホストをクライアントに提供する機能の最も重要な情報の 1 つは、そのベース言語の式エバリュエーターにアクセスします。 IDebugHostEvaluator と IDebugHostEvaluator2 インターフェイスは、デバッグ ホストからその機能にアクセスする手段です。 

インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDebugHostEvaluator2, IDebugHostEvaluator)
{
    //
    // IDebugHostEvaluator:
    //
    STDMETHOD(EvaluateExpression)(_In_ IDebugHostContext* context, _In_ PCWSTR expression, _In_opt_ IModelObject* bindingContext, _COM_Errorptr_ IModelObject** result, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(EvaluateExtendedExpression)(_In_ IDebugHostContext* context, _In_ PCWSTR expression, _In_opt_ IModelObject* bindingContext, _COM_Errorptr_ IModelObject** result, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    //
    // IDebugHostEvaluator2:
    //
    STDMETHOD(AssignTo)(_In_ IModelObject* assignmentReference, _In_ IModelObject* assignmentValue, _COM_Errorptr_ IModelObject** assignmentResult, _COM_Outptr_opt_result_maybenull_ IKeyStore** assignmentMetadata) PURE;
}
```

[式の評価](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostevaluator-evaluateexpression)

式の評価方法は、言語を評価するデバッグ ホストの要求を許可 (例。C++) の式とその式の評価の結果として得られる値を返しますが、IModelObject としてボックス化されます。 メソッドのこの特定のバリアントは、言語構成要素を許可するだけです。 他の機能が言語に存在しないデバッグ ホストの式エバリュエーターで表示されます (例。LINQ クエリ メソッド) は、評価のため無効になります。 

[EvaluateExtendedExpression](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostevaluator-evaluateextendedexpression)

EvaluateExtendedExpression メソッドはを有効に戻す、式エバリュエーターに追加する特定のデバッグ ホストを選択する以外の言語機能を追加する点を除いて、式の評価メソッドに似ています。 Windows のツールをデバッグなど、これを行うと匿名型、LINQ クエリ、モジュールの修飾子、書式指定子およびその他の C と C++ の機能です。 


**IDebugHostEvaluator2**

[AssignTo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostevaluator2-assignto)

AssignTo メソッドは、デバッグされている言語のセマンティクスに従って割り当てを実行します。 


**ホストの機能拡張インターフェイス:IDebugHostExtensibility**

デバッグ ホストの特定の機能は拡張オプションです。 たとえば、式エバリュエーターを含めるこれ、可能性があります。 IDebugHostExtensibility インターフェイスは、これらの拡張ポイントをアクセスする手段です。 インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDebugHostExtensibility, IUnknown)
{
    STDMETHOD(CreateFunctionAlias)(_In_ PCWSTR aliasName, _In_ IModelObject *functionObject) PURE;
    STDMETHOD(DestroyFunctionAlias)(_In_ PCWSTR aliasName) PURE;
}
```

[CreateFunctionAlias](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostextensibility-createfunctionalias)

CreateFunctionAlias メソッドは、「関数のエイリアス」、いくつかの拡張機能で実装されるメソッドの「クイック エイリアス」を作成します。 このエイリアスの意味は、特定のホストです。 関数で、ホストの式エバリュエーターを拡張することがありますか、まったく異なるものに行うことができます。 

[DestroyFunctionAlias](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostextensibility-destroyfunctionalias)

DestroyFunctionAlias メソッド元 CreateFunctionAlias メソッドを呼び出す前に戻します。 関数は、クイック別名で使用可能なされなくなります。 



## <a name="span-idaccessdatamodel-accessing-the-data-model"></a><span id="accessdatamodel"> データ モデルにアクセスします。

第一に、データ モデルの機能拡張の Api がデータ モデルのホストとして機能するアプリケーション (通常はデバッガー) に依存しないにデザインされています。 理論上は、任意のアプリケーションは、一連のホストについて、どのようなターゲット、プロセス、スレッド、データ モデルの名前空間に、アプリケーションのデバッグ ターゲットの型システムと、射影されたオブジェクトのセットを公開する Api を提供することで、データ モデルをホストできるなどしています.は、ターゲットをデバッグします。 

データ モデルの Api - IDataModel を開始するときに<em>、IDebugHost</em>、定義しない、IModelObject--の集めてを移植できるように設計がどのような「デバッガー拡張機能」は。 今日では、Windows のツールのデバッグと、エンジンを拡張することを希望するコンポーネントは、データ モデルへのアクセスを取得するためにエンジンの拡張機能を記述する必要があります。 そのエンジンの拡張機能は、読み込みと拡張機能のメカニズムをブートス トラップにはエンジンの拡張機能にのみ必要があります。 そのため、最小限の実装は提供します。 

- **DebugExtensionInitialize**:データ モデルにアクセスするために作成された IDebugClient を利用し、オブジェクト モデルの操作を設定するメソッド。
- **DebugExtensionUninitialize**:DebugExtensionInitialize で実行されたオブジェクト モデルの操作を元に戻す方法。
- **DebugExtensionCanUnload**:拡張機能をアンロードできるかどうかを返すメソッド。 拡張機能にまだ存在している COM オブジェクトがある場合、これを示す必要があります。 これは、COM の DllCanUnloadNow のデバッガーのと同じです。 アンロードできない S_FALSE を示す値を返すこの場合、デバッガーはアンロードが安全か DebugExtensionInitialize をもう一度呼び出すことによって、拡張機能を再初期化できますが後でこのクエリを実行できます。 拡張機能は、両方のパスを処理するために準備する必要があります。
- **DebugExtensionUnload**:最終的なクリーンアップを行うメソッドには右が必要な DLL をアンロードする前に

*ブリッジ インターフェイス:IHostDataModelAccess*

説明したとおり、DebugExtensionInitialize が呼び出されると、デバッグのクライアントを作成し、データ モデルへのアクセスを取得します。 このようなアクセスは、Windows のツールのデバッグのレガシ IDebug * インターフェイスとデータ モデルの間のブリッジ インターフェイスによって提供されます。 このブリッジ インターフェイスは、' IHostDataModelAccess が次のように定義されているとします。 

```cpp
DECLARE_INTERFACE_(IHostDataModelAccess, IUnknown)
{
   STDMETHOD(GetDataModel)(_COM_Outptr_ IDataModelManager** manager, _COM_Outptr_ IDebugHost** host) PURE;
}
```

[GetDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ihostdatamodelaccess-getdatamodel)

GetDataModel メソッドは、データ モデルの両方の側へのアクセスを提供するブリッジ インターフェイスでメソッドを示します。デバッグ ホスト (デバッガーの下端) は、データ モデルの主要なコンポーネント - データ モデルのマネージャーは、返された IDataModelManager インターフェイスによって表されます。 返された IDebugHost インターフェイスによって表されます



## <a name="span-idsysteminterfacesspan-debugger-data-model-system-interfaces"></a><span id="systeminterfaces"></span> デバッガーのデータ モデル システム インターフェイス

**データ モデルのホスト**

デバッガーのデータ モデルは、さまざまな異なるコンテキストでホスト可能なコンポーネント化されたシステム設計されています。 通常、データ モデルは、デバッガーのアプリケーションのコンテキストでホストされます。 データ モデルのホストをするためにはインターフェイスの数は、デバッガーの主な側面を公開する実装する必要があります: その対象とする、そのメモリ領域、そのエバリュエーター、そのシンボリック システムなどの入力としています.データ モデルをホストしたい任意のアプリケーションでは、これらのインターフェイスが実装される、コア データ モデルとデータ モデルと相互運用を任意の拡張機能の両方によって利用されます。 

型システムとシンボリック インターフェイスは。 


インターフェイス名 | 説明
|--------------|------------------|
IDebugHostSymbols  | アクセスおよびのシンボルの解決を提供するコア インターフェイス
IDebugHostSymbol/IDebugHostSymbol2  | 任意の種類の 1 つのシンボルを表します。 特定のシンボルは、このインターフェイスの派生です。
IDebugHostModule  | プロセス内で読み込まれたモジュールを表します。 これは、シンボルの一種です。
IDebugHostType/IDebugHostType2  | ネイティブ/言語の型を表します。
IDebugHostConstant  | シンボリック情報内の定数を表します (例: C++ での非型テンプレート引数を)
IDebugHostField | 構造体またはクラス内のフィールドを表します。
IDebugHostData | モジュール内でデータを表します (構造体またはクラス、IDebugHostField なります内でしたこの)
IDebugHostBaseClass  | 基本クラスを表します。
IDebugHostPublic | PDB の publics テーブル内のシンボルを表します。 関連付けの種類の情報はありません。 名前とアドレスをお勧めします。
IDebugHostModuleSignature | モジュール署名 - これが一連のモジュール名やバージョンが一致する定義を表します
IDebugHostTypeSignature | 型シグネチャ--これモジュールや名前によって、一連の型が一致する定義を表します

その他の主要なインターフェイスは次のとおりです。 

インターフェイス名 | 説明
|--------------|------------------|
IDebugHost | デバッグ ホストするコア インターフェイスです。
IDebugHostStatus | ホストの状態のクエリにクライアントを許可するインターフェイスです。
IDebugHostContext | ホストでのコンテキストの抽象化 (例: 特定のターゲット、特定のプロセスと特定のアドレス空間など.)。
IDebugHostErrorSink | ホストとデータ モデルの特定の部分からエラーを受信する呼び出し元によって実装されるインターフェイス
IDebugHostEvaluator/IDebugHostEvaluator2 | デバッグ ホストの式エバリュエーター。
IDebugHostExtensibility | ホストの機能や、式エバリュエーター) などの部分を拡張するためのインターフェイスです。


**メインのシンボリック インターフェイス:IDebugHostSymbols**

IDebugHostSymbols インターフェイスとは、デバッグ対象のアクセスのシンボルにメインの開始点です。 このインターフェイスは IDebugHost のインスタンスからクエリを実行でき、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDebugHostSymbols, IUnknown)
{
    STDMETHOD(CreateModuleSignature)(_In_z_ PCWSTR pwszModuleName, _In_opt_z_ PCWSTR pwszMinVersion, _In_opt_z_ PCWSTR pwszMaxVersion, _Out_ IDebugHostModuleSignature** ppModuleSignature) PURE;
    STDMETHOD(CreateTypeSignature)(_In_z_ PCWSTR signatureSpecification, _In_opt_ IDebugHostModule* module, _Out_ IDebugHostTypeSignature** typeSignature) PURE;
    STDMETHOD(CreateTypeSignatureForModuleRange)(_In_z_ PCWSTR signatureSpecification, _In_z_ PCWSTR moduleName, _In_opt_z_ PCWSTR minVersion, _In_opt_z_ PCWSTR maxVersion, _Out_ IDebugHostTypeSignature** typeSignature) PURE;
    STDMETHOD(EnumerateModules)(_In_ IDebugHostContext* context, _COM_Outptr_ IDebugHostSymbolEnumerator** moduleEnum) PURE;
    STDMETHOD(FindModuleByName)(_In_ IDebugHostContext* context, _In_z_ PCWSTR moduleName, _COM_Outptr_ IDebugHostModule **module) PURE;
    STDMETHOD(FindModuleByLocation)(_In_ IDebugHostContext* context, _In_ Location moduleLocation, _COM_Outptr_ IDebugHostModule **module) PURE;
    STDMETHOD(GetMostDerivedObject)(_In_opt_ IDebugHostContext *pContext, _In_ Location location, _In_ IDebugHostType* objectType, _Out_ Location* derivedLocation, _Out_ IDebugHostType** derivedType) PURE;
}
```

[CreateModuleSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-createmodulesignature)

CreateModuleSignature メソッドは、名前とバージョンによって、必要に応じて、特定のモジュールのセットに一致するために使用する署名を作成します。 モジュール署名に 3 つのコンポーネントです。 

- 名前: 一致するモジュールには、署名内の名前に対する大文字と小文字を区別しない一致する名前が必要です。
- 最小バージョン: これは、少なくともこのバージョンと同程度に高バージョンを指定した場合一致するモジュールである必要があります。 バージョンは、以前よりも重要度の低いされている各後続の部分に"A.B.C.D"の形式で指定されます。 最初のセグメントのみが必須です。
- 最大バージョン: 場合は、指定された一致するモジュールがこのバージョン以上である最大バージョンをいる必要があります。 バージョンは、以前よりも重要度の低いされている各後続の部分に"A.B.C.D"の形式で指定されます。 最初のセグメントのみが必須です。

[CreateTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-createtypesignature)

CreateTypeSignature メソッドは、モジュールと型名を格納している別の一連の具象型に一致するために使用する署名を作成します。 型名の署名文字列の形式はデバッグ中の言語に固有です (および、デバッグ ホスト)。 C と C++ の署名文字列は、NatVis 型の指定と同じです。 署名文字列は、型名をワイルドカード (として指定された *) のテンプレート引数が許可されます。 

[CreateTypeSignatureForModuleRange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-createtypesignatureformodulerange)

CreateTypeSignatureForModuleRange メソッドは、具象型のセットに一致するモジュールの署名と型名で使用できる署名を作成します。 これは、シグネチャの一致するように特定のモジュールを渡す代わりに、呼び出し元引数を渡しますモジュールの署名を作成するために必要なドキュメントを除く CreateTypeSignature メソッドに似ています (モジュールの署名で作成された場合に、CreateModuleSignature メソッド)。 

[EnumerateModules](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-enumeratemodules)

EnumerateModules メソッドは、特定のホストのコンテキストで使用できるすべてのモジュールを列挙する列挙子を作成します。 そのホスト コンテキストがプロセスのコンテキストをカプセル化、または Windows カーネルのようなものがカプセル化があります。 


[FindModuleByName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-findmodulebyname)

FindModuleByName メソッドでは、特定のホスト コンテキストをよく見て、指定した名前を持つモジュールを特定およびそのにインターフェイスが返しますされます。 名前のファイル拡張子の有無で、モジュールを検索することはできます。 

[FindModuleByLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-findmodulebylocation)

FindModuleByLocation メソッドでは、特定のホスト コンテキスト全体を確認し、どのようなモジュールには、指定した場所によって指定されたアドレスが含まれるを決定します。 このようなモジュールに、インターフェイスを返します。 

[GetMostDerivedObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-getmostderivedobject)

GetMostDerivedObject は、静的な型のオブジェクトのランタイム型を決定するのに、デバッガーの型システムを使用します。 このメソッドはのみを使用して、シンボリック情報とヒューリスティックを使用可能な型システム レイヤーでこの分析を実行するには。 このような情報は、C++ RTTI を (実行時型情報) またはオブジェクトの仮想関数テーブルの形状の分析に含めることができます。 推奨ランタイム型の概念上、IModelObject などは含まれません。 分析では、ランタイム型が見つからないか、メソッドに渡される静的な型と異なるランタイム型を見つけることができません場合、入力場所と種類渡す可能性があります。これらの理由から、メソッドは失敗しません。 



**コアの個別のシンボル インターフェイス:IDebugHostSymbol**

データ モデルのホストから返されるすべてのシンボルは、なんらかの方法で IDebugHostSymbol から派生されます。 これは、すべてのシンボルをシンボルの種類に関係なく実装するコア インターフェイスです。 シンボルの種類、に応じて特定のシンボルは属性を返しますより一意な特定の種類のシンボル名のこのインターフェイスによって他のインターフェイスのセットを実装できます。 IDebugHostSymbol2 IDebugHostSymbol インターフェイスが次のように定義されている/。 

```cpp
DECLARE_INTERFACE_(IDebugHostSymbol2, IDebugHostSymbol)
{
    // 
    // IDebugHostSymbol:
    //
    STDMETHOD(GetContext)(_COM_Outptr_ IDebugHostContext** context) PURE;
    STDMETHOD(EnumerateChildren)(_In_ SymbolKind kind, _In_opt_z_ PCWSTR name, _Out_ IDebugHostSymbolEnumerator **ppEnum) PURE;
    STDMETHOD(GetSymbolKind)(_Out_ SymbolKind *kind) PURE;
    STDMETHOD(GetName)(_Out_ BSTR* symbolName) PURE;
    STDMETHOD(GetType)(_Out_ IDebugHostType** type) PURE;
    STDMETHOD(GetContainingModule)(_Out_ IDebugHostModule **containingModule) PURE;
    STDMETHOD(CompareAgainst)(_In_ IDebugHostSymbol *pComparisonSymbol, _In_ ULONG comparisonFlags, _Out_ bool *pMatches) PURE;
    //
    // IDebugHostSymbol2
    //
    STDMETHOD(EnumerateChildrenEx)(_In_ SymbolKind kind, _In_opt_z_ PCWSTR name, _In_opt_ SymbolSearchInfo* searchInfo, _Out_ IDebugHostSymbolEnumerator **ppEnum) PURE;
}
```

このインターフェイスが次のように値を持つ SymbolKind 列挙体によって区切られた--シンボルのさまざまな種類を表すことに注意してください。 非常に重要ですが。 

Enumarant | 説明
|--------------|------------------|
シンボル  | 指定されていないシンボルの種類 
SymbolModule | シンボルのモジュールし、IDebugHostModule に対してクエリを実行できます。
SymbolType | シンボルは型であり IDebugHostType を照会することができます。
SymbolField | シンボルはフィールド (構造体またはクラス内でのデータ メンバー) であり IDebugHostField を照会することができます。
SymbolConstant | シンボルは定数値と IDebugHostConstant に対してクエリを実行できます。
SymbolData | シンボルは、これは構造体またはクラスのメンバーでありは IDebugHostData のクエリ可能なデータ
SymbolBaseClass | シンボルの基本クラスし、IDebugHostBaseClass のクエリです。
SymbolPublic | シンボル (型情報を持たない) モジュールの publics テーブル内のエントリし、IDebugHostPublic のクエリです。
SymbolFunction | シンボルは関数であり IDebugHostData のクエリです。

[GetContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbol-getcontext)

GetContext メソッドは、シンボルが有効なコンテキストを返します。 など、シンボルが存在するデバッグ ターゲットおよびプロセス/アドレス領域を表すこれは、中にある可能性がありますいない具体的には、他の方法から取得したコンテキスト (例:: から、 *IModelObject*)。 

[EnumerateChildren](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbol-enumeratechildren)

EnumerateChildren メソッドは、特定のシンボルのすべての子を列挙する列挙子を返します。 基底クラス、フィールド、たとえば、C++ の型のメンバー関数、およびなどは、型のシンボルのすべてと見なされますの子です。 


**モジュール インターフェイス:IDebugHostModule**

デバッガーの概念のいくつかのアドレス空間内で読み込まれるモジュールは、データ モデル内の 2 つの点で表されます。IDebugHostModule インターフェイス経由で型システム レベル。 ここでは、モジュールは、シンボルとモジュールの core 属性はインターフェイス メソッドを呼び出す予測データ モデルで Debugger.Models.Module のデータ モデルを使用してレベル。 これは、型システム モジュールの IDebugHostModule 表現の拡張可能なカプセル化します。

IDebugHostModule インターフェイスは、次のとおりです (IDebugHostSymbol の一般的なメソッドを無視します) として定義されます。 

```cpp
DECLARE_INTERFACE_(IDebugHostModule, IDebugHostSymbol)
{
    //
    // IDebugHostModule:
    //
    STDMETHOD(GetImageName)(_In_ bool allowPath, _Out_ BSTR* imageName) PURE;
    STDMETHOD(GetBaseLocation)(_Out_ Location* moduleBaseLocation) PURE;
    STDMETHOD(GetVersion)(_Out_opt_ ULONG64* fileVersion, _Out_opt_ ULONG64* productVersion) PURE;
    STDMETHOD(FindTypeByName)(_In_z_ PCWSTR typeName, _Out_ IDebugHostType** type) PURE;
    STDMETHOD(FindSymbolByRVA)(_In_ ULONG64 rva, _Out_ IDebugHostSymbol** symbol) PURE;
    STDMETHOD(FindSymbolByName)(_In_z_ PCWSTR symbolName, _Out_ IDebugHostSymbol** symbol) PURE;
}
```

[GetImageName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-getimagename)

GetImageName メソッドは、モジュールのイメージの名前を返します。 AllowPath 引数の値、によって返されるイメージの名前は可能性があります。 またはイメージへの完全パスを含めることはできません。

[GetBaseLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-getbaselocation)

GetBaseLocation メソッドは、場所の構造体として、モジュールのベース読み込みアドレスを返します。 モジュール、構造体の返される場所は、通常仮想アドレスを参照してください。

[GetVersion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-getversion)

GetVersion メソッドは、(このような情報はヘッダーから正常に読み取ることができますを想定) モジュールのバージョン情報を返します。 読み取ることができません (nullptr 以外の出力ポインター) を使用して、指定したバージョンが要求された場合、適切なエラー コードがメソッドの呼び出しから返されます。 

[FindTypeByName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-findtypebyname)

FindTypeByName メソッドは、型名で、モジュール内で定義された型を検索して、その型のシンボルを返します。 このメソッドは、モジュールの子の明示的な再帰を使用して返されることはありませんが有効な IDebugHostType を返す可能性があります。 デバッグ ホストは、派生型、モジュール自体内で使用されることはありませんが、ある型から派生した型の作成を許可することがあります。 たとえば、モジュールが、MyStruct 型のシンボルで MyStruct 構造が定義されている場合 * * を初めて使用 FindTypeByName メソッド返す可能性があります合法的型シンボル MyStruct の * * のシンボルに明示的に表示されるその型の名前に関係なくモジュール。 

[FindSymbolByRVA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-findsymbolbyrva)

FindSymbolByRVA メソッドは、モジュール内の特定の相対仮想アドレスで単一の一致するシンボルを紹介します。 ないかどうか、1 つの記号で指定された RVA (例: 複数の一致がある)、このメソッドによって、エラーが返されます。 プライベート シンボル publics テーブル内のシンボルを返すことはこのメソッドで優先に注意してください。 

[FindSymbolByName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-findsymbolbyname)

FindSymbolByName メソッドは、モジュール内で指定した名前の単一のグローバル シンボルを検索します。 指定した名前に一致する単一のシンボルがない場合、このメソッドによってエラーが返されます。 プライベート シンボル publics テーブル内のシンボルを返すことはこのメソッドで優先に注意してください。 


**型システムへのアクセス:IDebugHostType2/IDebugHostType**

指定された言語/ネイティブ型は、IDebugHostType2 または IDebugHostType インターフェイスによって記述されます。 これらのインターフェイスのメソッドの一部のみ、特定の種類の型に適用されるに注意してください。 指定した型のシンボルは可能性があります TypeKind 列挙体の説明に従って、次の種類のいずれかに参照してください。 

型の種類 |  説明
|--------------|------------------|
TypeUDT | ユーザー定義型 (構造体、クラス、共用体など.)。種類が TypeUDT ネイティブ型がモデル オブジェクトには、対応する IModelObject 内で型が常に保存されている ObjectTargetObject の正規表現があります。
TypePointer | ポインター。 種類が TypePointer ネイティブ型がモデル オブジェクトには、ポインターの値のゼロする VT_UI8 拡張され、この 64 ビット形式での組み込みのデータとして保持されるが ObjectIntrinsic の正規表現があります。 TypePointer の任意の種類のシンボルには、ポインターが指す型の (GetBaseType メソッドによって返される) として基本型があります。
TypeMemberPointer | クラス メンバーへのポインター。 種類が TypeMemberPointer ネイティブ型がモデル オブジェクトが組み込みである正規表現 (ポインター値と同じ値)。 この値の厳密な意味は、特定のコンパイラ/デバッグ ホストです。
TypeArray | 配列。 種類が TypeArray ネイティブ型がモデル オブジェクトには、ObjectTargetObject の正規表現があります。 配列のベース アドレスは (GetLocation メソッドを使用して取得) のオブジェクトの場所と、配列の型が常に保持されます。 TypeArray の任意の種類のシンボルには、(GetBaseType メソッドによって返される) として、配列は配列の型の基本型があります。
TypeFunction | 関数。
TypeTypedef | Typedef。 種類は TypeTypedef にそれ以外の場合はネイティブ型がモデル オブジェクトには、typedef の基になる最終的な型の正規表現と同じ正規表現があります。 これは、IDebugHostType2 の typedef の明示的なメソッドを使用して、クエリの typedef 情報または typedef に対して登録されている、明示的なデータ モデルがある場合を除き、オブジェクトと型情報のエンドユーザーに完全に透過的な表示されます。 GetTypeKind メソッド TypeTypedef を返さないことに注意してください。 すべてのメソッドは、typedef の基になる最終的な型で返すように戻ります。 IDebugHostType2 typedef に固有の情報を取得するために使用するのには、typedef の特定のメソッドがあります。
TypeEnum | 列挙型。 種類が TypeEnum ネイティブ型がモデル オブジェクトには、値と、組み込みの型は列挙型の値と同じ ObjectIntrinsic の正規表現があります。 
TypeIntrinsic | 組み込み (基本型)。 種類が TypeIntrinsic ネイティブ型がモデル オブジェクトには、ObjectIntrinsic の正規表現があります。 型情報の可能性がありますまたは保持されません--、IModelObject に格納されている組み込みのデータのバリアント データ型 (vt _ を付けます *) を基になる型が完全に説明されている場合に特に

全体的な IDebugHostType2 (IDebugHostSymbol メソッド) を除く IDebugHostType インターフェイスは、次のように定義されている/。 

```cpp
DECLARE_INTERFACE_(IDebugHostType2, IDebugHostType)
{
    //
    // IDebugHostType:
    //
    STDMETHOD(GetTypeKind)(_Out_ TypeKind *kind) PURE;
    STDMETHOD(GetSize)(_Out_ ULONG64* size) PURE;
    STDMETHOD(GetBaseType)(_Out_ IDebugHostType** baseType) PURE;
    STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
    STDMETHOD(GetIntrinsicType)(_Out_opt_ IntrinsicKind *intrinsicKind, _Out_opt_ VARTYPE *carrierType) PURE;
    STDMETHOD(GetBitField)(_Out_ ULONG* lsbOfField, _Out_ ULONG* lengthOfField) PURE;
    STDMETHOD(GetPointerKind)(_Out_ PointerKind* pointerKind) PURE;
    STDMETHOD(GetMemberType)(_Out_ IDebugHostType** memberType) PURE;
    STDMETHOD(CreatePointerTo)(_In_ PointerKind kind, _COM_Outptr_ IDebugHostType** newType) PURE;
    STDMETHOD(GetArrayDimensionality)(_Out_ ULONG64* arrayDimensionality) PURE;
    STDMETHOD(GetArrayDimensions)(_In_ ULONG64 dimensions, _Out_writes_(dimensions) ArrayDimension *pDimensions) PURE;
    STDMETHOD(CreateArrayOf)(_In_ ULONG64 dimensions, _In_reads_(dimensions) ArrayDimension *pDimensions, _COM_Outptr_ IDebugHostType** newType) PURE;
    STDMETHOD(GetFunctionCallingConvention)(_Out_ CallingConventionKind* conventionKind) PURE;
    STDMETHOD(GetFunctionReturnType)(_COM_Outptr_ IDebugHostType** returnType) PURE;
    STDMETHOD(GetFunctionParameterTypeCount)(_Out_ ULONG64* count) PURE;
    STDMETHOD(GetFunctionParameterTypeAt)(_In_ ULONG64 i, _Out_ IDebugHostType** parameterType) PURE;
    STDMETHOD(IsGeneric)(_Out_ bool* isGeneric) PURE;
    STDMETHOD(GetGenericArgumentCount)(_Out_ ULONG64* argCount) PURE;
    STDMETHOD(GetGenericArgumentAt)(_In_ ULONG64 i, _Out_ IDebugHostSymbol** argument) PURE;
    //
    // IDebugHostType2:
    //
    STDMETHOD(IsTypedef)(_Out_ bool* isTypedef) PURE;
    STDMETHOD(GetTypedefBaseType)(_Out_ IDebugHostType2** baseType) PURE;
    STDMETHOD(GetTypedefFinalBaseType)(_Out_ IDebugHostType2** finalBaseType) PURE;
    STDMETHOD(GetFunctionVarArgsKind)(_Out_ VarArgsKind* varArgsKind) PURE;
}
```

**IDebugHostType2/IDebugHostType 一般的な方法**

次の IDebugHostType メソッド GetTypeKind メソッドから返されるどのような種類に関係なく任意の型の汎用のとおりです。 

```cpp
STDMETHOD(GetTypeKind)(_Out_ TypeKind *kind) PURE;
STDMETHOD(GetSize)(_Out_ ULONG64* size) PURE;
STDMETHOD(GetBaseType)(_Out_ IDebugHostType** baseType) PURE;
STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
```

[GetTypeKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-gettypekind)

GetTypeKind メソッドは、シンボルが参照する型 (ポインター、配列を組み込みなど) の種類を返します。 

[GetSize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getsize)

GetSize メソッドは、(sizeof(type) C++ では 1 つ実行済みだった) 場合と、型のサイズを返します。 

[GetBaseType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getbasetype)

型が別の 1 つの型の派生クラスである場合 (例:: MyStruct として * MyStruct から派生 ')、GetBaseType メソッドは、派生の基本型を返します。 ポインターが指す型を返します。 配列、配列が配列の内容を返します。 このような派生型でない型、エラーが返されます。 

[GetHashCode](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-gethashcode)

GetHashCode メソッドでは、型の 32 ビットのハッシュ コードを返します。 グローバルな一致を除く (例:: 型のシグネチャと等価 * ホストで許可されている場合は、すべてに一致する)、特定の型シグネチャに一致する型のインスタンスが同じハッシュ コードを返す必要があります。 このメソッドは、インスタンスの型に型のシグネチャを一致させるために、型のシグネチャと組み合わせて使用されます。 


**IDebugHostType2/IDebugHostType 組み込みメソッド**

次の IDebugHostType メソッドは、組み込み型 (または列挙型などの組み込みのデータを保持する型) に固有です。 

```cpp
STDMETHOD(GetIntrinsicType)(_Out_opt_ IntrinsicKind *intrinsicKind, _Out_opt_ VARTYPE *carrierType) PURE;
```

[GetIntrinsicType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getintrinsictype)

GetIntrinsicType メソッドは、どのような組み込み型は、に関する情報を返します。 このメソッドからは、2 つの値が返されます。 

- 組み込みの種類は、全体的な型を示します (例:: 整数、符号なしの浮動小数点) が、型のサイズではなく (例。8 ビット、16 ビット、32 ビット、64 ビット)
- 通信事業者の種類は、組み込みの種類を VARIANT 構造体にパックする方法を示します。 Vt _ を付けます * 定数です。

2 つの値の組み合わせでは、組み込みのに関する情報の完全なセットを提供します。 


**ビット フィールドの IDebugHostType2/IDebugHostType メソッド**

次の IDebugHostType メソッドは、ビット フィールドにデータを格納する型に固有です。 組み込み関数内のビット フィールドの配置についての情報は、型のシンボルの場所の属性ではなく、データ モデルの一部として格納されます。 

```cpp
STDMETHOD(GetBitField)(_Out_ ULONG* lsbOfField, _Out_ ULONG* lengthOfField) PURE;
```

[GetBitField](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getbitfield)

データ構造の指定されたメンバーがビット フィールド (例。フィールドの型情報が備える ULONG MyBits:8)、ビット フィールドの配置に関する情報。 GetBitField メソッドは、情報を取得するために使用します。 このメソッドは、ビット フィールドではない任意の型では失敗します。 これは、唯一の理由が、このメソッドは失敗します。 単にこのメソッドを呼び出すと、成功/失敗を調べるには、非ビット フィールドからのビット フィールドを区別するために十分です。 ハーフ オープン セットによって、フィールドの位置が定義されているビット フィールドを指定された型が発生する場合 *(lsbOfField + lengthOfField: lsbOfField]*


**IDebugHostType2/IDebugHostType ポインター関連メソッド**

次の IDebugHostType メソッドは、ポインター型に固有です。 GetTypeKind が TypePointer または TypeMemberPointer を返しますの種類など、'。 

```cpp
STDMETHOD(GetPointerKind)(_Out_ PointerKind* pointerKind) PURE;
STDMETHOD(GetMemberType)(_Out_ IDebugHostType** memberType) PURE;
```
[GetPointerKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getpointerkind)

型のポインターである場合は、GetPointerKind メソッドは、ポインターの種類を返します。 これは、PointerKind 列挙体によって定義されます。

[GetMemberType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getmembertype)

メンバーへのポインターである型の (と示されます TypeMemberPointer の型の種類によって)、GetMemberType メソッドは、ポインターは、ポインター メンバーへのクラスを返します。 


**IDebugHostType2/IDebugHostType 配列関連メソッド**

配列は GetTypeKind が TypeArray を返す型です。 配列デバッグ ホストの型システムで定義されていないこと、0 個のインデックス ベース、パックされた線形 1 次元配列 C を使用する 1 つの次元の場合と同じに注意してください。 C スタイル配列に、定義に合わせてが配列の範囲全体が IDebugHostType で広くなります。 デバッグ ホストで、配列は多次元があり、配列内の各ディメンションが、ArrayDimensionThis 記述子は、次のフィールドと呼ばれる記述子で定義されています。 



フィールド | 説明
|--------------|------------------|
LowerBound | 符号付き 64 ビット値として、配列のベース インデックス。 C スタイル配列にこの常に 0 になります。 必要はありません。 配列の個々 のディメンションは、負の値の 1 つであっても、任意の 64 ビットのインデックス位置にある開始を見なすことができます。
長さ | 符号なし 64 ビットの値として、配列の次元の長さ。 配列のインデックスにまたがるハーフ オープン セット [LowerBound、LowerBound + 長さ)。
stride | 配列の次元のストライドを定義します。 このディメンションのインデックス内に 1 つ (N N + 1) からの増加、メモリ内で前方に移動するバイト数を示します。 C スタイル配列の場合、配列の各要素のサイズになります。 する必要はありません。 要素間の余白は、各要素のサイズよりも大きい stride として表現できます。 多次元配列は、この値ディメンション全体を前方に移動する方法を示します。 M N 行列 x を検討してください。 これは、2 つのディメンションとして行優先の形式で記述可能性があります。 

```cpp   
{ [LowerBound: 0, Length: M, Stride: N \* sizeof(element)], [LowerBound: 0, Length: N, Stride: sizeof(element)]} 
```
または、別の方法として列優先形式で説明されている 2 つのディメンションとしてにすることが考えられます。 

```cpp   
{ [LowerBound: 0, Length: M, Stride: sizeof(element)], [LowerBound: 0, Length: N, Stride: M \* sizeof(element)]} 
```
ArrayDimension 概念は、このレベルの柔軟性を使用できます。 

次の IDebugHostType メソッドは、配列型に固有です。 

```cpp
STDMETHOD(GetArrayDimensionality)(\_Out_ ULONG64\* arrayDimensionality) PURE; 
STDMETHOD(GetArrayDimensions)(\_In_ ULONG64 dimensions, \_Out_writes_(dimensions) ArrayDimension \*pDimensions) PURE;
```

[GetArrayDimensionality](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getarraydimensionality)

GetArrayDimensionality メソッドは、配列のインデックスが設定されたディメンションの数を返します。 C スタイル配列では、値は、ここでは常に 1 を返します。 

[GetArrayDimensions](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getarraydimensions)

GetArrayDimensions メソッドは、記述子 GetArrayDimensionality メソッドで示されている配列の各次元のいずれかのセットを返します。 各記述子は、開始インデックス、長さ、および各配列の次元の前方のストライドを記述する ArrayDimension 構造です。 これにより、C の型システムで許可されてよりも大幅に強化の配列構造の説明です。 

C スタイル配列で 1 つの配列のディメンションが返されますここでは常に値を持つ。 

- 下限 = 0
- 長さ ARRAYSIZE(array) を =
- Stride sizeof(elementType) を =


**IDebugHostType2/IDebugHostType 関数関連メソッド**

関数型 TypeFunction の一種を使用していることを示す型は、IDebugHostType と IDebugHostType2 の両方で、次のメソッドをサポートします。 

```cpp
//
// IDebugHostType:
//
STDMETHOD(GetFunctionCallingConvention)(_Out_ CallingConventionKind* conventionKind) PURE;
STDMETHOD(GetFunctionReturnType)(_COM_Outptr_ IDebugHostType** returnType) PURE;
STDMETHOD(GetFunctionParameterTypeCount)(_Out_ ULONG64* count) PURE;
STDMETHOD(GetFunctionParameterTypeAt)(_In_ ULONG64 i, _Out_ IDebugHostType** parameterType) PURE;
//
// IDebugHostType2:
//
STDMETHOD(GetFunctionVarArgsKind)(_Out_ VarArgsKind* varArgsKind) PURE;
```

[GetFunctionCallingConvention](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getfunctioncallingconvention)

GetFunctionCallingConvention メソッドは、関数の呼び出し規約を返します。 このような CallingConventionKind 列挙体のメンバーとして返されます。 

[GetFunctionReturnType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionreturntype)

GetFunctionReturnType メソッドは、関数の戻り値の型を返します。 

[GetFunctionParameterTypeCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionparametertypecount)

GetFunctionParameterTypeCount メソッドは、関数が受け取る引数の数を返します。 この数に C と C++ の省略記号ベースの可変個引数のマーカーがないと見なされることに注意してください。 GetFunctionVarArgsKind メソッドを使用して、このような存在を検出する必要があります。 これはのみ、省略記号の前に引数が含まれます。 

[GetFunctionParameterTypeAt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionparametertypeat)

GetFunctionParameterTypeAt メソッドは、関数に、i 番目の引数の型を返します。 

GetFunctionVarArgsKind メソッドを返します、特定の関数は、可変個引数リストを利用し、そうである場合の可変個の引数には、どのようなスタイルで、日頃かどうか。 このようなは、次のように定義される VarArgsKind 列挙体のメンバーによって定義されます。 

 な列挙 | 説明
|---------|---------|
VarArgsNone | 関数は、変数引数を受け取りません。
VarArgsCStyle | C スタイルの varargs 関数 (returnType (arg1, arg2,...)) です。関数によって報告された引数の数では、省略記号の引数は含まれません。 変数引数を渡すには、GetFunctionParameterTypeCount メソッドによって返される引数の数の後に発生します。


**IDebugHostType2 GetFunctionVarArgsKind**

GetFunctionVarArgsKind メソッドを返します、特定の関数は、可変個引数リストを利用し、そうである場合の可変個の引数には、どのようなスタイルで、日頃かどうか。 このようなは、次のように定義される VarArgsKind 列挙体のメンバーによって定義されます。 


**IDebugHostType2/IDebugHostType Typedef 関連メソッド**

Typedef である任意の型は、型は、最終的な型、typedef の基になるかのように動作します。 これは、ある GetTypeKind などのメソッドは示しません型が typedef であることを意味します。 同様に、GetBaseType では、定義が参照する型が返されません。 Typedef の基になる最後の定義で呼び出されたかのように動作を示しているは代わりにします。 例。 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```

IDebugHostType ' PMYSTRUCT または PTRMYSTRUCT のいずれかに、次の情報を報告します。 

- GetTypeKind メソッドでは、TypePointer を返します。 MYSTRUCT を入力して、最終的な基になる * が実際のポインター。
- ' GetBaseType メソッドは MYSTRUCT の型を返します。 MYSTRUCT の基になる型 * MYSTRUCT です。

ここで唯一の違いは、IDebugHostType2 の typedef の特定のメソッドの動作です。 これらのメソッドは次のとおりです。 

```cpp
STDMETHOD(IsTypedef)(_Out_ bool* isTypedef) PURE;
STDMETHOD(GetTypedefBaseType)(_Out_ IDebugHostType2** baseType) PURE;
STDMETHOD(GetTypedefFinalBaseType)(_Out_ IDebugHostType2** finalBaseType) PURE;
```

この例では: 

- PMYSTRUCT と PTRMYSTRUCT IsTypedef メソッドは true を返します
- MYSTRUCT GetTypedefBaseType メソッドを返します * PMYSTRUCT と PTRMYSTRUCT の PMYSTRUCT
- MYSTRUCT GetTypedefFinalBaseType メソッドを返します * の両方の種類

[IsTypedef](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype2-istypedef)

IsTypedef メソッドは、型が typedef であるかどうかを確認できる唯一の方法です。 GetTypeKind メソッドは、基になる型で呼び出された場合のように動作します。 

[GetTypedefBaseType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype2-gettypedefbasetype)

GetTypedefBaseType メソッドでは、typedef の即時どのような定義を返します。 ドキュメントの説明の例。 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```
このメソッドは MYSTRUCT を返します * PMYSTRUCT と PTRMYSTRUCT の PMYSTRUCT します。


[GetTypedefFinalBaseType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype2-gettypedeffinalbasetype)

GetTypedefFinalBaseType メソッドでは、typedef の定義は、最後の種類を返します。 Typedef がもう 1 つの typedef の定義の場合は、次の定義のチェーンの typedef ではないと、返される型の型に達するまでこれは引き続き。 ドキュメントの説明の例。 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```

このメソッドは MYSTRUCT を返します * PMYSTRUCT または PTRMYSTRUCT のいずれかで呼び出されるとします。 

**IDebugHostType2/IDebugHostType 型の作成方法**

```cpp
STDMETHOD(CreatePointerTo)(_In_ PointerKind kind, _COM_Outptr_ IDebugHostType** newType) PURE;
STDMETHOD(CreateArrayOf)(_In_ ULONG64 dimensions, _In_reads_(dimensions) ArrayDimension *pDimensions, _COM_Outptr_ IDebugHostType** newType) PURE;
```

**定数のシンボル値:IDebugHostConstant**

定数の値が (特定の値は定数値である可能性がありますいないシンボル) シンボリック情報に存在する場所については、IDebugHostConstant インターフェイスは、そのような定数の概念を表現します。 これは、テンプレート引数が指定された引数が型では、通常、代わりに、非型テンプレート引数がありますなどの場所で通常使用される (例:: 定数)。 

IDebugHostConstant インターフェイスは、(IDebugHostSymbol によって実装される汎用のメソッドを無視します) を次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IDebugHostConstant, IDebugHostSymbol)
{
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostconstant-getvalue)

GetValue メソッドは、バリアントにパックされている定数の値を返します。 IDebugHostSymbol 上、GetType メソッドが、定数のシンボルに特定の型を返す可能性がありますに重要です。 このような場合は、定数値の型のシンボルで定義されているが同じである、パッキングとしてここで、GetValue メソッドによって返される保証はありません。 


**データ メンバーのアクセス:IDebugHostField**

IDebugHostField クラスは、クラス、構造体、共用体、または他の種類の構造体のデータ メンバーであるシンボルを表します。 これは無料のデータを表しません (例:: グローバル データ)。 インターフェイスは、次のとおりです (IDebugHostSymbol にジェネリック メソッドを無視します) として定義されます。 

```cpp
DECLARE_INTERFACE_(IDebugHostField, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetOffset)(_Out_ ULONG64* offset) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

[GetLocationKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostfield-getlocationkind)

GetLocationKind メソッドで、シンボルの場所の種類を返しますに LocationKind 列挙します。 このような列挙には、次の値のいずれかを指定できます。 

な列挙 | 説明
|---------|--------|
LocationMember | フィールドは、クラス、構造体、共用体、または他の種類の構造体の通常のデータ メンバーです。 親の型コンス トラクターのベース アドレスに対して相対的なオフセットがあります。 このようなベース アドレスが、これによって表される通常のポインター。 GetOffset メソッドを使用して、フィールドのオフセットを取得できます。 LocationMember、フィールド、GetLocation と GetValue メソッドは失敗します。
LocationStatic | フィールドは静的であり、独自のアドレスします。 GetLocation メソッドは抽象場所を返します (例:: アドレス) の静的フィールド。 LocationStatic、フィールド、GetOffset と GetValue メソッドは失敗します。
LocationConstant | フィールドは定数であり、値です。 GetValue メソッドでは、定数の値を返します。 GetOffset と GetLocation メソッドは、LocationConstant フィールドの失敗します。
LocationNone | フィールドには、場所がありません。 可能性がありますに最適化されていますが、コンパイラによって、または宣言されているが定義されていることはありませんが、静的フィールドがある可能性があります。 方法に、そのフィールドが追加されたに関係なく、物理的な操作または値がありません。 シンボルのみになります。 すべての取得方法 (GetOffset、GetLocation、および GetValue) LocationNone であるフィールドは失敗します。

[GetOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostfield-getoffset)

オフセットを含むフィールド (例:: フィールドがある場所の種類が LocationMember を示します)、GetOffset メソッドは、含んでいる型のベース アドレスからオフセットを返します (、このポインター) フィールド自体のデータをします。 このようなオフセットは常に、64 ビットの符号なしの値として表されます。 指定されたフィールドは、含んでいる型のベース アドレスからのオフセットである場所を持たない GetOffset メソッドは失敗します。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostfield-getlocation)

特定の型のインスタンスに関係なく、アドレスを含むフィールド用 (例:: フィールドがある場所の種類が LocationStatic を示します)、GetLocation メソッドでは、フィールドの抽象場所 (アドレス) を返します。 指定されたフィールドが静的な場所を持たない場合、GetLocation メソッドは失敗します。 

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostfield-getvalue)

シンボリック情報内で定義された定数値があるフィールド (例:: フィールドがある場所の種類が LocationConstant を示します)、GetValue メソッドは、フィールドの定数値を返します。 指定されたフィールドが定数の値を持たない場合は、GetValue メソッドは失敗します。 


**無料のデータ アクセス:IDebugHostData**

別の型のメンバーではないモジュール内のデータは、IDebugHostData インターフェイスによって表されます。 そのインターフェイスは、次のとおりです (IDebugHostSymbol にジェネリック メソッドを無視します) として定義されます。 

```cpp
DECLARE_INTERFACE_(IDebugHostData, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

これらのメソッドのすべては IDebugHostField 内の対応するのと同じ意味です。 唯一の違いは、GetLocationKind メソッドは無料のデータの LocationMember 事項を返すことことはありません。 

[GetLocationKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostdata-getlocationkind)

GetLocationKind メソッドで、シンボルの場所の種類を返しますに LocationKind 列挙します。 この列挙体の説明は IDebugHostField のドキュメントに記載されています。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostdata-getlocation)

アドレスが与えられたデータでは、GetLocation メソッドは、フィールドの抽象場所 (アドレス) を返します。 指定されたデータが静的な場所を持たない場合、GetLocation メソッドは失敗します。 

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostdata-getvalue)

あるいはがシンボリック情報内で定義された定数値 (例: データの場所の種類が LocationConstant を示します)、GetValue メソッドは、フィールドの定数値を返します。 指定されたデータが定数の値を持たない場合は、GetValue メソッドは失敗します。 


**基本クラス。IDebugHostBaseClass**

指定された型の継承階層は、型のシンボルの子を使って表されます。 場合は、指定された型は、(継承 wise) を 1 つまたは複数の型から派生、型の型のシンボルの 1 つまたは複数の SymbolBaseClass 子があります。 これら SymbolBaseClass シンボルは、特定の型から直接継承を表します。 基底クラスの名前は、両方 SymbolBaseClass シンボルの名前と基底クラスの型のシンボルです。 基底クラス自体の型のシンボルを取得する SymbolBaseClass シンボル、GetType メソッドを使用できます。 完全な継承階層は、SymbolBaseClass 子シンボルの調査を再帰的にスキャンできます。 これらのシンボルの基本クラスの各は次のとおりです (IDebugHostSymbol にジェネリック メソッドを無視します) として定義されている IDebugHostBaseClass インターフェイスによって表されます。 

```cpp
DECLARE_INTERFACE_(IDebugHostBaseClass, IDebugHostSymbol)
{
    STDMETHOD(GetOffset)(_Out_ ULONG64* offset) PURE;
}
```

[GetOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostbaseclass-getoffset)

GetOffset メソッドは、派生クラスの基本アドレスからの基本クラスのオフセットを返します。 このようなオフセットでは、0 または正の符号なし 64 ビット値があります。 


**パブリック シンボル:IDebugHostPublic**

パブリック シンボルは、パブリック シンボル ファイル内でテーブルには点を表します。 実際には、アドレスをエクスポートします。 パブリック シンボル--アドレスだけに関連付けられている種類の情報はありません。 呼び出し元によってパブリック シンボルを明示的に要求しない限り、プライベート シンボルのすべての照会を返すデバッグ ホストが優先されます。 パブリック シンボルは、次のとおりです (IDebugHostSymbol にジェネリック メソッドを無視します) として定義されている IDebugHostPublic インターフェイスによって表されます。 

```cpp
DECLARE_INTERFACE_(IDebugHostPublic, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
}
```

これらのメソッドのすべては IDebugHostField 内の対応するのと同じ意味です。 唯一の違いは、こと GetLocationKind メソッドが返すことはありません LocationMember または LocationConstant このようなシンボルです。 

[GetLocationKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostpublic-getlocationkind)

GetLocationKind メソッドで、シンボルの場所の種類を返しますに LocationKind 列挙します。 この列挙体の説明は IDebugHostField のドキュメントに記載されています。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostpublic-getlocation)

アドレスが与えられたデータでは、GetLocation メソッドは、フィールドの抽象場所 (アドレス) を返します。 指定されたパブリックでは、静的な場所はありません、GetLocation メソッドは失敗します。 


**モジュールの署名とバージョンの一致:IDebugHostModuleSignature**

モジュール署名は、指定したモジュールが一連の名前付けとバージョン管理に関する基準を満たしているかどうかを確認する手段を表します。 モジュール署名が IDebugHostSymbols で CreateModuleSignature メソッドを使用して作成されます。 モジュール名とモジュールのバージョン番号の省略可能な範囲に一致することができます。 このような署名が作成されると、クライアントは次のように定義されている IDebugHostModuleSignature インターフェイスを受け取ります。 

```cpp
DECLARE_INTERFACE_(IDebugHostModuleSignature, IUnknown)
{
    STDMETHOD(IsMatch)(_In_ IDebugHostModule* pModule, _Out_ bool* isMatch) PURE;
}
```

[IsMatch](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodulesignature-ismatch)

IsMatch メソッドは、モジュール名とバージョン、シグネチャに示されている名前とバージョンの範囲を比較する、署名に対して (IDebugHostModule 記号で指定) として、特定のモジュールを比較します。 指定したモジュールのシンボルが、署名と一致するかどうかを示す値が返されます。 

**署名と型の照合を入力します。IDebugHostTypeSignature**

型のシグネチャは、特定の型のインスタンスが、一連の型の名前、型、および種類が内にあるモジュールを汎用引数に関する条件を満たすかどうかを確認する手段を表します。 型シグネチャが IDebugHostSymbols で CreateTypeSignature メソッドを使用して作成されます。 このような署名が作成されると、クライアントは次のように定義されている IDebugHostTypeSignature インターフェイスを受け取ります。 

```cpp
DECLARE_INTERFACE_(IDebugHostTypeSignature, IUnknown)
{
    STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
    STDMETHOD(IsMatch)(_In_ IDebugHostType* type, _Out_ bool* isMatch, _COM_Outptr_opt_ IDebugHostSymbolEnumerator** wildcardMatches) PURE;
    STDMETHOD(CompareAgainst)(_In_ IDebugHostTypeSignature* typeSignature, _Out_ SignatureComparison* result) PURE;
}
```

[GetHashCode](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttypesignature-gethashcode)

GetHashCode メソッドでは、型シグネチャの 32 ビットのハッシュ コードを返します。 デバッグ ホストは、実装型のインスタンスに対して返されるハッシュ コードと型のシグネチャに対して返されるハッシュ コードの間で同期があることを保証します。 グローバルな一致を除く、型のインスタンスは、型シグネチャを一致させることがある場合両方が同じ 32 ビットのハッシュ コード。 これにより、迅速な初期の比較と、型のインスタンス、多種多様なデータ モデルのマネージャーに登録されている型のシグネチャと一致します。 

[IsMatch](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttypesignature-ismatch)

IsMatch メソッドは、特定の型のインスタンスが型シグネチャで指定された条件に一致するかどうかを示す値を返します。 場合は、すべての型シグネチャ内のワイルドカードに一致する (シンボル) として型のインスタンスの特定の部分を示す列挙子とこれを示す値が返されます。 

[CompareAgainst](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttypesignature-compareagainst)

CompareAgainst メソッドは、型シグネチャに別の型シグネチャを比較し、2 つの署名の比較を返します。 返される比較結果は、次のように定義されている SignatureComparison 列挙体のメンバーです。 

な列挙 | 説明
|---------|-----------|
関連付けられていません。 | 2 つの署名または比較対象となる型の関係はありません。
あいまいな |1 つの署名または型に対して、あいまいと比較します。 2 つの型シグネチャでしたか署名にも同じように一致する潜在的な型のインスタンスがあることを意味します。 たとえば、次に示す 2 つの型シグネチャがあいまいです。  1 の署名:`std::pair<*, int>`  署名 2:`std::pair<int,*>`ため、型のインスタンス`std::pair<int, int>`いずれも同じように (両方がある 1 つの具象型と 1 つのワイルドカード) 一致します。
LessSpecific | 1 つの署名または型は、他方より小さい固有です。 多くの場合、つまりより一般的な署名がワイルドカードより特定の 1 つの具象型があります。 例として、以下の最初の署名は、2 番目よりも限定です。 1 の署名:`std::pair<*, int>` 署名 2:`std::pair<int, int>`ワイルドカードがあるため、(、 `*`)、2 つ目の具象型 (int) があります。
MoreSpecific | 1 つの署名または型は、他よりも具体的です。 多くの場合、つまり、特定の署名が具象型低い特定の 1 つのワイルドカードがあります。 たとえば、以下の最初の署名は、2 番目よりも具体的です。 1 の署名:`std::pair<int, int>` 署名 2:`std::pair<*, int>`ワイルドカードの 2 つ目が、具体的な型 (int) があるため、(、 `*`)。
同じです。 | 2 つのシグネチャや型は同じです。







---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[デバッガー データ モデルの C++ の概要](data-model-cpp-overview.md)

[デバッガーのデータ モデルの C++ インターフェイス](data-model-cpp-interfaces.md)

[デバッガーのデータ モデルの C++ オブジェクト](data-model-cpp-objects.md)

[デバッガーのデータ モデルの C++ の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーのデータ モデルの C の概念](data-model-cpp-concepts.md)

[デバッガー データ モデルの C++ のスクリプト](data-model-cpp-scripting.md)
