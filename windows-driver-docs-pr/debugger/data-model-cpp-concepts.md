---
title: Debugger Data Model C++ の概念
description: このトピックでは、デバッガーの C++ のデータ モデルの概念について説明します。
ms.date: 10/04/2018
ms.openlocfilehash: f29334ea8b034f05000b97d2a232ec5c0a250503
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376119"
---
# <a name="debugger-data-model-c-concepts"></a>Debugger Data Model C++ の概念

このトピックでは、デバッガーの C++ のデータ モデルの概念について説明します。

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

[データ モデルの概念](#concepts) 

---


## <a name="span-idconcepts-concepts-in-the-data-model"></a><span id="concepts"> データ モデルの概念 

データ モデルの合成オブジェクトとは、実質的に 2 つのことです。 

- メタデータ/キー/値のタプルのディクショナリ。
- データ モデルでサポートされている概念 (インターフェイス) のセット。
概念は、指定されたセマンティックの動作のセットを提供する (データ モデル) ではなく、クライアントを実装するインターフェイスです。 現在サポートされている一連の概念を次に示します。 

インターフェイスの概念 | 説明
|-----------------|-------------|
IDataModelConcept | 概念は、親モデルです。 このモデルは自動的に登録されているタイプの署名を使用してネイティブ型にアタッチされている、このような種類の新しいオブジェクトがインスタンス化されるたびに、InitializeObject メソッドが呼び出さ自動的にします。
IStringDisplayableConcept | オブジェクトは、表示目的での文字列に変換できます。
IIterableConcept | オブジェクトはコンテナーであり、反復処理されることができます。
IIndexableConcept | オブジェクトはコンテナーであり、インデックスを作成できます (ランダム アクセスを使用してアクセスされる) 1 つまたは複数のディメンションでします。
IPreferredRuntimeTypeConcept | オブジェクトでは、基になる型システムが提供することのできると、ランタイム型を静的から独自の変換を処理するよりも、それから派生した種類の詳細については理解します。
IDynamicKeyProviderConcept | オブジェクトは、動的なキーのプロバイダーであり、コア データ モデルからのすべてのキー クエリを実行したいです。 このインターフェイスは通常、JavaScript などの動的言語へのブリッジとして使用します。
IDynamicConceptProviderConcept | オブジェクトは概念の動的なプロバイダーであり、コア データ モデルからすべての概念のクエリを実行したいです。 このインターフェイスは通常、JavaScript などの動的言語へのブリッジとして使用します。


**データ モデルの概念:IDataModelConcept**

親モデルとして別のモデル オブジェクトに関連付けられている任意のモデル オブジェクトは、データ モデルの概念を直接サポートする必要があります。 IDataModelConcept が次のように定義されている、データ モデルの概念には、インターフェイスのサポートが必要です。 

```cpp
DECLARE_INTERFACE_(IDataModelConcept, IUnknown)
{
    STDMETHOD(InitializeObject)(_In_ IModelObject* modelObject, _In_opt_ IDebugHostTypeSignature* matchingTypeSignature, _In_opt_ IDebugHostSymbolEnumerator* wildcardMatches) PURE;
    STDMETHOD(GetName)(_Out_ BSTR* modelName) PURE;
}
```

[InitializeObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelconcept-initializeobject)

データ モデルは、データ モデルのマネージャーの RegisterModelForTypeSignature または RegisterExtensionForTypeSignature メソッドによって正規ビジュアライザーとして、または特定のネイティブ型の拡張機能として登録できます。 これらのメソッドのいずれかを使用して、モデルが登録されると、自動的にデータ モデルが接続されている、親モデルとして型を持つ登録に渡されるシグネチャに一致する任意のネイティブ オブジェクトにします。 その添付ファイルが自動的に行われた時点で、データ モデルに InitializeObject メソッドが呼び出されます。 これには、インスタンス オブジェクト、添付ファイルの原因となった型シグネチャや型シグネチャに、ワイルドカードに一致する (線形な順序) で型のインスタンスを生成する列挙子が渡されます。 データ モデルの実装では、必要がありますすべてのキャッシュを初期化するために、このメソッドの呼び出しを使用できます。 

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelconcept-getname)

RegisterNamedModel メソッドを使用して既定の名前で指定されたデータ モデルが登録されている、登録済みのデータ モデルの IDataModelConcept インターフェイスは、このメソッドからその名前を返す必要があります。 複数の名前 (既定または最高ここで 1 つ返される必要があります) に登録するモデルの申し分なく正当なことに注意してください。 (限り名前で登録されていない) にモデルを完全に名前付きできない可能性があります。 このような状況では、GetName メソッドが E_NOTIMPL を返す必要があります。 


**文字列の表示可能な概念:IStringDisplayableConcept**

オブジェクトの表示のために、文字列変換を提供するには、IStringDisplayableConcept インターフェイスの実装で文字列の表示可能な概念を実装できます。 インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IStringDisplayableConcept, IUnknown)
{
    STDMETHOD(ToDisplayString)(_In_ IModelObject* contextObject, _In_opt_ IKeyStore* metadata, _Out_ BSTR* displayString) PURE;
}
```

[ToDisplayString](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-istringdisplayableconcept-todisplaystring)

クライアントがオブジェクトを表示する文字列に変換する必要があるたびに、ToDisplayString メソッドが呼び出されます (などの UI では、コンソールに.)。このような文字列変換を追加のプログラムによる操作の基盤として使用されませんする必要があります。 文字列変換自体は、呼び出しに渡されるメタデータで深く影響を受ける可能性があります。 文字列変換では、PreferredRadix と PreferredFormat キーを優先するすべての試行をする必要があります。 


**反復可能な概念:IIterableConcept と IModelIterator**

その他のオブジェクトのコンテナーであり、含まれているオブジェクトを反復処理する機能を表現することを希望するオブジェクトは、IIterableConcept および IModelIterator インターフェイスの実装で反復可能な概念をサポートできます。 反復可能な概念のサポートとインデックスの概念のサポートの非常に重要な関係があります。 含まれているオブジェクトへのランダム アクセスをサポートするオブジェクトには、反復可能な概念だけでなく、インデックス可能な概念をサポートできます。 この場合は、反復要素には、既定値が生成する必要がありますもインデックス、インデックスの概念に渡されるときに、同じオブジェクトを参照してください。 デバッグ ホストで未定義の動作をこの不変性を満たすためにエラーが発生します。 

IIterableConcept の定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IIterableConcept, IUnknown)
{
    STDMETHOD(GetDefaultIndexDimensionality)(_In_ IModelObject* contextObject, _Out_ ULONG64* dimensionality) PURE;
    STDMETHOD(GetIterator)(_In_ IModelObject* contextObject, _Out_ IModelIterator** iterator) PURE;
}
```

IModelIterator 概念の定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IModelIterator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Errorptr_ IModelObject** object, _In_ ULONG64 dimensions, _Out_writes_opt_(dimensions) IModelObject** indexers, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
}
```

IIterableConcept の[GetDefaultIndexDimensionality](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iiterableconcept-getdefaultindexdimensionality)

GetDefaultIndexDimensionality メソッドは、既定のインデックスにディメンションの数を返します。 オブジェクトがインデックス可能でない場合、このメソッドは 0 が返され、(S_OK) が成功する必要があります。 このメソッドから 0 以外の値を返す任意のオブジェクトを示すプロトコル コントラクトのサポートを宣言しています。 
- オブジェクトは、IIndexableConcept のサポートを使用してインデックスの概念をサポートしています
- 反復可能な概念の GetIterator メソッドから返される IModelIterator の GetNext メソッドでは、生成された各要素の一意の既定のインデックスを返します。 このようなインデックスは、ここに示すように、ディメンションの数があります。
- インデックスの概念には、GetAt メソッドに、IModelIterator の GetNext メソッドから返されるインデックスを渡す (IIndexableConcept) は GetNext を生成したのと同じオブジェクトを参照します。 同じ値が返されます。

IIterableConcept の[GetIterator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iiterableconcept-getiterator)

反復可能な概念に GetIterator メソッドは、オブジェクトを反復処理するために使用できる反復子インターフェイスを返します。 返された反復子は、GetIterator メソッドに渡されたコンテキスト オブジェクトを忘れないでください。 メソッド自体、反復子では渡されません。 


IModelIterator の[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodeliterator-reset)

反復可能な概念から返された反復子の Reset メソッドは、(最初の要素) の前に、反復子が最初に作成したときに、反復子の位置に復元されます。 反復子の強く勧め Reset メソッドをサポートして、必須ではありません。 反復子では、C++ の入力反復子に相当するでき、順方向の反復の 1 つのパスのみを許可することができます。 このような場合、E_NOTIMPL と Reset メソッドがあります。 

IModelIterator の[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodeliterator-getnext)

GetNext メソッドは、前方反復子に移動し、次の反復処理される要素をフェッチします。 オブジェクト indexable 反復可能なだけでなく、これは、0 以外の値を返す GetDefaultIndexDimensionality 引数によって示されます、このメソッドは必要に応じてインデクサーから生成された値に戻るには既定のインデックスを返す可能性があります。 0/nullptr を渡すし、インデックスを取得する呼び出し元ができますに注意してください。 部分のインデックスを要求する呼び出し元の無効と見なされます (例:: GetDefaultIndexDimensionality によって生成された数よりも小さい)。 

メソッドがエラーを返す可能性があります、反復子が正常に移動進む場合は、繰り返し行う一連の要素の値を読み取り中にエラーが発生しました*AND*エラー オブジェクトには、「オブジェクト」を入力します。 含まれる要素の反復処理の最後に、反復子は、GetNext メソッドから、E_BOUNDS を返します。 すべての後続の呼び出し (ない場合のリセットの中間の呼び出しがあった) でも E_BOUNDS が返されます。 


**インデックスの概念:IIndexableConcept**

オブジェクトの内容のセットへのランダム アクセスを提供するには、IIndexableConcept インターフェイスのサポートを使用してインデックスの概念をサポートできます。 インデックス可能であるほとんどのオブジェクトは、反復可能な概念のサポートを通じても反復可能になります。 これは、ただし、必要ありません。 、サポートされている場合は、反復子とインデクサーの重要な関係があります。 反復子では、GetDefaultIndexDimensionality のサポートからこのメソッドは、0 以外の値を返す、および説明があるコントラクトをサポートする必要があります。 インデクサーの概念のインターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IIndexableConcept, IUnknown)
{
    STDMETHOD(GetDimensionality)(_In_ IModelObject* contextObject, _Out_ ULONG64* dimensionality) PURE;
    STDMETHOD(GetAt)(_In_ IModelObject* contextObject, _In_ ULONG64 indexerCount, _In_reads_(indexerCount) IModelObject** indexers, _COM_Errorptr_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetAt)(_In_ IModelObject* contextObject, _In_ ULONG64 indexerCount, _In_reads_(indexerCount) IModelObject** indexers, _In_ IModelObject *value) PURE;
}
```

インデクサー (および反復子とその相互作用) を使用する例は、以下に示します。 この例では、インデックス可能なコンテナーの内容を反復処理し、だけ返された値に戻るには、インデクサーを使用します。 その操作は、書き込まれると機能的には役に立ちませんが、これらのインターフェイスの対話方法を示します。 次の例はメモリ割り当ての失敗を扱うしないことに注意してください。 スローを新しい (可能性のあるコードが存在するです--データ モデルの COM メソッドが C++ 例外のエスケープを持つことはできません、環境に応じて不適切な想定) を仮定します。 

```cpp
ComPtr<IModelObject> spObject;

//
// Assume we have gotten some object in spObject that is iterable (e.g.: an object which represents a std::vector<SOMESTRUCT>)
//
ComPtr<IIterableConcept> spIterable;
ComPtr<IIndexableConcept> spIndexer;
if (SUCCEEDED(spObject->GetConcept(__uuidof(IIterableConcept), &spIterable, nullptr)) &&
    SUCCEEDED(spObject->GetConcept(__uuidof(IIndexableConcept), &spIndexable, nullptr)))
{
    ComPtr<IModelIterator> spIterator;

    //
    // Determine how many dimensions the default indexer is and allocate the requisite buffer.
    //
    ULONG64 dimensions;
    if (SUCCEEDED(spIterable->GetDefaultIndexDimensionality(spObject.Get(), &dimensions)) && dimensions > 0 &&
        SUCCEEDED(spIterable->GetIterator(spObject.Get(), &spIterator)))
    {
        std::unique_ptr<ComPtr<IModelObject>[]> spIndexers(new ComPtr<IModelObject>[dimensions]);

        //
        // We have an iterator.  Error codes have semantic meaning here.  E_BOUNDS indicates the end of iteration.  E_ABORT indicates that
        // the debugger host or application is trying to abort whatever operation is occurring.  Anything else indicates
        // some other error (e.g.: memory read failure) where the iterator MIGHT still produce values.
        //
        for(;;)
        {
            ComPtr<IModelObject> spContainedStruct;
            ComPtr<IKeyStore> spContainedMetadata;

            //
            // When we fetch the value from the iterator, it will pass back the default indicies.
            //
            HRESULT hr = spIterable->GetNext(&spContainedStruct, dimensions, reinterpret_cast<IModelObject **>(spIndexers.get()), &spContainedMetadata);
            if (hr == E_BOUNDS || hr == E_ABORT)
            {
                break;
            }

            if (FAILED(hr))
            {
                //
                // Decide how to deal with failure to fetch an element.  Note that spContainedStruct *MAY* contain an error object
                // which has detailed information about why the failure occurred (e.g.: failure to read memory at address X).
                //
            }

            //
            // Use the indexer to get back to the same value.  We already have them, so there isn't much functional point to this.  It simply
            // highlights the interplay between iterator and indexer.
            //
            ComPtr<IModelObject> spIndexedStruct;
            ComPtr<IKeyStore> spIndexedMetadata;

            if (SUCCEEDED(spIndexer->GetAt(spObject.Get(), dimensions, reinterpret_cast<IModelObject **>(spIndexers.get()), &spIndexedStruct, &spIndexedMetadata)))
            {
                //
                // spContainedStruct and spIndexedStruct refer to the same object.  They may not have interface equality.
                // spContainedMetadata and spIndexedMetadata refer to the same metadata store with the same contents.  They may not have interface equality.
                //
            }
        }
    }
}
```


[GetDimensionality](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iindexableconcept-getdimensionality)

GetDimensionality メソッドは、オブジェクトのインデックスが設定されたディメンションの数を返します。 オブジェクトが反復可能なとインデックスの両方の場合は、GetDefaultIndexDimensionality の実装が、インデクサーの次元数に関して GetDimensionality の実装に同意する必要がありますに注意してくださいがあります。 

[GetAt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iindexableconcept-getat)

GetAt メソッドでは、インデックス付きオブジェクト内から特定の N 次元インデックス値を取得します。 N は GetDimensionality から返される値を N 次元のインデクサーをサポートする必要があります。 オブジェクトをさまざまな種類が異なるドメインにあるインデックス可能する可能性がありますに注意してください (例:: 序数と文字列の両方を使用してインデックスを付ける)。 メソッドが; エラーを返す場合、インデックスが範囲外です (またはアクセスできませんでした)ただし、このような場合は、出力オブジェクトは、エラー オブジェクトには設定もすることがあります。 

[SetAt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iindexableconcept-setat)

SetAt メソッドは、インデックス付きオブジェクト内から特定の N 次元インデックスに値を設定しようとします。 N は GetDimensionality から返される値を N 次元のインデクサーをサポートする必要があります。 オブジェクトをさまざまな種類が異なるドメインにあるインデックス可能する可能性がありますに注意してください (例:: 序数と文字列の両方を使用してインデックスを付ける)。 一部のインデクサーとは、読み取り専用です。 このような場合、SetAt メソッドへの呼び出しから E_NOTIMPL が返されます。 


**優先のランタイム型の概念:IPreferredRuntimeTypeConcept**

デバッグ ホスト シンボリック情報については、静的な型のオブジェクトの実際の実行時の型を判断するためにクエリを実行できます。 この変換は、完全に正確な情報に基づく可能性があります (例。C++ RTTI) またはオブジェクト内のすべての仮想関数テーブルの図形などの強力なヒューリスティックに基づく可能性があります。 一部のオブジェクトが、変換できませんから静的なランタイム型にデバッグ ホストのヒューリスティックに収まらないため、(例: あるありません RTTI または仮想関数テーブル)。 このような場合、オブジェクトのデータ モデルは、既定の動作をオーバーライドし、宣言を把握している複数のオブジェクトの「ランタイム型」についてデバッグ ホストが理解できるよりも選択できます。 これは、任意のランタイム型の概念と IPreferredRuntimeTypeConcept インターフェイスのサポートを通じて実行されます。 

IPreferredRuntimeTypeConcept インターフェイスは、次のように宣言されます。 

```cpp
DECLARE_INTERFACE_(IPreferredRuntimeTypeConcept, IUnknown)
{
    STDMETHOD(CastToPreferredRuntimeType)(_In_ IModelObject* contextObject, _COM_Errorptr_ IModelObject** object) PURE;
}
```

[CastToPreferredRuntimeType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ipreferredruntimetypeconcept-casttopreferredruntimetype)

CastToPreferredRuntimeType メソッドは、クライアントが、静的な型のインスタンスからそのインスタンスのランタイム型に変換しようとする必要があるたびに呼び出されます。 対象のオブジェクトは、(その親が接続されているモデルのいずれか) で推奨ランタイム型の概念をサポートする場合、このメソッドは変換を実行するを呼び出せません。 このメソッドは、元のオブジェクトを返す可能性がありますか (変換がないか分析されません)、ランタイム型の新しいインスタンスを返すと、非セマンティック上の理由から失敗 (例:: メモリ不足)、または E_NOT_SET を取得します。 E_NOT_SET のエラー コードは、データ モデルの実装が既定の動作をオーバーライドしないこと、およびデータ モデルがどのような分析が実行するデバッグ ホスト (例: フォールバックにする必要がありますに示す非常に特殊なエラー コード:RTTI 分析、仮想関数テーブルなどの図形の調査.)。 


**動的なプロバイダーの概念:IDynamicKeyProviderConcept と IDynamicConceptProviderConcept**

データ モデル自体通常オブジェクトのハンドルのキーと概念の管理も回その概念が遅くなります。 クライアントがデータ モデルと別のものの間のブリッジを作成するには、これは完全に動的に希望と具体的には、(例。JavaScript の場合)、データ モデルの実装からキーと概念の管理を引き継ぐに役に立つできます。 コア データ モデルは、1 つと IModelObject の実装のみが、これは、代わりに 2 つの概念の組み合わせを使用して: 動的なキー プロバイダーの概念と動的な概念のプロバイダーの概念です。 実装の両方またはどちらも通常はできますが、このような要件はありません。 

両方が実装されている場合は、動的な概念のプロバイダーの概念の前に動的なキー プロバイダーの概念を追加する必要があります。 これらの概念の両方は特別です。 効果的にオブジェクトを「静的にマネージ」から「動的に管理対象」に変更することで、スイッチを反転します。 これらの概念は、オブジェクトのデータ モデルによって管理されているキー/概念がない場合にのみ設定できます。 オブジェクトには、これらの概念が追加される、このアクションは取り消し可能なです。 

これには、IModelObject 動的概念プロバイダーであるとは 1 つの機能拡張に関する追加セマンティック違いがあります。 これらの概念はクライアントがデータ モデルと JavaScript などの動的言語のシステムの間のブリッジを作成できるようにするためのものです。 データ モデルでは、JavaScript のプロトタイプ チェーンのようなリニア チェーンではなく、親モデルのツリーは、JavaScript などのシステムとやや根本的には異なる機能拡張の概念があります。 このようなシステムをより良い関係を許可するのには、動的概念プロバイダーである、IModelObject は、1 つのデータ モデルの親を持ちます。 その 1 つのデータ モデルの親では、親モデルのデータ モデルの一般的な同様の任意の数を持つことができる標準 IModelObject です。 動的な概念プロバイダーを追加または削除の親への要求は、1 つの親を自動的にリダイレクトされます。 部外者の観点から動的概念プロバイダーがあるモデルの親の通常のツリー スタイルのチェーンのように見えます。 動的な概念のプロバイダーの概念の実装者は、中間の 1 つの親に対応した (コア データ モデル) の外部でのみオブジェクトです。 その 1 つの親は、ブリッジを提供する動的言語のシステムにリンクすることができます (例: JavaScript のプロトタイプ チェーンに配置されます)。 

動的なキー プロバイダーの概念の定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDynamicKeyProviderConcept, IUnknown)
{
    STDMETHOD(GetKey)(_In_ IModelObject *contextObject, _In_ PCWSTR key, _COM_Outptr_opt_result_maybenull_ IModelObject** keyValue, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata, _Out_opt_ bool *hasKey) PURE;
    STDMETHOD(SetKey)(_In_ IModelObject *contextObject, _In_ PCWSTR key, _In_ IModelObject *keyValue, _In_ IKeyStore *metadata) PURE;
    STDMETHOD(EnumerateKeys)(_In_ IModelObject *contextObject, _COM_Outptr_ IKeyEnumerator **ppEnumerator) PURE;
}
```

動的な概念のプロバイダーの概念の定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IDynamicConceptProviderConcept, IUnknown)
{
    STDMETHOD(GetConcept)(_In_ IModelObject *contextObject, _In_ REFIID conceptId, _COM_Outptr_result_maybenull_ IUnknown **conceptInterface, _COM_Outptr_opt_result_maybenull_ IKeyStore **conceptMetadata, _Out_ bool *hasConcept) PURE;
    STDMETHOD(SetConcept)(_In_ IModelObject *contextObject, _In_ REFIID conceptId, _In_ IUnknown *conceptInterface, _In_opt_ IKeyStore *conceptMetadata) PURE;
    STDMETHOD(NotifyParent)(_In_ IModelObject *parentModel) PURE;
    STDMETHOD(NotifyParentChange)(_In_ IModelObject *parentModel) PURE;
    STDMETHOD(NotifyDestruct)() PURE;
}
```

IDynamicKeyProviderConcept の[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-getkey)

動的なキー プロバイダーの GetKey メソッドは、大きく IModelObject GetKey メソッドのオーバーライドです。 動的なキー プロバイダーは、キーとそのキーに関連付けられたメタデータの値を返すと想定されます。 キーが存在しない (ただし、他のエラーが発生しない) ことプロバイダーは hasKey パラメーターに false を返すし、s_ok 成功する必要があります。 この呼び出しの失敗は、キーの取得に失敗したと見なされ、モデルの親チェーンを使用して、キーの検索は、明示的に停止します。 HasKey と成功状態の場合は false を返すと、キーの検索を継続します。 完全に正しく GetKey をキーとしてボックス化されたプロパティのアクセサーを返すことに注意してください。 これは、プロパティ アクセサーを返す IModelObject GetKey メソッドに意味的に同一になります。 

IDynamicKeyProviderConcept の[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-setkey)

動的なキー プロバイダーの SetKey メソッドは、効果的に IModelObject SetKey メソッドのオーバーライドです。 これには、動的なプロバイダーのキーを設定します。 プロバイダーの新しいプロパティの作成では効果的にします。 Expando プロパティの作成などの任意の概念をサポートしていないプロバイダーが E_NOTIMPL をここで返す必要があることに注意してください。 

IDynamicKeyProviderConcept の[EnumerateKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-enumeratekeys)

動的なキー プロバイダーの EnumerateKeys メソッドは、効果的に IModelObject EnumerateKeys メソッドのオーバーライドです。 これには、動的なプロバイダーのすべてのキーを列挙します。 返された列挙子が実装によって受け入れられるいくつかの制限事項があります。 

- EnumerateKeyValues や EnumerateKeyReferences はなく EnumerateKeys の呼び出しとその動作する必要があります。 キーの値 (このような概念は、プロバイダーに存在する) 場合は、基になるプロパティ アクセサーに解決されていません返す必要があります。
- 1 つの動的なキー プロバイダーの観点から物理的に異なるキーである同じ名前の複数のキーを列挙することはできません。 これは、親モデル チェーンを介して接続されている別のプロバイダーで発生しますに 1 つのプロバイダーの観点から発生することはできません。

IDynamicConceptProviderConcept's [GetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-getconcept)

動的概念プロバイダー GetConcept メソッドは、効果的に IModelObject GetConcept メソッドのオーバーライドです。 動的概念プロバイダーとその概念に関連付けられたメタデータが存在する場合、クエリの概念のインターフェイスを返す必要があります。 プロバイダーの概念が存在しない場合、hasConcept 引数を正常終了したときに返される値は false を使用してを示す必要があります。 このメソッドのエラーは、概念のフェッチに失敗したし、概念については、検索は、明示的に停止します。 HasConcept とコードの正常な場合は false を返すと、親モデル ツリーを概念の検索を継続します。 

IDynamicConceptProviderConcept の[SetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-setconcept)

動的概念プロバイダー SetConcept メソッドは、効果的に IModelObject SetConcept メソッドのオーバーライドです。 動的なプロバイダーは、概念を割り当てられます。 オブジェクトの反復可能なインデックス可能な文字列変換などがあることがあります.ここで E_NOPTIMPL を返す必要がありますの概念の作成を許可されていないプロバイダーにことに注意してください。 

IDynamicConceptProviderConcept の[NotifyParent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifyparent)

動的概念プロバイダー NotifyParent 呼び出しは、コア データ モデルで、動的に通知するために使用されてはプロバイダーの 1 つの親モデルとデータ モデルをより動的な言語の「複数の親モデル」パラダイムをブリッジするために作成されます。 その 1 つの親モデルの操作、さらに通知動的プロバイダーになります。 このコールバックが動的概念プロバイダーの概念の割り当て時にすぐに作成されたことに注意してください。 

IDynamicConceptProviderConcept の[NotifyParentChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifyparentchange)

NotifyParent メソッドは、動的な概念のプロバイダーは、静的オブジェクトの 1 つの親モデルの操作が行われたときに、コア データ モデルによって行われたコールバック。 追加された任意の指定した親モデルこのメソッドが呼び出されるときにその親モデルが追加され、親モデルの削除をもう一度場合は、最初に。 

IDynamicConceptProviderConcept の[NotifyDestruct](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifydestruct)

NotifyDestruct メソッドは、動的な概念のプロバイダーは、動的概念プロバイダーであるオブジェクトの破棄の開始時のコア データ モデルによって行われたコールバック。 クライアントで必要とする機会をクリーンアップする追加提供します。 


---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[デバッガー データ モデルの C++ の概要](data-model-cpp-overview.md)

[デバッガーのデータ モデルの C++ インターフェイス](data-model-cpp-interfaces.md)

[デバッガーのデータ モデルの C++ オブジェクト](data-model-cpp-objects.md)

[デバッガーのデータ モデルの C++ の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーのデータ モデルの C の概念](data-model-cpp-concepts.md)

[デバッガー データ モデルの C++ のスクリプト](data-model-cpp-scripting.md)


 

 






