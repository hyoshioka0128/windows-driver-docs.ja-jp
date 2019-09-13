---
title: Debugger Data Model C++ の概念
description: このトピックでは、デバッガー C++データモデルの概念について説明します。
ms.date: 09/12/2019
ms.openlocfilehash: 74f48979e347634855bb851a4be0dada62589868
ms.sourcegitcommit: 3b7c8b3cb59031e0f4e39dac106c1598ad108828
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2019
ms.locfileid: "70930378"
---
# <a name="debugger-data-model-c-concepts"></a>Debugger Data Model C++ の概念

このトピックでは、デバッガー C++データモデルの概念について説明します。

## <a name="span-idconcepts-concepts-in-the-data-model"></a><span id="concepts">データモデルの概念 

データモデルの合成オブジェクトは、実質的に次の2つの処理を行います。 

- キー/値/メタデータの組のディクショナリ。
- データモデルによってサポートされる一連の概念 (インターフェイス)。
概念とは、指定されたセマンティック動作のセットを提供するために (データモデルではなく) クライアントが実装するインターフェイスです。 現在サポートされている概念のセットを次に示します。 

概念インターフェイス | 説明
|-----------------|-------------|
IDataModelConcept | 概念は親モデルです。 このモデルが登録された型のシグネチャを使用してネイティブ型に自動的にアタッチされる場合、そのような型の新しいオブジェクトがインスタンス化されるたびに、InitializeObject メソッドが自動的に呼び出されます。
IStringDisplayableConcept | オブジェクトを文字列に変換して、表示することができます。
IIterableConcept | オブジェクトはコンテナーであり、反復処理できます。
IIndexableConcept | オブジェクトはコンテナーであり、1つまたは複数のディメンションで (ランダムアクセスによってアクセスされる) インデックスを作成できます。
IPreferredRuntimeTypeConcept | オブジェクトは、基になる型システムから派生した型についてより多くの情報を認識し、静的な型からランタイム型への変換を処理することができます。
IDynamicKeyProviderConcept | オブジェクトはキーの動的プロバイダーであり、コアデータモデルからのすべての主要なクエリを引き継ぎます。 このインターフェイスは、通常、JavaScript などの動的言語へのブリッジとして使用されます。
IDynamicConceptProviderConcept | オブジェクトは、概念の動的プロバイダーであり、コアデータモデルからのすべての概念クエリを引き継ぐことを望んでいます。 このインターフェイスは、通常、JavaScript などの動的言語へのブリッジとして使用されます。


**データモデルの概念は次のとおりです。IDataModelConcept**

別のモデルオブジェクトに親モデルとしてアタッチされているモデルオブジェクトは、データモデルの概念を直接サポートする必要があります。 データモデルの概念では、次のように定義されているインターフェイス IDataModelConcept をサポートする必要があります。 

```cpp
DECLARE_INTERFACE_(IDataModelConcept, IUnknown)
{
    STDMETHOD(InitializeObject)(_In_ IModelObject* modelObject, _In_opt_ IDebugHostTypeSignature* matchingTypeSignature, _In_opt_ IDebugHostSymbolEnumerator* wildcardMatches) PURE;
    STDMETHOD(GetName)(_Out_ BSTR* modelName) PURE;
}
```

[InitializeObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelconcept-initializeobject)

データモデルは、標準ビジュアライザーとして登録することも、データモデルマネージャーの RegisterModelForTypeSignature メソッドまたは RegisterExtensionForTypeSignature メソッドを使用して特定のネイティブ型の拡張機能として登録することもできます。 これらの方法のいずれかを使用してモデルを登録すると、データモデルは、登録で渡されたシグネチャと一致する型を持つ任意のネイティブオブジェクトに、親モデルとして自動的にアタッチされます。 この添付ファイルが自動的に作成される時点で、データモデルに対して InitializeObject メソッドが呼び出されます。 これには、インスタンスオブジェクト、添付ファイルの原因となった型シグネチャ、および型のインスタンス (線形の順序) を生成する列挙子が渡されます。これにより、型のシグネチャ内のすべてのワイルドカードと一致します。 データモデルの実装では、このメソッド呼び出しを使用して、必要なキャッシュを初期化することができます。 

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelconcept-getname)

特定のデータモデルが RegisterNamedModel メソッドを使用して既定の名前で登録されている場合、登録されているデータモデルの IDataModelConcept インターフェイスは、このメソッドからその名前を返す必要があります。 モデルが複数の名前で登録されている場合は、完全に一致していることに注意してください (既定値または最適なものをここで返す必要があります)。 モデルは完全に名前が付けられていない場合があります (名前に登録されていない限り)。 このような場合、GetName メソッドは E_NOTIMPL を返す必要があります。 


**文字列の概要を示す概念:IStringDisplayableConcept**

表示目的で文字列変換を提供するオブジェクトは、IStringDisplayableConcept インターフェイスの実装を通じて、文字列表示可能概念を実装できます。 インターフェイスは次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IStringDisplayableConcept, IUnknown)
{
    STDMETHOD(ToDisplayString)(_In_ IModelObject* contextObject, _In_opt_ IKeyStore* metadata, _Out_ BSTR* displayString) PURE;
}
```

[ToDisplayString](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-istringdisplayableconcept-todisplaystring)

ToDisplayString メソッドは、クライアントがオブジェクトを文字列に変換して (コンソールや UI などに) 表示するようにするたびに呼び出されます。このような文字列変換は、追加のプログラム操作の基礎として使用しないでください。 文字列変換自体は、呼び出しに渡されたメタデータの影響を受ける可能性があります。 文字列変換では、PreferredRadix および PreferredFormat キーを使用するすべての試行が行われます。 


**反復可能なの概念は次のとおりです。IIterableConcept と IModelIterator**

他のオブジェクトのコンテナーであり、それらのオブジェクトを反復処理する機能を表すオブジェクトは、IIterableConcept および IModelIterator インターフェイスの実装によって反復可能な概念をサポートできます。 反復可能な概念のサポートと、インデックス可能な概念のサポートの間には非常に重要な関係があります。 含まれているオブジェクトへのランダムアクセスをサポートするオブジェクトは、反復可能な概念に加えて、インデックス可能な概念をサポートできます。 この場合、反復される要素は既定のインデックスも生成する必要があります。これは、インデックス可能な概念に渡すときに、同じオブジェクトを参照します。 この不変性を満たしていないと、デバッグホストで未定義の動作が発生します。 

IIterableConcept は次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IIterableConcept, IUnknown)
{
    STDMETHOD(GetDefaultIndexDimensionality)(_In_ IModelObject* contextObject, _Out_ ULONG64* dimensionality) PURE;
    STDMETHOD(GetIterator)(_In_ IModelObject* contextObject, _Out_ IModelIterator** iterator) PURE;
}
```

IModelIterator の概念は次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IModelIterator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Errorptr_ IModelObject** object, _In_ ULONG64 dimensions, _Out_writes_opt_(dimensions) IModelObject** indexers, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
}
```

IIterableConcept の[GetDefaultIndexDimensionality](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iiterableconcept-getdefaultindexdimensionality)

GetDefaultIndexDimensionality メソッドは、既定のインデックスの次元数を返します。 オブジェクトをインデックス可能にしない場合、このメソッドは0を返し、成功します (S_OK)。 このメソッドから0以外の値を返すオブジェクトは、次の状態を示すプロトコルコントラクトのサポートを宣言しています。 
- オブジェクトは、IIndexableConcept をサポートすることで、インデックス可能な概念をサポートします。
- 反復可能な概念の GetIterator メソッドから返された IModelIterator の GetNext メソッドは、生成された各要素に対して一意の既定のインデックスを返します。 このようなインデックスには、ここで示したディメンションの数が含まれます。
- IModelIterator の GetNext メソッドから返された決まっを、インデックス可能な概念 (IIndexableConcept) の GetAt メソッドに渡すと、GetNext が生成したのと同じオブジェクトが参照されます。 同じ値が返されます。

IIterableConcept の[Getiterator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iiterableconcept-getiterator)

反復可能な概念の GetIterator メソッドは、オブジェクトを反復処理するために使用できる反復子インターフェイスを返します。 返された反復子は、GetIterator メソッドに渡されたコンテキストオブジェクトを記憶する必要があります。 反復子自体のメソッドには渡されません。 


IModelIterator の[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodeliterator-reset)

反復可能な概念から返された反復子の Reset メソッドは、反復子が最初に作成された位置 (最初の要素の前) に反復子の位置を復元します。 反復子が Reset メソッドをサポートすることを強くお勧めしますが、必須ではありません。 反復子は、 C++入力反復子に相当するものであり、前方反復の単一のパスのみを許可します。 このような場合、Reset メソッドは E_NOTIMPL で失敗する可能性があります。 

IModelIterator の[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodeliterator-getnext)

GetNext メソッドは反復子を前方に移動し、次に反復される要素をフェッチします。 オブジェクトが反復可能なに加えてインデックス可能であり、それが0以外の値を返す GetDefaultIndexDimensionality 引数によって示されている場合、このメソッドは、インデクサーから生成された値に戻るために、必要に応じて既定の決まっを返すことができます。 呼び出し元は、0/nullptr を渡すことを選択し、決まっを取得しないことに注意してください。 このメソッドは、呼び出し元が部分的な決まっを要求する場合には無効と見なされます (例: GetDefaultIndexDimensionality によって生成される数値よりも小さい)。 

反復子が正常に移動したにもかかわらず、反復される要素の値の読み取り中にエラーが発生した場合、メソッドはエラーを返し、"object" にエラーオブジェクト*を格納する*ことがあります。 含まれている要素の反復処理の最後に、反復子は GetNext メソッドから E_BOUNDS を返します。 それ以降の呼び出しでは (介在している Reset 呼び出しがない限り)、E_BOUNDS も返されます。 


**インデックス可能の概念は次のとおりです。IIndexableConcept**

一連のコンテンツへのランダムアクセスを提供するオブジェクトは、IIndexableConcept インターフェイスをサポートすることで、インデックス可能な概念をサポートできます。 インデックスを設定できるオブジェクトのほとんどは、反復可能なの概念をサポートすることによって反復可能なされます。 ただし、これは必須ではありません。 サポートされている場合は、反復子とインデクサーの間に重要な関係があります。 反復子は、GetDefaultIndexDimensionality をサポートし、そのメソッドから0以外の値を返し、そこに記載されているコントラクトをサポートする必要があります。 インデクサーの概念インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IIndexableConcept, IUnknown)
{
    STDMETHOD(GetDimensionality)(_In_ IModelObject* contextObject, _Out_ ULONG64* dimensionality) PURE;
    STDMETHOD(GetAt)(_In_ IModelObject* contextObject, _In_ ULONG64 indexerCount, _In_reads_(indexerCount) IModelObject** indexers, _COM_Errorptr_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetAt)(_In_ IModelObject* contextObject, _In_ ULONG64 indexerCount, _In_reads_(indexerCount) IModelObject** indexers, _In_ IModelObject *value) PURE;
}
```

インデクサー (および反復子との内部再生) の使用例を次に示します。 この例では、インデックス可能なコンテナーの内容を反復処理し、そのインデクサーを使用して返された値に戻ります。 この操作は機能的には記述されていませんが、これらのインターフェイスがどのように対話するかを示しています。 次の例では、メモリ割り当てエラーについては扱いません。 これは、new をスローすることを前提としています (これは、コードが存在する環境によっては適切ではないC++可能性があります。データモデルの COM メソッドでは、例外をエスケープすることはできません)。 

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

GetDimensionality メソッドは、オブジェクトのインデックスが作成されるディメンションの数を返します。 オブジェクトが反復可能なとインデックス可能の両方である場合、GetDefaultIndexDimensionality の実装は、インデクサーが持つ次元の数に対する GetDimensionality の実装に同意する必要があります。 

[GetAt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iindexableconcept-getat)

GetAt メソッドは、インデックス付きオブジェクト内から特定の N 次元インデックスにある値を取得します。 N 次元のインデクサー。 N は GetDimensionality から返された値で、サポートされている必要があります。 オブジェクトは、異なる型 (序数と文字列の両方でインデックス可能) で異なるドメインでインデックスを設定できることに注意してください。 インデックスが範囲外 (またはアクセスできない) の場合、メソッドはエラーを返します。ただし、このような場合は、出力オブジェクトがエラーオブジェクトに設定されている可能性があります。 

[SetAt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iindexableconcept-setat)

SetAt メソッドは、インデックス付きオブジェクト内の特定の N 次元インデックスに値を設定しようとします。 N 次元のインデクサー。 N は GetDimensionality から返された値で、サポートされている必要があります。 オブジェクトは、異なる型 (序数と文字列の両方でインデックス可能) で異なるドメインでインデックスを設定できることに注意してください。 一部のインデクサーは読み取り専用です。 このような場合、SetAt メソッドの呼び出しから E_NOTIMPL が返されます。 


**優先されるランタイム型の概念は次のとおりです。IPreferredRuntimeTypeConcept**

シンボル情報に含まれる静的な型から、オブジェクトの実際のランタイム型を特定するために、デバッグホストを照会できます。 この変換は、完全に正確な情報 (例:C++RTTI) またはは、オブジェクト内の仮想関数テーブルの形などの強力なヒューリスティックに基づいている場合があります。 ただし、一部のオブジェクトはデバッグホストのヒューリスティックに適合しないため、静的からランタイム型に変換することはできません (たとえば、RTTI や仮想関数テーブルがない)。 このような場合、オブジェクトのデータモデルは、既定の動作をオーバーライドし、デバッグホストが理解できるオブジェクトの "ランタイム型" についてより多く認識していることを宣言できます。 これを行うには、IPreferredRuntimeTypeConcept インターフェイスの推奨されるランタイム型の概念とサポートを使用します。 

IPreferredRuntimeTypeConcept インターフェイスは、次のように宣言されます。 

```cpp
DECLARE_INTERFACE_(IPreferredRuntimeTypeConcept, IUnknown)
{
    STDMETHOD(CastToPreferredRuntimeType)(_In_ IModelObject* contextObject, _COM_Errorptr_ IModelObject** object) PURE;
}
```

[CastToPreferredRuntimeType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ipreferredruntimetypeconcept-casttopreferredruntimetype)

CastToPreferredRuntimeType メソッドは、クライアントが静的な型のインスタンスからそのインスタンスのランタイム型に変換しようとするたびに呼び出されます。 対象のオブジェクトが、アタッチされている親モデルの1つを通じて、優先するランタイム型の概念をサポートしている場合、このメソッドは変換を実行するために呼び出されます。 このメソッドは、元のオブジェクトを返すことができます (変換がないか、または分析できません)。ランタイム型の新しいインスタンスを返すか、非セマンティックの理由で失敗します (例: メモリ不足)、または E_NOT_SET を返します。 E_NOT_SET エラーコードは、非常に特殊なエラーコードです。これは、実装で既定の動作をオーバーライドしないこと、およびデバッグホストによって実行される任意の分析にデータモデルがフォールバックする必要があることをデータモデルに示すことを意味します (例::RTTI の分析、仮想関数テーブルの構造の検査など) 


**動的プロバイダーの概念は次のとおりです。IDynamicKeyProviderConcept と IDynamicConceptProviderConcept**

データモデル自体は、通常、オブジェクトのキーと概念の管理を処理しますが、その概念が理想的ではない場合もあります。 特に、クライアントがデータモデルと、真に動的なもの (たとえば、次のようなものとの間にブリッジを作成しようとするとします。JavaScript) では、データモデルの実装から、キーと概念の管理を引き継ぐことが重要な場合があります。 コアデータモデルは IModelObject の唯一の実装であり、動的キープロバイダーの概念と動的概念プロバイダーの概念という2つの概念の組み合わせによって行われます。 またはどちらも実装するのは一般的ではありませんが、このような要件はありません。 

両方が実装されている場合は、動的な概念プロバイダーの概念の前に動的キープロバイダーの概念を追加する必要があります。 これらの概念はどちらも特殊です。 "静的管理" から "動的管理" に変更するオブジェクトのスイッチを効果的に反転させます。 これらの概念は、オブジェクトのデータモデルによって管理されているキーや概念がない場合にのみ設定できます。 これらの概念がオブジェクトに追加されると、その操作は後になります。 

IModelObject (動的概念プロバイダー) と、それ以外の機能の間には、機能拡張に関する追加のセマンティックの違いがあります。 これらの概念は、クライアントがデータモデルと、JavaScript などの動的言語システムの間にブリッジを作成できるようにすることを目的としています。 データモデルには、javascript のようなシステムとは基本的に異なる機能拡張の概念があります。これは、JavaScript プロトタイプチェーンなどの線形チェーンではなく、親モデルのツリーがあることを示しています。 このようなシステムとの関係を向上させるために、動的概念プロバイダーである IModelObject には、単一のデータモデルの親があります。 この1つのデータモデルの親は通常の IModelObject で、データモデルにとっては通常のように任意の数の親モデルを持つことができます。 動的概念プロバイダーに対する親の追加または削除の要求は、1つの親に自動的にリダイレクトされます。 部外者の観点から見ると、動的概念プロバイダーには、親モデルの通常のツリースタイルチェーンがあるように見えます。 動的概念プロバイダーの概念の実装者は、中間の単一の親を認識する唯一のオブジェクト (コアデータモデル以外) です。 この1つの親を動的言語システムにリンクして、ブリッジを提供できます (例: JavaScript プロトタイプチェーンに配置されます)。 

動的キープロバイダーの概念は、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDynamicKeyProviderConcept, IUnknown)
{
    STDMETHOD(GetKey)(_In_ IModelObject *contextObject, _In_ PCWSTR key, _COM_Outptr_opt_result_maybenull_ IModelObject** keyValue, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata, _Out_opt_ bool *hasKey) PURE;
    STDMETHOD(SetKey)(_In_ IModelObject *contextObject, _In_ PCWSTR key, _In_ IModelObject *keyValue, _In_ IKeyStore *metadata) PURE;
    STDMETHOD(EnumerateKeys)(_In_ IModelObject *contextObject, _COM_Outptr_ IKeyEnumerator **ppEnumerator) PURE;
}
```

動的概念プロバイダーの概念は、次のように定義されています。 

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

IDynamicKeyProviderConcept の[Getkey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-getkey)

動的キープロバイダーの GetKey メソッドは、主に IModelObject での GetKey メソッドのオーバーライドです。 動的キープロバイダーは、キーの値と、そのキーに関連付けられているメタデータを返すことが想定されています。 キーが存在しない (ただし、他のエラーが発生しない) 場合、プロバイダーは hasKey パラメーターで false を返し、S_OK で成功する必要があります。 この呼び出しに失敗すると、キーをフェッチできなくなり、親モデルチェーンを通じてキーの検索が明示的に停止されます。 HasKey で false を返し、success を返すと、キーの検索が続行されます。 GetKey では、ボックス化されたプロパティアクセサーをキーとして返すことができることに注意してください。 これは、プロパティアクセサーを返す IModelObject の GetKey メソッドと意味的に同じです。 

IDynamicKeyProviderConcept の[Setkey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-setkey)

動的キープロバイダーの SetKey メソッドは事実上、IModelObject での SetKey メソッドのオーバーライドです。 これにより、動的プロバイダーにキーが設定されます。 実質的には、プロバイダーで新しいプロパティが作成されます。 Expando プロパティの作成などの概念をサポートしていないプロバイダーは、ここで E_NOTIMPL を返す必要があることに注意してください。 

IDynamicKeyProviderConcept の[EnumerateKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-enumeratekeys)

動的キープロバイダーの EnumerateKeys メソッドは、実質的に IModelObject の EnumerateKeys メソッドをオーバーライドします。 これにより、動的プロバイダー内のすべてのキーが列挙されます。 返される列挙子には、実装によって無視される必要があるいくつかの制限があります。 

- これは、EnumerateKeyValues または EnumerateKeyReferences ではなく、EnumerateKeys の呼び出しとして動作する必要があります。 基になるプロパティアクセサーを解決しないキー値を返す必要があります (そのような概念がプロバイダーに存在する場合)。
- 単一の動的キープロバイダーの観点からは、物理的に異なるキーを持つ同じ名前の複数のキーを列挙することは無効です。 これは、親モデルチェーンを介してアタッチされたさまざまなプロバイダーで発生する可能性がありますが、1つのプロバイダーの観点からは発生しません。

IDynamicConceptProviderConcept の[Getconcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-getconcept)

動的概念プロバイダーでの GetConcept メソッドは、事実上、IModelObject での GetConcept メソッドのオーバーライドです。 動的概念プロバイダーは、クエリされた概念が存在する場合はその概念のインターフェイスと、その概念に関連付けられているメタデータを返す必要があります。 概念がプロバイダーに存在しない場合は、hasConcept 引数で返される false 値と正常な戻り値を使用して指定する必要があります。 この方法のエラーは、概念を取得できなかったため、概念の検索を明示的に停止します。 HasConcept の場合は false を返し、コードが成功した場合は、親モデルツリーを通じて概念の検索を続行します。 

IDynamicConceptProviderConcept の[Setconcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-setconcept)

動的概念プロバイダーの SetConcept メソッドは、実質的に IModelObject の SetConcept メソッドをオーバーライドします。 動的プロバイダーによって概念が割り当てられます。 これにより、オブジェクトを反復可能な、インデックス可能、文字列に変換できるようになります。ここでは、概念の作成が許可されていないプロバイダーが E_NOPTIMPL を返す必要があることに注意してください。 

IDynamicConceptProviderConcept の[NotifyParent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifyparent)

動的概念プロバイダーの NotifyParent 呼び出しは、コアデータモデルによって、データモデルの "複数の親モデル" パラダイムをより動的な言語にブリッジングできるように作成された単一の親モデルの動的プロバイダーを通知するために使用されます。 この1つの親モデルを操作すると、動的プロバイダーに対するさらなる通知が発生します。 このコールバックは、動的概念プロバイダーの概念の割り当て時に直ちに行われることに注意してください。 

IDynamicConceptProviderConcept の[NotifyParentChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifyparentchange)

動的概念プロバイダーの NotifyParent メソッドは、オブジェクトの単一の親モデルの静的操作が行われたときに、コアデータモデルによって作成されるコールバックです。 追加された特定の親モデルについては、親モデルが追加されたときに初めてこのメソッドが呼び出され、親モデルが削除された場合は2回目になります。 

IDynamicConceptProviderConcept の[Notifydestruct](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifydestruct)

動的概念プロバイダーの NotifyDestruct メソッドは、動的概念プロバイダーであるオブジェクトの破棄の開始時に、コアデータモデルによって作成されるコールバックです。 これにより、クライアントに必要な追加のクリーンアップ機会が提供されます。 

--

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

このトピックは、からC++アクセス可能なインターフェイス、それらを使用してC++ベースのデバッガー拡張機能を構築する方法、および他のデータモデル構造を使用する方法について説明したシリーズの一部です (例:JavaScript または NatVis) をC++データモデル拡張機能から。

[デバッガーデータモデルC++の概要](data-model-cpp-overview.md)

[デバッガーデータモデルC++のインターフェイス](data-model-cpp-interfaces.md)

[デバッガーデータモデルC++オブジェクト](data-model-cpp-objects.md)

[デバッガーデータモデルC++の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーデータモデルC++の概念](data-model-cpp-concepts.md)

[デバッガーデータモデルC++のスクリプト](data-model-cpp-scripting.md)


 

 






