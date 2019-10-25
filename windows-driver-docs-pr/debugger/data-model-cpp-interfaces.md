---
title: Debugger Data Model C++ のインターフェイス
description: このトピックでは、デバッガーのデータモデルC++インターフェイスを使用して、デバッガーの機能を拡張およびカスタマイズする方法について説明します。
ms.date: 10/08/2018
ms.openlocfilehash: 90a0efd006ad0ff9237d2c4af0943fcf07e38e03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837809"
---
# <a name="debugger-data-model-c-interfaces"></a>Debugger Data Model C++ のインターフェイス 

このトピックでは、デバッガーデータモデルC++インターフェイスを使用してデバッガーの機能を拡張およびカスタマイズする方法の概要を説明します。

## <a name="span-idhostinterfacespan-debugger-data-model-c-host-interfaces"></a><span id="hostinterface"></span>デバッガーデータモデルC++のホストインターフェイス

**デバッガーデータモデルホスト**

デバッガーデータモデルは、さまざまな異なるコンテキストでホストできる、コンポーネント化されたシステムとして設計されています。 通常、データモデルは、デバッガーアプリケーションのコンテキストでホストされます。 データモデルのホストにするには、デバッガーの主要な側面を公開するために、いくつかのインターフェイスを実装する必要があります。これには、ターゲット、メモリ空間、エバリュエーター、シンボルと型システムなどが含まれます。これらのインターフェイスは、データモデルをホストするアプリケーションによって実装されますが、コアデータモデルと、データモデルと相互運用する任意の拡張機能によって使用されます。 

コアインターフェイスのセットは次のとおりです。 

インターフェイス名 | 説明
|--------------|---------------|
IDebugHost | デバッグホストへのコアインターフェイス。
IDebugHostStatus  | クライアントがホストの状態を照会できるようにするインターフェイス。
IDebugHostContext  | ホスト内でのコンテキストの抽象化 (例: 特定のターゲット、特定のプロセス、特定のアドレス空間など)。
IDebugHostErrorSink  | ホストとデータモデルの特定の部分からのエラーを受信するために呼び出し元によって実装されるインターフェイス
IDebugHostEvaluator / IDebugHostEvaluator2  | デバッグホストの式エバリュエーター。
IDebugHostExtensibility  | ホストまたはその一部 (式エバリュエーターなど) の機能を拡張するためのインターフェイスです。

型システムとシンボリックインターフェイスは次のとおりです。 

InterfaceName | 説明
|--------------|---------------|
IDebugHostSymbols | シンボルへのアクセスと解決を提供するコアインターフェイス
IDebugHostSymbol / IDebugHostSymbol2  | 任意の種類の1つの記号を表します。 特定のシンボルは、このインターフェイスの派生です。
IDebugHostModule | プロセス内に読み込まれたモジュールを表します。 これは一種のシンボルです。
IDebugHostType / IDebugHostType2  | ネイティブ/言語の型を表します。
IDebugHostConstant  | シンボル情報内の定数を表します (例: のC++非型テンプレート引数)
IDebugHostField  | 構造体またはクラス内のフィールドを表します。
IDebugHostData | モジュール内のデータを表します (これは、構造体またはクラス内では IDebugHostField になります)。
IDebugHostBaseClass | 基本クラスを表します。
IDebugHostPublic  | PDB の publics テーブル内のシンボルを表します。 これには、型情報が関連付けられていません。 これは名前とアドレスです。
IDebugHostModuleSignature | モジュール署名を表します。これは、名前またはバージョン別にモジュールのセットと一致する定義です
IDebugHostTypeSignature | 型シグネチャを表します。これは、モジュール名または名前によって型のセットに一致する定義です


**コアホストインターフェイス: IDebugHost**

IDebugHost インターフェイスは、任意のデータモデルホストのコアインターフェイスです。 次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDebugHost, IUnknown)
{
    STDMETHOD(GetHostDefinedInterface)(_COM_Outptr_ IUnknown** hostUnk) PURE;
    STDMETHOD(GetCurrentContext)(_COM_Outptr_ IDebugHostContext** context) PURE;
    STDMETHOD(GetDefaultMetadata)(_COM_Outptr_ IKeyStore** defaultMetadataStore) PURE;
}
```

[GetHostDefinedInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughost-gethostdefinedinterface)

GetHostDefinedInterface メソッドは、ホストのメインプライベートインターフェイスが、指定されたホストに存在する場合はそれを返します。 Windows 用のデバッグツールでは、ここで返されるインターフェイスは IDebugClient (IUnknown にキャスト) です。 

[GetCurrentContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughost-getcurrentcontext)

GetCurrentContext メソッドは、デバッガーホストの現在の状態を表すインターフェイスを返します。 これの正確な意味はホストに残されていますが、通常は、デバッグホストのユーザーインターフェイスでアクティブになっているセッション、プロセス、アドレス空間などが含まれます。 返されたコンテキストオブジェクトは、ほとんどの場合、呼び出し元には見えませんが、デバッグホストの呼び出しの間に渡す重要なオブジェクトです。 たとえば、呼び出し元がメモリを読み取る場合は、メモリの読み取り元のプロセスとアドレス空間を把握しておくことが重要です。 この概念は、このメソッドから返されるコンテキストオブジェクトの概念にカプセル化されています。 

[GetDefaultMetadata](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughost-getdefaultmetadata)

GetDefaultMetadata メソッドは、明示的なメタデータが渡されていない場合に特定の操作 (例: 文字列の変換) に使用できる既定のメタデータストアを返します。 これにより、デバッグホストはデータの表示方法を制御できるようになります。 たとえば、既定のメタデータには PreferredRadix キーを含めることができます。これにより、ホストは、特に指定されていない場合に、序数を10進数または16進数で表示するかどうかを指定できます。 

既定のメタデータストアのプロパティ値は、手動で解決する必要があり、既定のメタデータのクエリ対象となるオブジェクトを渡す必要があることに注意してください。 Getkey の代わりに GetKey メソッドを使用する必要があります。 

**状態インターフェイス: IDebugHostStatus** 

IDebugHostStatus インターフェイスを使用すると、データモデルまたはデバッグホストのクライアントは、デバッグホストの状態の特定の側面を照会できます。 インターフェイスは次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IDebugHostStatus, IUnknown)
{
    STDMETHOD(PollUserInterrupt)(_Out_ bool* interruptRequested) PURE;
}
```

[PollUserInterrupt](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughoststatus-polluserinterrupt)

PollUserInterrupt メソッドは、デバッグホストのユーザーが現在の操作の中断を要求したかどうかを照会するために使用されます。 たとえば、データモデル内のプロパティアクセサーでは、任意のコード (JavaScript メソッドなど) を呼び出すことができます。 そのコードは、任意の時間を要することがあります。 デバッグホストの応答性を維持するために、任意の時間を要する可能性のあるコードでは、このメソッドを呼び出すことによって、割り込み要求を確認する必要があります。 InterruptRequested 値が true として返された場合、呼び出し元はすぐに中止し、E_ABORT の結果を返す必要があります。 


**コンテキストインターフェイス: IDebugHostContext**

Context は、データモデルと基になるデバッグホストの最も重要な側面の1つです。 オブジェクトを保持する場合は、オブジェクトがどこから送信されたかを把握しておくことが重要です。これは、どのプロセスがどのようなものであるか、どのようなアドレス空間が関連付けられているかを把握できることです。 この情報を知っておくと、ポインター値などの正しい解釈を行うことができます。 IDebugHostContext 型のオブジェクトは、デバッグホストの多くのメソッドに渡す必要があります。 このインターフェイスは、さまざまな方法で取得できます。

- デバッガーの現在のコンテキストを取得する方法: IDebugHost の GetCurrentContext メソッドの呼び出し
- オブジェクトのコンテキストを取得する方法: IModelObject の GetContext メソッドの呼び出し
- シンボルのコンテキストを取得する方法: IDebugHostSymbol の GetContext メソッドの呼び出し

さらに、2つの値があります。これは、IDebugHostContext インターフェイスのコンテキストでは、データモデルまたはデバッグホストメソッドによって返されるか、またはこのインターフェイスに渡されます。 

*nullptr*: コンテキストが存在しないことを示します。 一部のオブジェクトがコンテキストを持たない場合は、完全に有効です。 データモデルのルート名前空間にあるデバッガーオブジェクトは、特定のプロセスまたはアドレス空間内のものを参照していません。 コンテキストがありません。

*USE_CURRENT_HOST_CONTEXT*: 一方がデバッグホストの現在の UI コンテキストを使用する必要があることを示す sentinel 値。 この値は、デバッグホストからは返されません。 ただし、IDebugHost の GetCurrentContext メソッドを明示的に呼び出す代わりに入力 IDebugHostContext を受け取るデバッグホストメソッドに渡すこともできます。 USE_CURRENT_HOST_CONTEXT を明示的に渡すことは、多くの場合、現在のコンテキストを明示的に取得するよりもパフォーマンスに優れています。 

ホストコンテキストのコンテキストは、ほとんどの場合、呼び出し元に対して非透過的です。 コアデバッグホストの外部の呼び出し元がホストコンテキストで実行できる唯一の操作は、別のホストコンテキストと比較することです。 

IDebugHostContext インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDebugHostContext, IUnknown)
{
    STDMETHOD(IsEqualTo)(_In_ IDebugHostContext *pContext, _Out_ bool *pIsEqual) PURE;
}
```

[IsEqualTo](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostcontext-isequalto)

IsEqualTo メソッドは、ホストコンテキストを別のホストコンテキストと比較します。 2つのコンテキストが等しい場合は、このを示す値が返されます。 この比較は、インターフェイスの等価性ではないことに注意してください。 これにより、コンテキスト自体の基になる非透過コンテンツが比較されます。 


**エラーシンク: IDebugHostErrorSink**

IDebugHostErrorSink は、特定の操作中に発生したエラーの通知をクライアントが受信し、必要に応じてそれらのエラーをルーティングする手段です。 インターフェイスは次のように定義されます。 

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

[ReportError](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosterrorsink-reporterror)

ReportError メソッドは、エラーが発生したことを通知するエラーシンクのコールバックです。シンクは、適切な UI やメカニズムにエラーをルーティングできます。 


**ホストエバリュエーター: IDebugHostEvaluator/IDebugHostEvaluator2**

デバッグホストがクライアントに提供する最も重要な機能の1つは、その言語ベースの式エバリュエーターにアクセスすることです。 IDebugHostEvaluator インターフェイスと IDebugHostEvaluator2 インターフェイスは、デバッグホストからその機能にアクセスするための手段です。 

これらのインターフェイスは、次のように定義されています。 

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

[EvaluateExpression](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostevaluator-evaluateexpression)

EvaluateExpression メソッドを使用すると、デバッグホストに対して言語 (例: C++) 式を評価し、IModelObject としてボックス化された式評価の結果値を返すように要求できます。 メソッドのこの特定のバリアントでは、言語コンストラクトのみを使用できます。 言語に存在しないデバッグホストの式エバリュエーター (LINQ クエリメソッドなど) に表示される追加機能は、評価のために無効になります。 

[EvaluateExtendedExpression](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostevaluator-evaluateextendedexpression)

EvaluateExtendedExpression メソッドは EvaluateExpression メソッドに似ていますが、特定のデバッグホストが式エバリュエーターに追加することを選択する追加の言語以外の機能が再び有効になる点が異なります。 たとえば、Windows 用のデバッグツールでは、匿名型、LINQ クエリ、モジュール修飾子、書式指定子、および C 以外のその他C++の機能を使用できます。 


**IDebugHostEvaluator2**

[割り当て先](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostevaluator2-assignto)

割り当て方法は、デバッグ対象の言語のセマンティクスに従って割り当てを実行します。 


**ホスト機能拡張インターフェイス: IDebugHostExtensibility**

デバッグホストの特定の機能は、必要に応じて、機能拡張に従うことができます。 たとえば、式エバリュエーターを含めることができます。 IDebugHostExtensibility インターフェイスは、これらの拡張ポイントにアクセスするための手段です。 インターフェイスは次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IDebugHostExtensibility, IUnknown)
{
    STDMETHOD(CreateFunctionAlias)(_In_ PCWSTR aliasName, _In_ IModelObject *functionObject) PURE;
    STDMETHOD(DestroyFunctionAlias)(_In_ PCWSTR aliasName) PURE;
}
```

[CreateFunctionAlias](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostextensibility-createfunctionalias)

CreateFunctionAlias メソッドは、一部の拡張機能で実装されているメソッドの "関数エイリアス"、つまり "クイックエイリアス" を作成します。 このエイリアスの意味はホスト固有です。 これは、関数を使用してホストの式エバリュエーターを拡張する場合もあれば、まったく異なる処理を実行する場合もあります。 

[DestroyFunctionAlias](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostextensibility-destroyfunctionalias)

DestroyFunctionAlias メソッドは、CreateFunctionAlias メソッドの前の呼び出しを元に戻します。 関数は、クイックエイリアス名では使用できなくなります。 



## <a name="span-idaccessdatamodel-accessing-the-data-model"></a>データモデルへのアクセスの <span id="accessdatamodel">

まず、データモデルの機能拡張 Api は、データモデルのホストとして機能するアプリケーション (通常はデバッガー) と中立的になるように設計されています。 理論的には、アプリケーションは、アプリケーションのデバッグターゲットの型システムと一連の射影されたオブジェクトを、ターゲット、プロセス、スレッドなどに関するデータモデルの名前空間に公開する一連のホスト Api を提供することで、データモデルをホストできます。これらのデバッグターゲットに含まれています。 

データモデル Api (IDataModel<em>、IDebugHost</em>、IModelObject を開始するもの) は、移植性のあるものとして設計されていますが、"デバッガー拡張機能" を定義していません。 現在、Windows 用のデバッグツールとそれが提供するエンジンを拡張する必要があるコンポーネントは、データモデルにアクセスするためにエンジン拡張機能を記述する必要があります。 このエンジン拡張機能は、拡張機能の読み込みとブートストラップのメカニズムと同様に、エンジン拡張機能である必要があります。 そのため、最小限の実装は次のようになります。 

- **Debugextensioninitialize**: 作成された IDebugClient を利用してデータモデルにアクセスし、オブジェクトモデルの操作を設定するメソッド。
- **Debugextensionuninitialize**解除: Debugextensionuninitialize で実行されたオブジェクトモデルの操作を元に戻すメソッド。
- **Debugextensioncanunload**: 拡張機能をアンロードできるかどうかを返すメソッド。 拡張機能にライブ COM オブジェクトが残っている場合は、これを示す必要があります。 これは、デバッガーの COM の DllCanUnloadNow に相当します。 アンロードできないことを示す S_FALSE が返された場合、デバッガーは後でこのクエリを実行してアンロードが安全かどうかを確認したり、DebugExtensionInitialize を再度呼び出して拡張機能を再初期化したりすることができます。 この拡張機能は、両方のパスを処理できるように準備する必要があります。
- **Debugextensionunload**: DLL のアンロードの直前に必要な最後のクリーンアップを実行するメソッド

*ブリッジインターフェイス: IHostDataModelAccess*

前述のように、DebugExtensionInitialize を呼び出すと、デバッグクライアントが作成され、データモデルにアクセスできるようになります。 このようなアクセスは、Windows 用のデバッグツールおよびデータモデルの従来の IDebug * インターフェイス間のブリッジインターフェイスによって提供されます。 このブリッジインターフェイスは "IHostDataModelAccess" で、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IHostDataModelAccess, IUnknown)
{
   STDMETHOD(GetDataModel)(_COM_Outptr_ IDataModelManager** manager, _COM_Outptr_ IDebugHost** host) PURE;
}
```

[GetDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ihostdatamodelaccess-getdatamodel)

GetDataModel メソッドは、データモデルの両側へのアクセスを提供するブリッジインターフェイスのメソッドです。デバッグホスト (デバッガーの下端) は、データモデルのメインコンポーネントである、返された IDebugHost インターフェイスによって表されます (データモデル)。マネージャーは、返された IDataModelManager インターフェイスによって表されます。



## <a name="span-idsysteminterfacesspan-debugger-data-model-system-interfaces"></a><span id="systeminterfaces"></span>デバッガーデータモデルのシステムインターフェイス

**データモデルホスト**

デバッガーデータモデルは、さまざまな異なるコンテキストでホストできる、コンポーネント化されたシステムとして設計されています。 通常、データモデルは、デバッガーアプリケーションのコンテキストでホストされます。 データモデルのホストにするには、デバッガーの主要な側面を公開するために、いくつかのインターフェイスを実装する必要があります。これには、ターゲット、メモリ空間、エバリュエーター、シンボルと型システムなどが含まれます。これらのインターフェイスは、データモデルをホストするアプリケーションによって実装されますが、コアデータモデルと、データモデルと相互運用する任意の拡張機能によって使用されます。 

型システムとシンボリックインターフェイスは次のとおりです。 


インターフェイス名 | 説明
|--------------|------------------|
IDebugHostSymbols  | シンボルへのアクセスと解決を提供するコアインターフェイス
IDebugHostSymbol / IDebugHostSymbol2  | 任意の種類の1つの記号を表します。 特定のシンボルは、このインターフェイスの派生です。
IDebugHostModule  | プロセス内に読み込まれたモジュールを表します。 これは一種のシンボルです。
IDebugHostType / IDebugHostType2  | ネイティブ/言語の型を表します。
IDebugHostConstant  | シンボル情報内の定数を表します (例: のC++非型テンプレート引数)
IDebugHostField | 構造体またはクラス内のフィールドを表します。
IDebugHostData | モジュール内のデータを表します (これは、構造体またはクラス内では IDebugHostField になります)。
IDebugHostBaseClass  | 基本クラスを表します。
IDebugHostPublic | PDB の publics テーブル内のシンボルを表します。 これには、型情報が関連付けられていません。 これは名前とアドレスです。
IDebugHostModuleSignature | モジュール署名を表します。これは、名前またはバージョン別にモジュールのセットと一致する定義です
IDebugHostTypeSignature | 型シグネチャを表します。これは、モジュール名または名前によって型のセットに一致する定義です

その他のコアインターフェイスは次のとおりです。 

インターフェイス名 | 説明
|--------------|------------------|
IDebugHost | デバッグホストへのコアインターフェイス。
IDebugHostStatus | クライアントがホストの状態を照会できるようにするインターフェイス。
IDebugHostContext | ホスト内でのコンテキストの抽象化 (例: 特定のターゲット、特定のプロセス、特定のアドレス空間など)。
IDebugHostErrorSink | ホストとデータモデルの特定の部分からのエラーを受信するために呼び出し元によって実装されるインターフェイス
IDebugHostEvaluator / IDebugHostEvaluator2 | デバッグホストの式エバリュエーター。
IDebugHostExtensibility | ホストまたはその一部 (式エバリュエーターなど) の機能を拡張するためのインターフェイスです。


**メインのシンボリックインターフェイス: IDebugHostSymbols**

IDebugHostSymbols インターフェイスは、デバッグターゲットのシンボルにアクセスするための主要な開始点です。 このインターフェイスは、IDebugHost のインスタンスからクエリを実行でき、次のように定義されています。 

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

[CreateModuleSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-createmodulesignature)

CreateModuleSignature メソッドは、特定のモジュールのセットを名前で一致させるために使用できる署名を作成します。また、必要に応じてバージョンを指定します。 モジュール署名には、次の3つのコンポーネントがあります。 

- 名前: 一致するモジュールは、署名内の名前と一致する大文字と小文字が区別されない名前を持つ必要があります
- 最小バージョン: 指定されている場合、一致するモジュールは、少なくともこのバージョンの最小バージョンを持つ必要があります。 バージョンは "A. b. d." 形式で指定され、後続の各部分は前よりも重要度が低くなります。 最初のセグメントのみが必須です。
- 最大バージョン: 指定されている場合、一致するモジュールの最大バージョンは、このバージョン以下である必要があります。 バージョンは "A. b. d." 形式で指定され、後続の各部分は前よりも重要度が低くなります。 最初のセグメントのみが必須です。

[CreateTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-createtypesignature)

CreateTypeSignature メソッドは、モジュール名と型名を含む一連の具象型を照合するために使用できるシグネチャを作成します。 型名の署名文字列の形式は、デバッグされる言語 (およびデバッグホスト) に固有です。 C/C++の場合、署名文字列は NatVis 型の仕様に相当します。 つまり、署名文字列は、ワイルドカード (*) がテンプレート引数として許可されている型名です。 

[CreateTypeSignatureForModuleRange](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-createtypesignatureformodulerange)

CreateTypeSignatureForModuleRange メソッドは、モジュールのシグネチャと型名によって具象型のセットを照合するために使用できるシグネチャを作成します。 これは、CreateTypeSignature メソッド違うに似ています。これは、シグネチャに一致する特定のモジュールを渡すのではなく、モジュール署名を作成するために必要な引数を呼び出し元が渡します。CreateModuleSignature メソッド)。 

[EnumerateModules](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-enumeratemodules)

列挙子のメソッドは、特定のホストコンテキストで使用可能なすべてのモジュールを列挙する列挙子を作成します。 そのホストコンテキストは、プロセスコンテキストをカプセル化する場合もあれば、Windows カーネルのようなものをカプセル化する場合もあります。 


[FindModuleByName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-findmodulebyname)

FindModuleByName メソッドは、指定されたホストコンテキストを検索し、指定された名前を持つモジュールを見つけて、それに対するインターフェイスを返します。 ファイル拡張子の有無に関係なく、名前でモジュールを検索することはできます。 

[FindModuleByLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-findmodulebylocation)

FindModuleByLocation メソッドは、指定されたホストコンテキストを検索し、指定した場所によって指定されたアドレスを含むモジュールを判別します。 その後、そのモジュールにインターフェイスが返されます。 

[GetMostDerivedObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-getmostderivedobject)

GetMostDerivedObject は、デバッガーの型システムを使用して、静的な型からオブジェクトのランタイム型を判断します。 このメソッドは、この分析を実行するために、型システムレイヤーで使用できるシンボル情報とヒューリスティックのみを使用します。 このような情報C++には、RTTI (実行時の型情報)、またはオブジェクトの仮想関数テーブルの構造の分析が含まれる場合があります。 IModelObject での推奨されるランタイム型の概念などは含まれません。 分析がランタイム型を見つけられない場合、またはメソッドに渡された静的な型とは異なるランタイム型が見つからない場合は、入力の場所と型が渡される可能性があります。このような理由で、メソッドは失敗しません。 



**コアの個々のシンボルインターフェイス: IDebugHostSymbol**

データモデルホストから返される可能性があるすべてのシンボルは、IDebugHostSymbol から何らかの方法で派生します。 これは、シンボルの種類に関係なく、すべてのシンボルが実装するコアインターフェイスです。 シンボルの種類によっては、指定されたシンボルが、このインターフェイスによって表される特定の種類のシンボルに対してより一意な属性を返す他のインターフェイスのセットを実装する場合があります。 IDebugHostSymbol2/IDebugHostSymbol インターフェイスは、次のように定義されています。 

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

このインターフェイスは、次のように値を持つシンボルの種類の列挙によって区切られた、さまざまな種類のシンボルを表すことに注意してください。 

Enumarant | 意味
|--------------|------------------|
記号  | シンボルの種類が指定されていません 
シンボルモジュール | シンボルはモジュールであり、IDebugHostModule に対してクエリを実行できます。
シンボルの種類 | シンボルは型であり、IDebugHostType に対してクエリを実行できます。
シンボルフィールド | シンボルはフィールド (構造体またはクラス内のデータメンバー) であり、IDebugHostField に対してクエリを実行できます。
シンボル定数 | シンボルは定数値であり、IDebugHostConstant に対してクエリを実行できます。
シンボルデータ | シンボルは、構造体またはクラスのメンバーではなく、IDebugHostData に対してクエリ可能なデータです。
SymbolBaseClass | シンボルは基本クラスであり、IDebugHostBaseClass に対してクエリ可能です。
シンボルパブリック | シンボルは、モジュールの publics テーブル内のエントリ (型情報を持たない) で、IDebugHostPublic に対してクエリ可能です。
シンボル関数 | シンボルは関数であり、IDebugHostData に対してクエリ可能です。

[GetContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbol-getcontext)

GetContext メソッドは、シンボルが有効なコンテキストを返します。 これは、シンボルが存在するデバッグターゲットやプロセス/アドレス空間などを表しますが、他の手段から取得されたコンテキスト ( *Imodelobject*など) とは異なる場合があります。 

[EnumerateChildren](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbol-enumeratechildren)

EnumerateChildren メソッドは、指定されたシンボルのすべての子を列挙する列挙子を返します。 たとえば、 C++型の場合、基本クラス、フィールド、メンバー関数、およびなどはすべて、型シンボルの子と見なされます。 


**モジュールインターフェイス: IDebugHostModule**

いくつかのアドレス空間内に読み込まれるモジュールのデバッガーの概念は、データモデルの2つの異なる方法で表されます。これは、IDebugHostModule インターフェイスを使用した型システムレベルです。 ここでは、モジュールはシンボルであり、モジュールのコア属性は、デバッガーを介してデータモデルレベルで投影されたインターフェイスメソッド呼び出しです。 これは、モジュールの型システム IDebugHostModule 表現の拡張可能なカプセル化です。

IDebugHostModule インターフェイスは、次のように定義されています (IDebugHostSymbol に汎用のメソッドは無視されます)。 

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

[GetImageName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-getimagename)

GetImageName メソッドは、モジュールのイメージ名を返します。 AllowPath 引数の値によっては、返されるイメージ名にイメージの完全パスが含まれる場合と、含まれない場合があります。

[GetBaseLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-getbaselocation)

GetBaseLocation メソッドは、モジュールのベース読み込みアドレスを場所構造体として返します。 モジュールに対して返される場所の構造は、通常、仮想アドレスを参照します。

[GetVersion](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-getversion)

GetVersion メソッドは、モジュールに関するバージョン情報を返します (この情報をヘッダーから正常に読み取ることができることを前提としています)。 (Nullptr 以外の出力ポインターによって) 特定のバージョンが要求され、それを読み取ることができない場合、メソッド呼び出しから適切なエラーコードが返されます。 

[FindTypeByName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-findtypebyname)

FindTypeByName メソッドは、型名によってモジュール内で定義されている型を検索し、その型のシンボルを返します。 このメソッドは、モジュールの子の明示的な再帰によって返されることのない有効な IDebugHostType を返す場合があります。 デバッグホストでは、モジュール自体では使用されていないが、型から派生した型から派生した派生型を作成できます。 例として、構造体の MyStruct がモジュールのシンボルで定義されていても、MyStruct * * 型が使用されていない場合、FindTypeByName メソッドは、型名が明示的にシンボルに含まれていなくても、MyStruct * * の型シンボルを返します。モジュール。 

[Findシンボル Byrva](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-findsymbolbyrva)

Findsymbol Byrva メソッドは、モジュール内の指定された相対仮想アドレスで、一致する1つのシンボルを検索します。 指定された RVA に1つのシンボルがない場合 (例: 複数の一致がある場合)、このメソッドによってエラーが返されます。 このメソッドでは、publics テーブル内のシンボルに対してプライベートシンボルが返されることに注意してください。 

[FindSymbolByName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-findsymbolbyname)

FindSymbolByName メソッドは、モジュール内の指定された名前の1つのグローバルシンボルを検索します。 指定された名前に一致するシンボルが1つもない場合は、このメソッドによってエラーが返されます。 このメソッドでは、publics テーブル内のシンボルに対してプライベートシンボルが返されることに注意してください。 


**型システムへのアクセス: IDebugHostType2/IDebugHostType**

特定の言語/ネイティブ型は、IDebugHostType2 インターフェイスまたは IDebugHostType インターフェイスによって記述されます。 これらのインターフェイスのメソッドの一部は、特定の種類の型にのみ適用されることに注意してください。 指定された型シンボルは、TypeKind 列挙体で記述されているように、次のいずれかの型を参照できます。 

種類の種類 |  説明
|--------------|------------------|
TypeUDT | ユーザー定義型 (構造体、クラス、共用体など)。種類が TypeUDT であるネイティブ型を持つモデルオブジェクトは、ObjectTargetObject の正規表現を持ちます。この場合、型は常に対応する IModelObject 内に保持されます。
TypePointer | ポインター。 種類が TypePointer であるネイティブな型を持つモデルオブジェクトは ObjectIntrinsic の正規表現を持ちます。この場合、ポインターの値は0に拡張され、VT_UI8 に設定され、この64ビット形式の組み込みデータとして保持されます。 TypePointer の型シンボルには、ポインターが指す型の基本型 (GetBaseType メソッドによって返される) があります。
TypeMemberPointer | クラスメンバーへのポインター。 種類が TypeMemberPointer であるネイティブな型を持つモデルオブジェクトには、標準の表現があります (値はポインター値と同じです)。 この値の正確な意味は、コンパイラ/デバッグホスト固有です。
TypeArray | 配列。 種類が TypeArray であるネイティブ型を持つモデルオブジェクトには、ObjectTargetObject の正規表現があります。 配列のベースアドレスはオブジェクトの場所 (GetLocation メソッドによって取得されます) で、配列の型は常に保持されます。 TypeArray のすべての型シンボルには、配列が配列である型の基本型 (GetBaseType メソッドによって返される) があります。
TypeFunction | 関数。
TypeTypedef | Typedef。 種類が TypeTypedef であるネイティブ型を持つモデルオブジェクトには、typedef の基になる最終的な型の正規表現と同一の正規表現があります。 これは、IDebugHostType2 の明示的な typedef メソッドが typedef 情報のクエリに使用されているか、typedef に明示的に登録されているデータモデルがある場合を除き、オブジェクトのエンドユーザーと型情報の両方に対して完全に透過的に表示されます。 GetTypeKind メソッドは TypeTypedef を返さないことに注意してください。 すべてのメソッドは、typedef の基になる最後の型が返す内容を返します。 IDebugHostType2 には typedef 固有のメソッドがあり、typedef 固有の情報を取得するために使用できます。
TypeEnum | 列挙型。 種類が TypeEnum であるネイティブ型を持つモデルオブジェクトには、組み込みの値と型が列挙値と同じである ObjectIntrinsic の正規表現があります。 
TypeIntrinsic | 組み込み (基本型)。 種類が TypeIntrinsic のネイティブ型を持つモデルオブジェクトには、ObjectIntrinsic の正規表現があります。 型情報は、特に、IModelObject に格納されている組み込みデータの variant データ型 (VT_ *) によって、基になる型が完全に記述されている場合、または保持されない場合があります。

IDebugHostType2/IDebugHostType インターフェイス全体は、次のように定義されています (IDebugHostSymbol メソッドは除く)。 

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

**IDebugHostType2/IDebugHostType General メソッド**

次の IDebugHostType メソッドは、GetTypeKind メソッドから返される型に関係なく、すべての型に対して一般的です。 

```cpp
STDMETHOD(GetTypeKind)(_Out_ TypeKind *kind) PURE;
STDMETHOD(GetSize)(_Out_ ULONG64* size) PURE;
STDMETHOD(GetBaseType)(_Out_ IDebugHostType** baseType) PURE;
STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
```

[GetTypeKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-gettypekind)

GetTypeKind メソッドは、シンボルが参照する型 (ポインター、配列、組み込みなど) の種類を返します。 

[GetSize](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getsize)

GetSize メソッドは、型のサイズを返します (での sizeof (型) が完了しC++たかのように)。 

[GetBaseType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getbasetype)

型が別の単一の型の派生クラスである場合 (例: MyStruct * が MyStruct ' から派生している場合)、GetBaseType メソッドは派生の基本型を返します。 ポインターの場合は、が指す型を返します。 配列の場合、配列がの配列であることを返します。 型がそのような派生型でない場合は、エラーが返されます。 

[GetHashCode](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-gethashcode)

GetHashCode メソッドは、型の32ビットのハッシュコードを返します。 グローバル一致を除き (たとえば、ホストで許可されている場合はすべてに一致する型シグネチャ)、特定の型シグネチャに一致するすべての型インスタンスは、同じハッシュコードを返す必要があります。 型のシグネチャを型のインスタンスに一致させるために、このメソッドを型シグネチャと組み合わせて使用します。 


**IDebugHostType2/IDebugHostType 組み込みメソッド**

次の IDebugHostType メソッドは、組み込み型 (または列挙型などの組み込みデータを保持する型) に固有です。 

```cpp
STDMETHOD(GetIntrinsicType)(_Out_opt_ IntrinsicKind *intrinsicKind, _Out_opt_ VARTYPE *carrierType) PURE;
```

[GetIntrinsicType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getintrinsictype)

GetIntrinsicType メソッドは、型の組み込みの種類に関する情報を返します。 このメソッドから2つの値が返されます。 

- 組み込みの種類は、全体の型 (例: 整数、符号なし、浮動小数点) を示しますが、型のサイズは示しません (例: 8 ビット、16ビット、32ビット、64ビット)
- 通信事業者の種類は、組み込みの種類のパックをバリアント構造にする方法を示します。 これは VT_ * 定数です。

2つの値の組み合わせによって、組み込みに関する情報の完全なセットが提供されます。 


**IDebugHostType2/IDebugHostType ビットフィールドメソッド**

次の IDebugHostType メソッドは、ビットフィールドにデータを格納する型に固有のものです。 組み込みの内のビットフィールド配置に関する情報は、場所の属性ではなく、データモデルの型シンボルの一部として格納されます。 

```cpp
STDMETHOD(GetBitField)(_Out_ ULONG* lsbOfField, _Out_ ULONG* lengthOfField) PURE;
```

[GetBitField](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getbitfield)

データ構造体の特定のメンバーがビットフィールド (例: ULONG MyBits: 8) の場合、フィールドの型情報は、ビットフィールドの配置に関する情報と共に保持されます。 GetBitField メソッドを使用して、その情報を取得できます。 このメソッドは、ビットフィールドではない型では失敗します。 これは、メソッドが失敗する唯一の理由です。 このメソッドを呼び出して成功/失敗を確認するだけで、ビットフィールドと非ビットフィールドを区別できます。 特定の型がビットフィールドである場合、フィールドの位置はハーフオープンセット *(lsbOfField + lengthOfField: lsbOfField)* によって定義されます。


**IDebugHostType2/IDebugHostType ポインターに関連するメソッド**

次の IDebugHostType メソッドは、ポインター型に固有です。 このような型は、GetTypeKind が TypePointer または TypeMemberPointer ' を返す型です。 

```cpp
STDMETHOD(GetPointerKind)(_Out_ PointerKind* pointerKind) PURE;
STDMETHOD(GetMemberType)(_Out_ IDebugHostType** memberType) PURE;
```
[Getポインタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getpointerkind)

ポインターである型の場合、Getpointer Kind メソッドはポインターの種類を返します。 これは、ポインターの種類の列挙体によって定義されます。

[GetMemberType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getmembertype)

TypeMemberPointer の型によって示されるように、メンバーへのポインターである型の場合、GetMemberType メソッドは、ポインターがメンバーへのポインターであるクラスを返します。 


**IDebugHostType2/IDebugHostType 配列に関連するメソッド**

配列は、GetTypeKind が TypeArray を返す型です。 デバッグホストの型システムによって定義されている配列は、C で利用される、インデックスベースの1次元配列とは異なります。 C スタイル配列は定義に適していますが、配列全体のスコープは IDebugHostType にあります。 デバッグホスト内の配列は多次元にすることができ、配列内の各次元は ArrayDimensionThis 呼ばれる記述子によって定義されます。この記述子には次のフィールドがあります。 



フィールド | 意味
|--------------|------------------|
LowerBound | 符号付き64ビット値としての配列のベースインデックス。 C スタイルの配列の場合、これは常に0になります。 である必要はありません。 配列の個々の次元は、64ビットの任意のインデックスで開始することを検討できます。
長さ | 配列次元の長さを、符号なし64ビット値として指定します。 配列の決まっは、ハーフオープンセット [下限、下限、長さ) にまたがります。
Stride | 配列の次元のストライドを定義します。 このディメンションのインデックス内の 1 (N から N + 1) の増加については、メモリ内で前方に移動するバイト数を示します。 C スタイルの配列の場合、これは配列の各要素のサイズになります。 である必要はありません。 要素間の埋め込みは、個々の要素のサイズを超える stride として表すことができます。 多次元配列の場合、この値は、ディメンション全体を前方に移動する方法を示します。 M x N 行列を考えてみましょう。 これは、次の2つのディメンションとして行メジャー形式で記述されている可能性があります。 

```cpp   
{ [LowerBound: 0, Length: M, Stride: N \* sizeof(element)], [LowerBound: 0, Length: N, Stride: sizeof(element)]} 
```
または、次の2つのディメンションとして、列メジャー形式で記述することもできます。 

```cpp   
{ [LowerBound: 0, Length: M, Stride: sizeof(element)], [LowerBound: 0, Length: N, Stride: M \* sizeof(element)]} 
```
ArrayDimension の概念により、この程度の柔軟性が実現します。 

次の IDebugHostType メソッドは、配列型に固有です。 

```cpp
STDMETHOD(GetArrayDimensionality)(\_Out_ ULONG64\* arrayDimensionality) PURE; 
STDMETHOD(GetArrayDimensions)(\_In_ ULONG64 dimensions, \_Out_writes_(dimensions) ArrayDimension \*pDimensions) PURE;
```

[GetArrayDimensionality](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getarraydimensionality)

GetArrayDimensionality メソッドは、配列のインデックスが作成されている次元の数を返します。 C スタイルの配列の場合、ここで返される値は常に1になります。 

[GetArrayDimensions](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getarraydimensions)

GetArrayDimensions メソッドは、Getarraydimensions メソッドによって示されるように、配列の各次元に対して1つずつ、一連の記述子を返します。 各記述子は ArrayDimension 構造体であり、各配列次元の開始インデックス、長さ、および前方ストライドを記述します。 これにより、C 型システムで許可されているよりもはるかに強力な配列コンストラクトを記述できます。 

C スタイルの配列の場合は、次のような値を持つ1つの配列ディメンションがここに返されます。 

- 下限 = 0
- 長さ = ARRAYSIZE (配列)
- ストライド = sizeof (elementType)


**IDebugHostType2/IDebugHostType 関数に関連するメソッド**

種類が TypeFunction によって関数型であることを示す型は、IDebugHostType と IDebugHostType2 の両方で次のメソッドをサポートします。 

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

[GetFunctionCallingConvention](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getfunctioncallingconvention)

GetFunctionCallingConvention メソッドは、関数の呼び出し規約を返します。 このような値は、CallingConventionKind 列挙体のメンバーとして返されます。 

[GetFunctionReturnType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionreturntype)

GetFunctionReturnType メソッドは、関数の戻り値の型を返します。 

[GetFunctionParameterTypeCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionparametertypecount)

GetFunctionParameterTypeCount メソッドは、関数によって取得される引数の数を返します。 このカウントでは、C++ C/省略記号に基づく可変個の引数マーカーは考慮されません。 このようなの存在は、GetFunctionVarArgsKind メソッドを使用して検出される必要があります。 省略記号の前に引数のみが含まれます。 

[GetFunctionParameterTypeAt](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionparametertypeat)

GetFunctionParameterTypeAt メソッドは、関数の i 番目の引数の型を返します。 

GetFunctionVarArgsKind メソッドは、指定された関数が可変個の引数リストを利用しているかどうかを返します。その場合、その関数が利用する可変引数のスタイルを返します。 このような定義は、次のように定義されている VarArgsKind 列挙体のメンバーによって定義されます。 

 列挙 | 意味
|---------|---------|
VarArgsNone | 関数は、可変個の引数を受け取りません。
VarArgsCStyle | 関数は C スタイルの varargs 関数です (returnType (arg1, arg2,...))。関数によって報告される引数の数には、省略記号引数は含まれません。 変数引数の引き渡しは、GetFunctionParameterTypeCount メソッドによって返される引数の数の後に行われます。


**IDebugHostType2 GetFunctionVarArgsKind**

GetFunctionVarArgsKind メソッドは、指定された関数が可変個の引数リストを利用しているかどうかを返します。その場合、その関数が利用する可変引数のスタイルを返します。 このような定義は、次のように定義されている VarArgsKind 列挙体のメンバーによって定義されます。 


**IDebugHostType2/IDebugHostType Typedef 関連のメソッド**

Typedef であるすべての型は、型が typedef の基になる最終的な型であるかのように動作します。 これは、GetTypeKind などのメソッドは、型が typedef であることを示していないことを意味します。 同様に、GetBaseType は、定義が参照する型を返しません。 代わりに、typedef の基になる最終的な定義で呼び出されたかのように動作を示します。 例を次に示します。 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```

' PMYSTRUCT または PTRMYSTRUCT ' の IDebugHostType は、次の情報を報告します。 

- GetTypeKind メソッドは TypePointer を返します。 基になる最後の型 MYSTRUCT * は、実際にはポインターです。
- ' GetBaseType メソッドは MYSTRUCT の型を返します。 MYSTRUCT * の基になる型は MYSTRUCT です。

ここでの違いは、IDebugHostType2 の typedef 固有のメソッドがどのように動作するかという点だけです。 これらのメソッドは次のとおりです。 

```cpp
STDMETHOD(IsTypedef)(_Out_ bool* isTypedef) PURE;
STDMETHOD(GetTypedefBaseType)(_Out_ IDebugHostType2** baseType) PURE;
STDMETHOD(GetTypedefFinalBaseType)(_Out_ IDebugHostType2** finalBaseType) PURE;
```

この例では、次の操作を行います。 

- IsTypedef メソッドは、PMYSTRUCT と PTRMYSTRUCT の両方に対して true を返します。
- GetTypedefBaseType メソッドは、PTRMYSTRUCT の PMYSTRUCT および PMYSTRUCT の MYSTRUCT * を返します。
- GetTypedefFinalBaseType メソッドは、両方の型に対して MYSTRUCT * を返します。

[IsTypedef](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype2-istypedef)

IsTypedef メソッドは、型が typedef であるかどうかを確認できる唯一のメソッドです。 GetTypeKind メソッドは、基になる型で呼び出されているかのように動作します。 

[GetTypedefBaseType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype2-gettypedefbasetype)

GetTypedefBaseType メソッドは、typedef の直接の定義を返します。 ドキュメントで説明されている例では、次のようになります。 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```
このメソッドは、PTRMYSTRUCT の PMYSTRUCT および PMYSTRUCT の MYSTRUCT * を返します。


[GetTypedefFinalBaseType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype2-gettypedeffinalbasetype)

GetTypedefFinalBaseType メソッドは、typedef が定義している最終的な型を返します。 Typedef が別の typedef の定義である場合、typedef ではなく、その型が返されるまでは、定義チェーンに従います。 ドキュメントで説明されている例では、次のようになります。 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```

このメソッドは、PMYSTRUCT または PTRMYSTRUCT のいずれかで呼び出された場合、MYSTRUCT * を返します。 

**IDebugHostType2/IDebugHostType 型の作成方法**

```cpp
STDMETHOD(CreatePointerTo)(_In_ PointerKind kind, _COM_Outptr_ IDebugHostType** newType) PURE;
STDMETHOD(CreateArrayOf)(_In_ ULONG64 dimensions, _In_reads_(dimensions) ArrayDimension *pDimensions, _COM_Outptr_ IDebugHostType** newType) PURE;
```

**定数シンボル値: IDebugHostConstant**

定数値がシンボル情報に含まれる場所 (特定の値が定数値であるか、または定数値でない場合があります) では、IDebugHostConstant インターフェイスはそのような定数の概念を表します。 通常、これはテンプレート引数のような場所で使用されます。指定された引数は通常、型ですが、代わりに非型テンプレート引数 (例: 定数) である場合があります。 

IDebugHostConstant インターフェイスは、次のように定義されます (IDebugHostSymbol によって実装されたジェネリックメソッドは無視されます)。 

```cpp
DECLARE_INTERFACE_(IDebugHostConstant, IDebugHostSymbol)
{
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostconstant-getvalue)

GetValue メソッドは、バリアントにパックされた定数の値を返します。 IDebugHostSymbol の GetType メソッドは、定数に対して特定の型シンボルを返す場合があることに注意してください。 このような場合、型シンボルによって定義された定数値のパッキングは、ここでは、GetValue メソッドによって返されるパッキングと同じであるという保証はありません。 


**データメンバーアクセス: IDebugHostField**

IDebugHostField クラスは、クラス、構造体、共用体、またはその他の型コンストラクトのデータメンバーであるシンボルを表します。 これは、空きデータ (例: グローバルデータ) を表していません。 インターフェイスは次のように定義されています (IDebugHostSymbol からジェネリックメソッドを無視します)。 

```cpp
DECLARE_INTERFACE_(IDebugHostField, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetOffset)(_Out_ ULONG64* offset) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

[GetLocationKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostfield-getlocationkind)

GetLocationKind メソッドは、LocationKind 列挙に従って、シンボルがある場所の種類を返します。 この列挙型には、次のいずれかの値を指定できます。 

列挙 | 意味
|---------|--------|
LocationMember | フィールドは、クラス、構造体、共用体、またはその他の型コンストラクトの通常のデータメンバーです。 これには、包含する型のコンストラクトのベースアドレスを基準としたオフセットがあります。 このようなベースアドレスは、通常、このポインターによって表されます。 フィールドのオフセットは、GetOffset メソッドを使用して取得できます。 GetLocation および GetValue メソッドは、LocationMember であるフィールドに対して失敗します。
LocationStatic | フィールドは静的で、独自のアドレスを持ちます。 GetLocation メソッドは、静的フィールドの抽象的な場所 (例: アドレス) を返します。 GetOffset メソッドと GetValue メソッドは、LocationStatic であるフィールドに対して失敗します。
LocationConstant | フィールドは定数で、値を持ちます。 GetValue メソッドは、定数の値を返します。 GetOffset メソッドと GetLocation メソッドは、LocationConstant であるフィールドに対して失敗します。
LocationNone | フィールドに場所がありません。 コンパイラによって最適化されているか、宣言されているが定義されていない静的フィールドである可能性があります。 このようなフィールドがどのようになったかにかかわらず、物理的な存在も値もありません。 シンボルのみに含まれています。 すべての取得方法 (GetOffset、GetLocation、および GetValue) は、LocationNone のフィールドに対して失敗します。

[GetOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostfield-getoffset)

オフセットを持つフィールド (場所の種類が LocationMember を示すフィールドなど) の場合、GetOffset メソッドは、含まれている型 (this ポインター) のベースアドレスからフィールド自体のデータへのオフセットを返します。 このようなオフセットは、常に符号なし64ビット値として表されます。 指定されたフィールドに格納されている型のベースアドレスからのオフセットである場所がない場合、GetOffset メソッドは失敗します。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostfield-getlocation)

特定の型インスタンスに関係なくアドレスを持つフィールドの場合 (場所の種類が LocationStatic を示すフィールドなど)、GetLocation メソッドはフィールドの抽象的な場所 (アドレス) を返します。 指定されたフィールドに静的な場所がない場合、GetLocation メソッドは失敗します。 

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostfield-getvalue)

シンボル情報内に定数値が定義されているフィールド (場所の種類が LocationConstant を示すフィールドなど) の場合、GetValue メソッドはフィールドの定数値を返します。 指定されたフィールドに定数値がない場合、GetValue メソッドは失敗します。 


**無料のデータアクセス: IDebugHostData**

別の型のメンバーではないモジュール内のデータは、IDebugHostData インターフェイスによって表されます。 このインターフェイスは、次のように定義されています (IDebugHostSymbol のジェネリックメソッドは無視されます)。 

```cpp
DECLARE_INTERFACE_(IDebugHostData, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

これらのメソッドはすべて、IDebugHostField の対応するメソッドと意味的に等価です。 唯一の違いは、GetLocationKind メソッドがフリーデータの LocationMember を返さないことです。 

[GetLocationKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostdata-getlocationkind)

GetLocationKind メソッドは、LocationKind 列挙に従って、シンボルがある場所の種類を返します。 この列挙体の説明については、IDebugHostField のドキュメントを参照してください。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostdata-getlocation)

アドレスを持つデータの場合、GetLocation メソッドはフィールドの抽象的な場所 (アドレス) を返します。 指定されたデータに静的な場所がない場合、GetLocation メソッドは失敗します。 

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostdata-getvalue)

シンボリック情報内に定数値 (場所の種類が LocationConstant を示すデータなど) が定義されている datawhich 場合、GetValue メソッドはフィールドの定数値を返します。 指定されたデータに定数値がない場合、GetValue メソッドは失敗します。 


**基底クラス: IDebugHostBaseClass**

指定された型の継承階層は、型シンボルの子を通じて表現されます。 特定の型が1つ以上の型から派生 (継承) される場合、その型の型シンボルには1つ以上の SymbolBaseClass 子が存在します。 これらの各 SymbolBaseClass シンボルは、特定の型からの即時継承を表します。 基底クラスの名前は、SymbolBaseClass 記号の名前と基底クラスの型シンボルの名前の両方になります。 SymbolBaseClass シンボルの GetType メソッドを使用して、基底クラス自体の型シンボルを取得できます。 SymbolBaseClass の子シンボルを再帰的に探索することで、完全継承階層を走査できます。 これらの基底クラスシンボルはそれぞれ、次のように定義されている IDebugHostBaseClass インターフェイスによって表されます (IDebugHostSymbol のジェネリックメソッドは無視されます)。 

```cpp
DECLARE_INTERFACE_(IDebugHostBaseClass, IDebugHostSymbol)
{
    STDMETHOD(GetOffset)(_Out_ ULONG64* offset) PURE;
}
```

[GetOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostbaseclass-getoffset)

GetOffset メソッドは、派生クラスのベースアドレスから基底クラスのオフセットを返します。 このようなオフセットは0にすることも、符号なし64ビットの正の値にすることもできます。 


**パブリックシンボル: IDebugHostPublic**

パブリックシンボルは、シンボルファイル内のパブリックテーブル内の項目を表します。 実際には、アドレスがエクスポートされます。 パブリックシンボルに関連付けられている型情報がありません--アドレスのみ。 パブリックシンボルが呼び出し元によって明示的に要求されない限り、デバッグホストは、すべての問い合わせに対してプライベートシンボルを返すことを推奨します。 パブリックシンボルは、次のように定義されている IDebugHostPublic インターフェイスによって表されます (IDebugHostSymbol に汎用のメソッドは無視されます)。 

```cpp
DECLARE_INTERFACE_(IDebugHostPublic, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
}
```

これらのメソッドはすべて、IDebugHostField の対応するメソッドと意味的に等価です。 唯一の違いは、GetLocationKind メソッドは、このような記号の LocationMember または LocationConstant を返さないという点です。 

[GetLocationKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostpublic-getlocationkind)

GetLocationKind メソッドは、LocationKind 列挙に従って、シンボルがある場所の種類を返します。 この列挙体の説明については、IDebugHostField のドキュメントを参照してください。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostpublic-getlocation)

アドレスを持つデータの場合、GetLocation メソッドはフィールドの抽象的な場所 (アドレス) を返します。 指定されたパブリックに静的な場所がない場合、GetLocation メソッドは失敗します。 


**モジュール署名とバージョンの一致: IDebugHostModuleSignature**

モジュール署名は、特定のモジュールが名前付けとバージョン管理に関する一連の条件を満たすかどうかを確認する手段を表します。 モジュール署名は、IDebugHostSymbols の CreateModuleSignature メソッドを使用して作成されます。 モジュール名と、モジュールのバージョン番号のオプションの範囲を一致させることができます。 このような署名が作成されると、クライアントは次のように定義された IDebugHostModuleSignature インターフェイスを受け取ります。 

```cpp
DECLARE_INTERFACE_(IDebugHostModuleSignature, IUnknown)
{
    STDMETHOD(IsMatch)(_In_ IDebugHostModule* pModule, _Out_ bool* isMatch) PURE;
}
```

[IsMatch](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodulesignature-ismatch)

IsMatch メソッドは、特定のモジュール (IDebugHostModule シンボルによって指定されたもの) を署名に対して比較し、モジュール名とバージョンをシグネチャに示されている名前とバージョン範囲と比較します。 指定されたモジュールシンボルが署名と一致するかどうかを示す値が返されます。 

**型のシグネチャと型の一致: IDebugHostTypeSignature**

型シグネチャは、特定の型インスタンスが型の名前、型の汎用引数、およびその型が存在するモジュールに関する一連の条件を満たすかどうかを確認する手段を表します。 型シグネチャは、IDebugHostSymbols の CreateTypeSignature メソッドを使用して作成されます。 このような署名が作成されると、クライアントは次のように定義された IDebugHostTypeSignature インターフェイスを受け取ります。 

```cpp
DECLARE_INTERFACE_(IDebugHostTypeSignature, IUnknown)
{
    STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
    STDMETHOD(IsMatch)(_In_ IDebugHostType* type, _Out_ bool* isMatch, _COM_Outptr_opt_ IDebugHostSymbolEnumerator** wildcardMatches) PURE;
    STDMETHOD(CompareAgainst)(_In_ IDebugHostTypeSignature* typeSignature, _Out_ SignatureComparison* result) PURE;
}
```

[GetHashCode](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttypesignature-gethashcode)

GetHashCode メソッドは、型シグネチャの32ビットハッシュコードを返します。 デバッグホストは、型のインスタンスに対して返されるハッシュコードと、型シグネチャに対して返されるハッシュコードの間で、実装に同期があることを保証します。 グローバル一致を除き、型インスタンスが型シグネチャに対応できる場合は、両方とも同じ32ビットハッシュコードが使用されます。 これにより、型インスタンスと、データモデルマネージャーに登録されている多数の型シグネチャとの間で、最初の迅速な比較と照合が可能になります。 

[IsMatch](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttypesignature-ismatch)

IsMatch メソッドは、特定の型のインスタンスが、型シグネチャで指定された条件と一致するかどうかを示す値を返します。 そのような場合は、このことが示され、列挙子が返されます。これにより、型のシグネチャに含まれるワイルドカードと一致する型インスタンスのすべての特定部分 (シンボル) が示されます。 

[CompareAgainst](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttypesignature-compareagainst)

CompareAgainst メソッドは、型シグネチャを別の型シグネチャと比較し、2つのシグネチャの比較方法を返します。 返される比較結果は、次のように定義されている SignatureComparison 列挙のメンバーです。 

列挙 | 意味
|---------|-----------|
関連 | 比較対象の2つのシグネチャまたは型の間にリレーションシップがありません。
一意 |1つの署名または型は、あいまいを他方と比較します。 2つの型シグネチャの場合は、シグネチャが同じである可能性のある型のインスタンスが存在する可能性があることを意味します。 例として、次に示す2つの型シグネチャはあいまいです。  署名 1: `std::pair<*, int>` シグネチャ 2: `std::pair<int,*>` は、型のインスタンス `std::pair<int, int>` 一致している (両方とも1つの具象と1つのワイルドカードが一致している) ためです。
限定しない | 一方のシグネチャまたは型は、もう一方よりも限定的です。 多くの場合、これは、より限定的なシグネチャには、具体的な型が具象型であるワイルドカードがあることを意味します。 例として、以下の最初のシグネチャは、2番目のシグネチャよりも限定的です。 シグネチャ 1: `std::pair<*, int>` シグネチャ 2: `std::pair<int, int>` には、2番目の型が具象型 (int) であるワイルドカード (`*`) があるため、このようになります。
MoreSpecific | 1つのシグネチャまたは型は、もう一方よりも固有です。 多くの場合、これは、より具体的なシグネチャには、ワイルドカードを持つ特定の型があることを意味します。 例として、以下の最初のシグネチャは、2番目よりも具体的なものです。 Signature 1: `std::pair<int, int>` Signature 2: `std::pair<*, int>` は具象型 (int) を持ち、2番目の型にはワイルドカード (`*`) があるため、このようになります。
内容 | 2つのシグネチャまたは型は同じです。

---

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

このトピックは、からC++アクセス可能なインターフェイス、それらを使用してC++ベースのデバッガー拡張機能を構築する方法、およびC++データモデル拡張機能から他のデータモデル構造 (JavaScript や NatVis など) を使用する方法について説明したシリーズの一部です.

[デバッガーデータモデルC++の概要](data-model-cpp-overview.md)

[デバッガーデータモデルC++のインターフェイス](data-model-cpp-interfaces.md)

[デバッガーデータモデルC++オブジェクト](data-model-cpp-objects.md)

[デバッガーデータモデルC++の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーデータモデルC++の概念](data-model-cpp-concepts.md)

[デバッガーデータモデルC++のスクリプト](data-model-cpp-scripting.md)
