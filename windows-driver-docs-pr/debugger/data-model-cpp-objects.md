---
title: Debugger Data Model C++ のオブジェクト
description: このトピックでは、デバッガーデータモデルC++オブジェクトの使用方法と、デバッガーの機能を拡張する方法について説明します。
ms.date: 01/13/2020
ms.openlocfilehash: 0ccc842300ab4f28792f32df7b128a76f8fba6dd
ms.sourcegitcommit: 1addd14b2063aba321f5428a23393f22f59c02b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2020
ms.locfileid: "76035726"
---
# <a name="debugger-data-model-c-objects"></a>Debugger Data Model C++ のオブジェクト

このトピックでは、デバッガーデータモデルC++オブジェクトの使用方法と、デバッガーの機能を拡張する方法について説明します。

## <a name="span-idcore--the-core-debugger-object-model"></a>コアデバッガーオブジェクトモデルの <span id="core">

データモデルに関する最も基本的な機能の1つは、オブジェクトの定義とオブジェクトとの相互作用を標準化することです。 *Imodelobject*インターフェイスは、オブジェクトの概念 (オブジェクトが整数、浮動小数点値、文字列、デバッガーのターゲットアドレス空間内の一部の複合型、またはプロセスやモジュールの概念などのデバッガーの概念) をカプセル化します。

*Imodelobject*で保持 (またはボックス化) できるいくつかの異なる点があります。

- **組み込み値**- *Imodelobject*は、複数の基本型 (8、16、32、64ビット符号付き整数、符号なし整数、ブール値、文字列、エラー、または空の概念) のコンテナーにすることができます。

- **ネイティブオブジェクト**- *Imodelobject*は、デバッガーが対象とするすべてのアドレス空間内で複合型 (デバッガーの型システムによって定義されている) を表すことができます。 

- **合成オブジェクト**- *Imodelobject*は動的オブジェクトにすることができます。これは、キー/値/メタデータの組のコレクション、およびキーと値のペアで単に表されない動作を定義する一連の**概念**です。

- **プロパティ**- *Imodelobject*は、プロパティを表すことができます。値を取得したり、メソッド呼び出しで変更したりできます。 *Imodelobject*内のプロパティは、事実上、 *imodelobject*にボックス化された*IModelPropertyAccessor*インターフェイスです。

- **メソッド**- *Imodelobject*は、メソッドを表すことができます。一連の引数を指定して呼び出すことができ、戻り値を取得できます。 *Imodelobject*内のメソッドは実質的に*imodelmethod*インターフェイスであり、 *imodelobject*にボックス化されます。

### <a name="extensibility-within-the-object-model"></a>オブジェクトモデル内の機能拡張

*Imodelobject*は、分離されたオブジェクトではありません。 上に示したオブジェクトのいずれかの型を表すことに加えて、各オブジェクトには親データモデルのチェーンの概念があります。 このチェーンは、 [JavaScript プロトタイプチェーン](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)とほぼ同じように動作します。
JavaScript などのプロトタイプの線形チェーンではなく、各データモデルオブジェクトは、**親モデル**の線形チェーンを定義します。 これらの各親モデルには、独自の親セットの別の線形チェーンがあります。 基本的に、各オブジェクトは、このツリー内のすべてのオブジェクトの機能 (プロパティなど) を集計したものです。 特定のプロパティに対してクエリを実行するときに、クエリを実行するオブジェクトがそのプロパティをサポートしていない場合、クエリは各親に順番に渡されます。 これにより、集計ツリーの深さ優先検索によってプロパティの検索が解決される動作が作成されます。

このオブジェクトモデル内の機能拡張は、すべてのオブジェクトがそれ自体の集合であり、親モデルのツリーであるという概念により、非常に単純です。 拡張機能は、別のオブジェクトの親モデルの一覧に追加できます。 この操作を行うと、オブジェクトが**拡張**されます。 この方法では、オブジェクトまたは値の特定のインスタンス、ネイティブ型、デバッガーのプロセスやスレッドの概念、または "all 反復可能な objects" の概念に加えて、機能を追加することができます。

### <a name="context-context-and-context-the-this-pointer-the-address-space-and-implementation-private-data"></a>コンテキスト、コンテキスト、およびコンテキスト: **this**ポインター、アドレス空間、および実装のプライベートデータ

**コンテキスト**には、オブジェクトモデルのコンテキスト内で理解する必要がある3つの概念があります。

#### <a name="context-the-this-pointer"></a>コンテキスト: **this**ポインター

特定のプロパティまたはメソッドは任意のレベルのデータモデルツリーに実装される可能性があるため、メソッドまたはプロパティの実装で元のオブジェクトにアクセスできるようにする必要があります (**こ**のC++ポインターを呼び出すか、JavaScript で**この**オブジェクトを呼び出すことができます)。 このインスタンスオブジェクトは、説明されているメソッドの**コンテキスト**と呼ばれる最初の引数として、さまざまなメソッドに渡されます。

#### <a name="context-the-address-space"></a>コンテキスト: アドレス空間

**コンテキスト**(ターゲット、プロセス、および参照しているスレッド) が現在の ui 状態を基準とするすべての api を含む UI 概念であるとは異なり、データモデルインターフェイスは、通常、明示的または暗黙的に*IDebugHostContext*インターフェイスとしてこのコンテキストを取得します。 データモデル内の各*Imodelobject*は、この種類のコンテキスト情報を格納し、返されたオブジェクトにそのコンテキストを反映させることができます。 つまり、ネイティブ値または*Imodelobject*からのキー値を読み取ると、ターゲットからオブジェクトが読み取られ、オブジェクトが最初に取得されたプロセスが読み取られます。

*IDebugHostContext*引数を受け取るメソッドに渡すことができる、明示的な定数値 **\_現在\_ホスト\_コンテキストを使用**します。 この値は、コンテキストがデバッガーの現在の UI の状態であることを示します。 ただし、この概念は明示的である必要があります。

#### <a name="context-implementation-private-data"></a>コンテキスト: 実装のプライベートデータ

データモデル内の各オブジェクトは、実際にはオブジェクトインスタンスの集計であり、アタッチされている親モデルのツリーであることに注意してください。
これらの各親モデル (多くの異なるオブジェクトのチェーンにリンクできます) は、プライベート実装データを任意のインスタンスオブジェクトに関連付けることができます。 作成される各*Imodelobject*は、概念的には、特定の親モデルから*IUnknown*インターフェイスによって定義されるプライベートインスタンスデータにマップされるハッシュテーブルを持ちます。 これにより、親モデルはすべてのインスタンスの情報をキャッシュしたり、それ以外の任意のデータを関連付けたりすることができます。

この種類のコンテキストには、 *Imodelobject*の*GetContextForDataModel*メソッドと*SetContextForDataModel*メソッドを使用してアクセスします。

## <a name="span-idimodelobjectspan-the-core-debugger-object-interface-imodelobject"></a><span id="imodelobject"></span>コアデバッガーオブジェクトインターフェイス: **Imodelobject**

-------------------------------------------

*Imodelobject*インターフェイスは、次のように定義されています。

```cpp
DECLARE_INTERFACE_(IModelObject, IUnknown)
{
    STDMETHOD(QueryInterface)(_In_ REFIID iid, _COM_Outptr_ PVOID* iface);
    STDMETHOD_(ULONG, AddRef)();
    STDMETHOD_(ULONG, Release)() PURE;
    STDMETHOD(GetContext)(_COM_Outptr_result_maybenull_ IDebugHostContext** context) PURE;
    STDMETHOD(GetKind)(_Out_ ModelObjectKind *kind) PURE;
    STDMETHOD(GetIntrinsicValue)(_Out_ VARIANT* intrinsicData);
    STDMETHOD(GetIntrinsicValueAs)(_In_ VARTYPE vt, _Out_ VARIANT* intrinsicData) PURE;
    STDMETHOD(GetKeyValue)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetKeyValue)(_In_ PCWSTR key, _In_opt_ IModelObject* object) PURE;
    STDMETHOD(EnumerateKeyValues)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
    STDMETHOD(GetRawValue)(_In_ SymbolKind kind, _In_ PCWSTR name, _In_ ULONG searchFlags, _COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(EnumerateRawValues)(_In_ SymbolKind kind, _In_ ULONG searchFlags, _COM_Outptr_ IRawEnumerator** enumerator) PURE;
    STDMETHOD(Dereference)(_COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(TryCastToRuntimeType)(_COM_Errorptr_ IModelObject** runtimeTypedObject) PURE;
    STDMETHOD(GetConcept)(_In_ REFIID conceptId, _COM_Outptr_ IUnknown** conceptInterface, _COM_Outptr_opt_result_maybenull_ IKeyStore** conceptMetadata) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetTypeInfo)(_Out_ IDebugHostType** type) PURE;
    STDMETHOD(GetTargetInfo)(_Out_ Location* location, _Out_ IDebugHostType** type) PURE;
    STDMETHOD(GetNumberOfParentModels)(_Out_ ULONG64* numModels) PURE;
    STDMETHOD(GetParentModel)(_In_ ULONG64 i, _COM_Outptr_ IModelObject **model, _COM_Outptr_result_maybenull_ IModelObject **contextObject) PURE;
    STDMETHOD(AddParentModel)(_In_ IModelObject* model, _In_opt_ IModelObject* contextObject, _In_ bool override) PURE;
    STDMETHOD(RemoveParentModel)(_In_ IModelObject* model) PURE;
    STDMETHOD(GetKey)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(GetKeyReference)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** objectReference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetKey)(_In_ PCWSTR key, _In_opt_ IModelObject* object, _In_opt_ IKeyStore* metadata) PURE;
    STDMETHOD(ClearKeys)() PURE;
    STDMETHOD(EnumerateKeys)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
    STDMETHOD(EnumerateKeyReferences)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
    STDMETHOD(SetConcept)(_In_ REFIID conceptId, _In_ IUnknown* conceptInterface, _In_opt_ IKeyStore* conceptMetadata) PURE;
    STDMETHOD(ClearConcepts)() PURE;
    STDMETHOD(GetRawReference)(_In_ SymbolKind kind, _In_ PCWSTR name, _In_ ULONG searchFlags, _COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(EnumerateRawReferences)(_In_ SymbolKind kind, _In_ ULONG searchFlags, _COM_Outptr_ IRawEnumerator** enumerator) PURE;
    STDMETHOD(SetContextForDataModel)(_In_ IModelObject* dataModelObject, _In_ IUnknown* context) PURE;
    STDMETHOD(GetContextForDataModel)(_In_ IModelObject* dataModelObject, _Out_ IUnknown** context) PURE;
    STDMETHOD(Compare)(_In_ IModelObject* other, _COM_Outptr_opt_result_maybenull_ IModelObject **ppResult) PURE;
    STDMETHOD(IsEqualTo)(_In_ IModelObject* other, _Out_ bool* equal) PURE;
}
```

**基本メソッド**

次に、IModelObject によって表されるあらゆる種類のオブジェクトに適用できる一般的な方法を示します。 

```cpp
STDMETHOD(GetKind)(_Out_ ModelObjectKind *kind) PURE;
STDMETHOD(GetContext)(_COM_Outptr_result_maybenull_ IDebugHostContext** context) PURE;
STDMETHOD(GetIntrinsicValue)(_Out_ VARIANT* intrinsicData);
STDMETHOD(GetIntrinsicValueAs)(_In_ VARTYPE vt, _Out_ VARIANT* intrinsicData) PURE;
STDMETHOD(Compare)(_In_ IModelObject* other, _COM_Outptr_opt_result_maybenull_ IModelObject **ppResult) PURE;
STDMETHOD(IsEqualTo)(_In_ IModelObject* other, _Out_ bool* equal) PURE;
STDMETHOD(Dereference)(_COM_Errorptr_ IModelObject** object) PURE;
```

[GetKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getkind) 

GetKind メソッドは、IModelObject 内にボックス化されているオブジェクトの種類を返します。 

[GetContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getcontext)

GetContext メソッドは、オブジェクトに関連付けられているホストコンテキストを返します。 

[GetIntrinsicValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getintrinsicvalue)

GetIntrinsicValue メソッドは、IModelObject 内にボックス化されたものを返します。 このメソッドは、ボックス化された組み込みのインターフェイスまたはボックス化された特定のインターフェイスを表す IModelObject インターフェイスでのみ、合法的に呼び出すことができます。 ネイティブオブジェクト、値オブジェクト、合成オブジェクト、および参照オブジェクトに対して呼び出すことはできません。 GetIntrinsicValueAs メソッドは、指定されたバリアント型に値を変換する GetIntrinsicValue メソッドと同様に動作します。 変換を実行できない場合、メソッドはエラーを返します。

[IsEqualTo](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-isequalto)

IsEqualTo メソッドは、2つのモデルオブジェクトを比較し、値が等しいかどうかを返します。 順序付けを持つオブジェクトの場合、このメソッドは true を返し、Compare メソッドと同じです。 順序付けされていないが equatable のオブジェクトの場合、Compare メソッドは失敗しますが、これは失敗します。 値に基づく比較の意味は、オブジェクトの型によって定義されます。 現時点では、これは組み込み型およびエラーオブジェクトに対してのみ定義されています。 Equatability の現在のデータモデルの概念はありません。 

[Dereference](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-dereference)

逆参照メソッドは、オブジェクトを逆参照します。 このメソッドは、データモデルベースの参照 (ObjectTargetObjectReference、ObjectKeyReference) またはネイティブ言語参照 (ポインターまたは言語参照) を逆参照するために使用できます。 このメソッドは、オブジェクトの1つのレベルの参照セマンティクスを削除することに注意してください。 たとえば、言語参照へのデータモデル参照を持つことができます。 このような場合は、最初に逆参照メソッドを呼び出すと、データモデル参照が削除され、言語参照はそのままになります。 その結果のオブジェクトで逆参照を呼び出すと、その後、言語参照が削除され、その参照の下にネイティブ値が返されます。 


**キーの操作方法**

キー、値、およびメタデータの組のディクショナリであるすべての合成オブジェクトには、それらのキー、値、およびそれらに関連付けられているメタデータを操作するための一連のメソッドがあります。 

Api の値ベースの形式は次のとおりです。 

```cpp
STDMETHOD(GetKeyValue)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
STDMETHOD(SetKeyValue)(_In_ PCWSTR key, _In_opt_ IModelObject* object) PURE;
STDMETHOD(EnumerateKeyValues)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
The key based forms of the APIs (including those used for key creation) are: 
STDMETHOD(GetKey)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
STDMETHOD(SetKey)(_In_ PCWSTR key, _In_opt_ IModelObject* object, _In_opt_ IKeyStore* metadata) PURE;
STDMETHOD(EnumerateKeys)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
STDMETHOD(ClearKeys)() PURE;
```

Api の参照ベースの形式は次のとおりです。 

```cpp
STDMETHOD(GetKeyReference)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** objectReference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
STDMETHOD(EnumerateKeyReferences)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
```

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getkeyvalue)

GetKeyValue メソッドは、指定されたキー (およびに関連付けられているメタデータ) の値を名前で取得するために、クライアントが最初に行うメソッドです。 キーがプロパティアクセサーの場合、これはボックス化された IModelPropertyAccessor である IModelObject としての値であるため、GetKeyValue メソッドは、実際の値を取得するために、プロパティアクセサーの GetValue メソッドを自動的に呼び出します。

[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-setkeyvalue)

SetKeyValue メソッドは、キーの値を設定するために、クライアントが最初に行うメソッドです。 このメソッドを使用してオブジェクトに新しいキーを作成することはできません。 既存のキーの値だけが設定されます。 多くのキーが読み取り専用であることに注意してください (例: プロパティアクセサーによって実装され、その SetValue メソッドから E_NOT_IMPL を返すことに注意してください)。 読み取り専用キーで呼び出された場合、このメソッドは失敗します。 

[EnumerateKeyValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeyvalues)

EnumerateKeyValues メソッドは、オブジェクトのすべてのキーを列挙するために、クライアントが最初に行うメソッドです (これには、親モデルのツリーの任意の場所に実装されているすべてのキーが含まれます)。 EnumerateKeyValues は、オブジェクトツリー内の重複する名前によって定義されているキーを列挙することに注意してください。ただし、GetKeyValue や SetKeyValue などのメソッドは、指定された名前を持つキーの最初のインスタンスを、深さ優先の検査で検出されたものとしてのみ操作します。 

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getkey)

GetKey メソッドは、指定されたキー (およびに関連付けられているメタデータ) の値を名前で取得します。 ほとんどのクライアントでは、代わりに GetKeyValue メソッドを使用する必要があります。 キーがプロパティアクセサーの場合、このメソッドを呼び出すと、IModelObject にボックス化されたプロパティアクセサー (IModelPropertyAccessor インターフェイス) が返されます。 GetKeyValue とは異なり、このメソッドは GetValue メソッドを呼び出すことによって、キーの基になる値を自動的に解決しません。 その責任は、呼び出し元のです。 

[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-setkey)

SetKey メソッドは、オブジェクトに対してキーを作成するためにクライアントが変換するメソッドであり、メタデータを作成したキーに関連付けることもできます。 指定されたオブジェクトに指定された名前のキーが既に存在する場合は、次の2つの動作のいずれかが発生します。 キーがこのによって指定されたインスタンス上にある場合、そのキーの値は、元のキーが存在しないかのように置き換えられます。 一方、キーがこのによって指定されたインスタンスの親データモデルのチェーンにある場合は、このによって指定されたインスタンスに、指定された名前の新しいキーが作成されます。 これにより、オブジェクトは同じ名前の2つのキーを持つことになります (基底クラスと同じ名前のメンバーをシャドウする派生クラスに似ています)。 

[EnumerateKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeys)

EnumerateKeys メソッドは、EnumerateKeyValues メソッドと同様に動作し、オブジェクトのプロパティアクセサーを自動的に解決しません。 つまり、キーの値がプロパティアクセサーの場合、EnumerateKeys メソッドは、GetValue メソッドを自動的に呼び出すのではなく、IModelObject にボックス化されたプロパティアクセサー (IModelPropertyAccessorInterface) を返します。 これは、GetKey と Getkey の違いに似ています。 

[ClearKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-clearkeys)

ClearKeys メソッドは、このによって指定されたオブジェクトのインスタンスから、すべてのキーとそれに関連付けられている値とメタデータを削除します。 このメソッドは、特定のオブジェクトインスタンスにアタッチされている親モデルには影響しません。 

[GetKeyReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getkeyreference)

GetKeyReference メソッドは、オブジェクト (またはその親モデルチェーン) で指定された名前のキーを検索し、IModelKeyReference にボックス化された IModelKeyReference インターフェイスによって指定されたそのキーへの参照を返します。 この参照は、後でキーの値を取得または設定するために使用できます。 

[EnumerateKeyReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeyreferences)

EnumerateKeyReferences メソッドは、EnumerateKeyValues メソッドと同様に動作します。これは、キーの値ではなく、IModelKeyReference インターフェイスによって、Imodelkeyreference にボックス化されたキーへの参照を返すことを指します。 このような参照を使用して、キーの基になる値を取得または設定できます。

**概念の操作方法**

モデルオブジェクトは、キー/値/メタデータタプルのディクショナリであるだけでなく、概念のコンテナーでもあります。 概念とは、またはオブジェクトによって実行できる抽象概念です。 概念とは、基本的には、オブジェクトがサポートするインターフェイスの動的なストアです。 現在、データモデルによっていくつかの概念が定義されています。 

概念インターフェイス | 説明
------------------|-------------
IDataModelConcept | 概念は親モデルです。 このモデルが登録された型のシグネチャを使用してネイティブ型に自動的にアタッチされる場合、そのような型の新しいオブジェクトがインスタンス化されるたびに、InitializeObject メソッドが自動的に呼び出されます。
IStringDisplayableConcept  | オブジェクトを文字列に変換して、表示することができます。
IIterableConcept  | オブジェクトはコンテナーであり、反復処理できます。
IIndexableConcept  | オブジェクトはコンテナーであり、1つまたは複数のディメンションで (ランダムアクセスによってアクセスされる) インデックスを作成できます。
IPreferredRuntimeTypeConcept  | オブジェクトは、基になる型システムから派生した型についてより多くの情報を認識し、静的な型からランタイム型への変換を処理することができます。
IDynamicKeyProviderConcept | オブジェクトはキーの動的プロバイダーであり、コアデータモデルからのすべての主要なクエリを引き継ぎます。 このインターフェイスは、通常、JavaScript などの動的言語へのブリッジとして使用されます。
IDynamicConceptProviderConcept  | オブジェクトは、概念の動的プロバイダーであり、コアデータモデルからのすべての概念クエリを引き継ぐことを望んでいます。 このインターフェイスは、通常、JavaScript などの動的言語へのブリッジとして使用されます。

IModelObject の次のメソッドは、オブジェクトがサポートする概念を操作するために使用されます。 

```cpp
STDMETHOD(GetConcept)(_In_ REFIID conceptId, _COM_Outptr_ IUnknown** conceptInterface, _COM_Outptr_opt_result_maybenull_ IKeyStore** conceptMetadata) PURE;
STDMETHOD(SetConcept)(_In_ REFIID conceptId, _In_ IUnknown* conceptInterface, _In_opt_ IKeyStore* conceptMetadata) PURE;
STDMETHOD(ClearConcepts)() PURE;
```

[GetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getconcept)

GetConcept メソッドは、オブジェクト (またはその親モデルチェーン) の概念を検索し、概念インターフェイスへのインターフェイスポインターを返します。 概念インターフェイスの動作とメソッドは、各概念に固有です。 ただし、多くの概念インターフェイスでは、呼び出し元がコンテキストオブジェクトを明示的に渡す必要があることに注意してください (または、これまでこのポインターを呼び出している可能性があります)。 すべての概念インターフェイスに正しいコンテキストオブジェクトが渡されるようにすることが重要です。

[SetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-setconcept)

SetConcept メソッドは、このポインターによって指定されたオブジェクトインスタンスに対して指定された概念を配置します。 こので指定されたオブジェクトインスタンスに関連付けられている親モデルが概念もサポートしている場合は、インスタンスの実装によって親モデル内のがオーバーライドされます。 

[ClearConcepts](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-clearconcepts)

ClearConcepts メソッドは、このによって指定されたオブジェクトのインスタンスからすべての概念を削除します。 

**ネイティブオブジェクトメソッド**

多くのモデルオブジェクトは、組み込み (整数、文字列など) または合成コンストラクト (キー/値/メタデータの組と概念のディクショナリ) を参照しますが、モデルオブジェクトはネイティブコンストラクト (たとえば、デバッグターゲットのアドレス空間にあるユーザー定義型) を参照することもあります。 IModelObject インターフェイスには、このようなネイティブオブジェクトに関する情報にアクセスするための一連のメソッドがあります。 これらのメソッドは次のとおりです。 

```cpp
STDMETHOD(GetRawValue)(_In_ SymbolKind kind, _In_ PCWSTR name, _In_ ULONG searchFlags, _COM_Errorptr_ IModelObject** object) PURE;
STDMETHOD(EnumerateRawValues)(_In_ SymbolKind kind, _In_ ULONG searchFlags, _COM_Outptr_ IRawEnumerator** enumerator) PURE;
STDMETHOD(TryCastToRuntimeType)(_COM_Errorptr_ IModelObject** runtimeTypedObject) PURE;
STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
STDMETHOD(GetTypeInfo)(_Out_ IDebugHostType** type) PURE;
STDMETHOD(GetTargetInfo)(_Out_ Location* location, _Out_ IDebugHostType** type) PURE;
STDMETHOD(GetRawReference)(_In_ SymbolKind kind, _In_ PCWSTR name, _In_ ULONG searchFlags, _COM_Errorptr_ IModelObject** object) PURE;
STDMETHOD(EnumerateRawReferences)(_In_ SymbolKind kind, _In_ ULONG searchFlags, _COM_Outptr_ IRawEnumerator** enumerator) PURE;
```

[GetRawValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getrawvalue)

GetRawValue メソッドは、指定されたオブジェクト内のネイティブコンストラクトを検索します。 このようなコンストラクトには、フィールド、基本クラス、基底クラスのフィールド、メンバー関数などがあります。

[列挙の値](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-enumeraterawvalues)

列挙 Aterawvalues メソッドは、指定されたオブジェクトのすべてのネイティブな子 (フィールド、基本クラスなど) を列挙します。 


[TryCastToRuntimeType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-trycasttoruntimetype)

TryCastToRuntimeType メソッドは、デバッグホストに対して分析を実行し、特定のオブジェクトの実際のランタイム型 (たとえば、最派生クラス) を判断するように要求します。 使用される正確な分析は、デバッグホストに固有のものでC++あり、RTTI (実行時の型情報)、オブジェクトの V テーブル (仮想関数テーブル) 構造の検査、またはホストが静的型から動的/ランタイム型を確実に決定するために使用できるその他の手段を含むことができます。 ランタイム型に変換できないことは、このメソッドの呼び出しが失敗することを意味するわけではありません。 このような場合、メソッドは、指定されたオブジェクト (this ポインター) を出力引数に返します。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getlocation) 

GetLocation メソッドは、ネイティブオブジェクトの場所を返します。 このような場所は通常、デバッグターゲットのアドレス空間内の仮想アドレスですが、必ずしもそうであるとは限りません。 このメソッドによって返される場所は、仮想アドレス、レジスタまたはサブレジスタ内の配置を示す、またはデバッグホストで定義されている他の任意のアドレス空間を示す可能性がある抽象的な場所です。 結果として得られる場所オブジェクトの HostDefined フィールドが0の場合、その場所は実際には仮想アドレスであることを示します。 このような仮想アドレスは、結果として得られる場所のオフセットフィールドを調べることによって取得できます。 HostDefined フィールドの0以外の値は、オフセットフィールドがそのアドレス空間内のオフセットである代替アドレス空間を示します。 ここでは、0以外の HostDefined 値の正確な意味は、デバッグホストに対してプライベートです。 

[GetTypeInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-gettypeinfo)

GetTypeInfo メソッドは、指定されたオブジェクトのネイティブ型を返します。 オブジェクトにネイティブ型情報が関連付けられていない場合 (たとえば、組み込みなど)、呼び出しは成功しますが、は null を返します。 

[GetTargetInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-gettargetinfo)

GetTargetInfo メソッドは、実質的には、指定されたオブジェクトの抽象位置とネイティブ型の両方を返す GetLocation メソッドと GetTypeInfo メソッドを組み合わせたものです。 

[GetRawReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getrawreference)

GetRawReference メソッドは、指定されたオブジェクト内でネイティブコンストラクトを検索し、そのオブジェクトへの参照を返します。 このようなコンストラクトには、フィールド、基本クラス、基底クラスのフィールド、メンバー関数などがあります。ここで返される参照 (ObjectTargetObjectReference 型のオブジェクト) を言語リファレンスから区別することが重要です (例: C++ & や & & スタイル参照)。 

[列挙の参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-enumeraterawreferences)

列挙 Aterawreferences メソッドは、指定されたオブジェクトのすべてのネイティブな子 (例: フィールド、基本クラスなど) への参照を列挙します。 


**拡張メソッド**

前に説明したように、モデルオブジェクトは JavaScript オブジェクトおよびプロトタイプチェーンと非常によく似ています。 特定の IModelObject インターフェイスによって表されるインスタンスに加えて、任意の数の親モデルがオブジェクトにアタッチされている場合もあります (それぞれに、任意の数の親モデルがアタッチされている場合があります)。 これは、データモデル内の機能拡張の主な手段です。 特定のプロパティまたは概念が特定のインスタンス内に配置できない場合は、インスタンスをルートとするオブジェクトツリー (親モデルによって定義) の深さ優先検索が実行されます。

次のメソッドは、特定の IModelObject インスタンスに関連付けられている親モデルのチェーンを操作します。 

```cpp
STDMETHOD(GetNumberOfParentModels)(_Out_ ULONG64* numModels) PURE;
STDMETHOD(GetParentModel)(_In_ ULONG64 i, _COM_Outptr_ IModelObject **model, _COM_Outptr_result_maybenull_ IModelObject **contextObject) PURE;
STDMETHOD(AddParentModel)(_In_ IModelObject* model, _In_opt_ IModelObject* contextObject, _In_ bool override) PURE;
STDMETHOD(RemoveParentModel)(_In_ IModelObject* model) PURE;
STDMETHOD(SetContextForDataModel)(_In_ IModelObject* dataModelObject, _In_ IUnknown* context) PURE;
STDMETHOD(GetContextForDataModel)(_In_ IModelObject* dataModelObject, _Out_ IUnknown** context) PURE;
```

[GetNumberOfParentModels](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getnumberofparentmodels)

GetNumberOfParentModels メソッドは、指定されたオブジェクトインスタンスにアタッチされている親モデルの数を返します。 親モデルは、親モデルチェーンの線形の順序で、深さ優先のプロパティを検索します。 

[GetParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getparentmodel)

GetParentModel メソッドは、指定されたオブジェクトの親モデルチェーン内の i 番目の親モデルを返します。 親モデルは、追加または列挙された線形の順序で、プロパティまたは概念を検索します。 Index i が0の親モデルは、index i + 1 の親モデルの前に (階層的に) 検索されます。 

[AddParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-addparentmodel)

AddParentModel メソッドは、指定されたオブジェクトに新しい親モデルを追加します。 このようなモデルは、検索チェーンの末尾 (override 引数が false として指定されている場合) または検索チェーンの先頭に追加される場合があります (override 引数は true として指定されます)。 また、各親モデルでは、必要に応じて、指定された親 (または親階層内のすべてのユーザー) 上のプロパティまたは概念のコンテキスト (セマンティック this ポインター) を調整することもできます。 コンテキストの調整はほとんど使用されませんが、オブジェクトの埋め込みや名前空間の構築など、いくつかの強力な概念が可能です。 

[RemoveParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-removeparentmodel)

RemoveParentModel は、指定されたオブジェクトの親検索チェーンから、指定された親モデルを削除します。 

[SetContextForDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-setcontextfordatamodel)

SetContextForDataModel メソッドは、インスタンスオブジェクトに実装データを配置するためにデータモデルを実装するために使用されます。 概念的には、各 IModelObject (このインスタンスをわかりやすくするために呼び出す) には、状態のハッシュテーブルが含まれています。 ハッシュテーブルには、別の IModelObject によってインデックスが作成されます (わかりやすくするために、このデータモデルを呼び出します)。これは、インスタンスの親モデル階層にあります。 このハッシュに含まれる値は、IUnknown インスタンスによって表される参照カウント状態情報のセットです。 データモデルによってインスタンスにこの状態が設定されると、プロパティの getter などで取得できる任意の実装データを格納できます。 

[GetContextForDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelobject-getcontextfordatamodel)

GetContextForDataModel メソッドは、SetContextForDataModel の前の呼び出しで設定されたコンテキスト情報を取得するために使用されます。 これにより、インスタンスオブジェクトの親モデル階層のさらに上にあるデータモデルによってインスタンスオブジェクトに設定された状態情報が取得されます。 このコンテキスト/状態とその意味の詳細については、SetContextForDataModel のドキュメントを参照してください。 

## <a name="span-idobjecttypesspan-debugger-data-model-core-object-types"></a><span id="objecttypes"></span>デバッガーデータモデルのコアオブジェクトの種類

データモデルのオブジェクトは、.NET のオブジェクトの概念に似ています。 これは、データモデルによって認識されるコンストラクトをボックス化できる汎用コンテナーです。 ネイティブオブジェクトと合成 (動的) オブジェクトに加えて、IModelObject のコンテナーに配置 (またはボックス化) できる一連の主要なオブジェクト型があります。 これらの値のほとんどが配置されているコンテナーは標準の COM/OLE バリアントであり、そのバリアントに含めることのできる制限がいくつかあります。 最も基本的な種類は次のとおりです。

- 8ビット符号なしの値と符号付きの値 (VT_UI1、VT_I1)
- 16ビットの符号なしの値と符号付きの値 (VT_UI2、VT_UI2)
- 32ビットの符号なしの値と符号付きの値 (VT_UI4、VT_I4)
- 64ビットの符号なしの値と符号付きの値 (VT_UI8、VT_I8)
- 単精度浮動小数点浮動小数点値 (VT_R4、VT_R8)
- 文字列 (VT_BSTR)
- ブール値 (VT_BOOL)

これらの基本的な型に加えて、多数のコアデータモデルオブジェクトが、格納されている IUnknown が特定のインターフェイスを実装することが保証される VT_UNKNOWN によって定義される IModelObject に配置されます。 これらの型は次のとおりです。 

- プロパティアクセサー (IModelPropertyAccessor)
- Method オブジェクト (IModelMethod)
- キー参照オブジェクト (IModelKeyReference または IModelKeyReference2)
- コンテキストオブジェクト (IDebugModelHostContext)

**プロパティアクセサー: *IModelPropertyAccessor***

データモデルのプロパティアクセサーは、IModelObject にボックス化された IModelPropertyAccessor インターフェイスを実装したものです。 クエリを実行すると、モデルオブジェクトは ObjectPropertyAccessor の種類を返します。組み込み値は、IModelPropertyAccessor に対してクエリ可能であることが保証されている VT_UNKNOWN です。 プロセスでは、IModelPropertyAccessor に対して静的に安定していることが保証されています。 

プロパティアクセサーは、データモデルでキー値を取得および設定するためのメソッド呼び出しを取得するための間接的な方法です。 指定されたキーの値がプロパティアクセサーの場合、GetKeyValue および SetKeyValue メソッドはこれに自動的に通知し、必要に応じて、プロパティアクセサーの基になる GetValue または SetValue メソッドを呼び出します。 

IModelPropertyAccessor インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IModelPropertyAccessor, IUnknown)
{
    STDMETHOD(GetValue)(_In_ PCWSTR key, _In_opt_ IModelObject* contextObject, _COM_Outptr_ IModelObject** value) PURE;
    STDMETHOD(SetValue)(_In_ PCWSTR key, _In_opt_ IModelObject* contextObject, _In_ IModelObject* value) PURE; 
}
```

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelpropertyaccessor-getvalue)

GetValue メソッドは、プロパティアクセサーの getter です。 これは、クライアントがプロパティの基になる値を取得しようとするたびに呼び出されます。 プロパティアクセサーを直接取得する呼び出し元は、キー名と正確なインスタンスオブジェクト (this ポインター) をプロパティアクセサーの GetValue メソッドに渡す必要があることに注意してください。 

[SetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelpropertyaccessor-setvalue)

SetValue メソッドは、プロパティアクセサーの setter です。 これは、クライアントが基になるプロパティに値を割り当てようとするたびに呼び出されます。 多くのプロパティは読み取り専用です。 このような場合、SetValue メソッドを呼び出すと E_NOTIMPL が返されます。 プロパティアクセサーを直接取得する呼び出し元は、キー名と正確なインスタンスオブジェクト (this ポインター) をプロパティアクセサーの SetValue メソッドに渡す必要があることに注意してください。 

**メソッド: *Imodelmethod***

データモデルのメソッドは IModelMethod インターフェイスを実装したもので、IModelObject にボックス化されています。 モデルオブジェクトは、クエリの実行時に ObjectMethod の種類を返します。組み込み値は VT_UNKNOWN であり、IModelMethod でクエリ可能であることが保証されています。 プロセスでは、IModelMethod に対して静的に安定していることが保証されます。 データモデルのすべてのメソッドは、本質的に動的です。 これらは、0個以上の引数のセットを入力として受け取り、1つの出力値を返します。 オーバーロードの解決はなく、パラメーター名、型、または予測に関するメタデータもありません。 

IModelMethod インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IModelMethod, IUnknown)
{
    STDMETHOD(Call)(_In_opt_ IModelObject *pContextObject, _In_ ULONG64 argCount, _In_reads_(argCount) IModelObject **ppArguments, _COM_Errorptr_ IModelObject **ppResult, _COM_Outptr_opt_result_maybenull_ IKeyStore **ppMetadata) PURE;
}
```

[Call](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelmethod-call)

呼び出しメソッドは、データモデルで定義されているメソッドを呼び出す方法です。 呼び出し元は、正確なインスタンスオブジェクト (this ポインター) と任意の引数セットを渡す役割を担います。 メソッドの結果と、その結果に関連付けられているオプションのメタデータが返されます。 論理的に値を返さないメソッドは、有効な IModelObject を返す必要があります。 このような場合、IModelObject はボックス化されていない値です。 メソッドが失敗した場合、(返された HRESULT がエラーの場合でも) 入力引数にオプションの拡張エラー情報が返されることがあります。 呼び出し元がこのことを確認する必要があります。 

**キー参照: *Imodelkeyreference または IModelKeyReference2***

キー参照は、基本的には特定のオブジェクトのキーへのハンドルです。 クライアントは、GetKeyReference などのメソッドを使用してこのようなハンドルを取得し、後でハンドルを使用して、元のオブジェクトを保持することなく、キーの値を取得または設定できます。 この型のオブジェクトは IModelKeyReference または IModelKeyReference2 インターフェイスを実装したもので、Imodelkeyreference にボックス化されています。 モデルオブジェクトは、クエリを実行すると、ObjectKeyReference の種類を返します。その後、組み込み値は VT_UNKNOWN であり、IModelKeyReference でクエリ可能であることが保証されます。 プロセスでは、IModelKeyReference に対して静的に安定していることが保証されます。 

キー参照インターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IModelKeyReference2, IModelKeyReference)
{
    STDMETHOD(GetKeyName)(_Out_ BSTR* keyName) PURE;
    STDMETHOD(GetOriginalObject)(_COM_Outptr_ IModelObject** originalObject) PURE;
    STDMETHOD(GetContextObject)(_COM_Outptr_ IModelObject** containingObject) PURE;
    STDMETHOD(GetKey)(_COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(GetKeyValue)(_COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetKey)(_In_opt_ IModelObject* object, _In_opt_ IKeyStore* metadata) PURE;
    STDMETHOD(SetKeyValue)(_In_ IModelObject* object) PURE;
    STDMETHOD(OverrideContextObject)(_In_ IModelObject* newContextObject) PURE;
}
```

[GetKeyName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelkeyreference-getkeyname)

GetKeyName メソッドは、このキー参照がハンドルであるキーの名前を返します。 返される文字列は標準の BSTR であり、SysFreeString の呼び出しを使用して解放する必要があります。 

[GetOriginalObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelkeyreference-getoriginalobject)

GetOriginalObject メソッドは、キー参照の作成元のインスタンスオブジェクトを返します。 キー自体がインスタンスオブジェクトの親モデルに存在する可能性があることに注意してください。 

[GetContextObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelkeyreference-getcontextobject)

GetContextObject メソッドは、問題のキーがプロパティアクセサーを参照している場合に、プロパティアクセサーの GetValue または SetValue メソッドに渡されるコンテキスト (this ポインター) を返します。 ここで返されるコンテキストオブジェクトは、GetOriginalObject からフェッチされた元のオブジェクトと同じか、または異なる場合があります。 キーが親モデルにあり、その親モデルに関連付けられたコンテキスト adjustor が存在する場合、元のオブジェクトは、GetKeyReference または EnumerateKeyReferences が呼び出されたインスタンスオブジェクトです。 コンテキストオブジェクトは、元のオブジェクトと、このキー参照がハンドルであるキーを含む親モデルとの間の最終的なコンテキスト adjustor から取得されます。 コンテキスト adjustors が存在しない場合、元のオブジェクトとコンテキストオブジェクトは同じになります。 

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelkeyreference-getkey)

キー参照の GetKey メソッドは、IModelObject の GetKey メソッドとして動作します。 このメソッドは、基になるキーと、そのキーに関連付けられているメタデータの値を返します。 キーの値がプロパティアクセサーである場合、これは IModelObject にボックス化されたプロパティアクセサー (IModelPropertyAccessor) を返します。 このメソッドは、プロパティアクセサーで基になる GetValue メソッドまたは SetValue メソッドを呼び出しません。 

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelkeyreference-getkeyvalue)

キー参照の GetKeyValue メソッドは、IModelObject の GetKeyValue メソッドとして動作します。 このメソッドは、基になるキーと、そのキーに関連付けられているメタデータの値を返します。 キーの値がプロパティアクセサーの場合は、プロパティアクセサーの基になる GetValue メソッドが自動的に呼び出されます。 

[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelkeyreference-setkey)

キー参照の SetKey メソッドは、IModelObject の SetKey メソッドとして動作します。 キーの値が割り当てられます。 元のキーがプロパティアクセサーの場合は、プロパティアクセサーが置き換えられます。 プロパティアクセサーで SetValue メソッドを呼び出すことはありません。 


[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelkeyreference-setkeyvalue)

キー参照の SetKeyValue メソッドは、IModelObject の SetKeyValue メソッドとして動作します。 キーの値が割り当てられます。 元のキーがプロパティアクセサーの場合、プロパティアクセサー自体を置き換えるのではなく、プロパティアクセサーで基になる SetValue メソッドを呼び出します。

[OverrideContextObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodelkeyreference2-overridecontextobject)

OverrideContextObject メソッド (IModelKeyReference2 にのみ存在) は高度なメソッドです。このメソッドは、このキー参照が基になるプロパティアクセサーの GetValue または SetValue メソッドに渡すコンテキストオブジェクトを完全に変更するために使用されます。 このメソッドに渡されるオブジェクトは、GetContextObject の呼び出しからも返されます。 このメソッドは、特定の動的言語の動作をレプリケートするためにスクリプトプロバイダーによって使用されます。 ほとんどのクライアントでは、このメソッドを呼び出すことはできません。 


**コンテキストオブジェクト: *IDebugHostContext***

コンテキストオブジェクトは、(データモデルと連携して) デバッグホストがすべてのオブジェクトに関連付けている情報の非透過的な blob です。 これには、情報の取得元のプロセスコンテキストやアドレス空間などが含まれます。コンテキストオブジェクトは、IModelObject 内にボックス化された IDebugHostContext の実装です。 IDebugHostContext はホストで定義されたインターフェイスであることに注意してください。 クライアントはこのインターフェイスを実装しません。 

コンテキストオブジェクトの詳細については、「デバッガーデータモデルの[ C++ホストインターフェイス](data-model-cpp-interfaces.md#hostinterface)」 C++を参照してください。 

## <a name="span-idmodelmanager-the-data-model-manager"></a>データモデルマネージャーの <span id="modelmanager">  

Data model manager、IDataModelManager2 (またはそれより前の IDataModelManager) へのコアインターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IDataModelManager2, IDataModelManager)
{
    //
    // IDataModelManager:
    //
    STDMETHOD(Close)() PURE;
    STDMETHOD(CreateNoValue)(_Out_ IModelObject** object) PURE;
    STDMETHOD(CreateErrorObject)(_In_ HRESULT hrError, _In_opt_ PCWSTR pwszMessage, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(CreateTypedObject)(_In_opt_ IDebugHostContext* context, _In_ Location objectLocation, _In_ IDebugHostType* objectType, _COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(CreateTypedObjectReference)(_In_opt_ IDebugHostContext* context, _In_ Location objectLocation, _In_ IDebugHostType* objectType, _COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(CreateSyntheticObject)(_In_opt_ IDebugHostContext* context, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(CreateDataModelObject)(_In_ IDataModelConcept* dataModel, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(CreateIntrinsicObject)(_In_ ModelObjectKind objectKind, _In_ VARIANT* intrinsicData, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(CreateTypedIntrinsicObject)(_In_ VARIANT* intrinsicData, _In_ IDebugHostType* type, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(GetModelForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _Out_ IModelObject** dataModel) PURE;
    STDMETHOD(GetModelForType)(_In_ IDebugHostType* type, _COM_Outptr_ IModelObject** dataModel, _COM_Outptr_opt_ IDebugHostTypeSignature** typeSignature, _COM_Outptr_opt_ IDebugHostSymbolEnumerator** wildcardMatches) PURE;
    STDMETHOD(RegisterModelForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _In_ IModelObject* dataModel) PURE;
    STDMETHOD(UnregisterModelForTypeSignature)(_In_ IModelObject* dataModel, _In_opt_ IDebugHostTypeSignature* typeSignature) PURE;
    STDMETHOD(RegisterExtensionForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _In_ IModelObject* dataModel) PURE;
    STDMETHOD(UnregisterExtensionForTypeSignature)(_In_ IModelObject* dataModel, _In_opt_ IDebugHostTypeSignature* typeSignature) PURE;
    STDMETHOD(CreateMetadataStore)(_In_opt_ IKeyStore* parentStore, _COM_Outptr_ IKeyStore** metadataStore) PURE;
    STDMETHOD(GetRootNamespace)(_COM_Outptr_ IModelObject** rootNamespace) PURE;
    STDMETHOD(RegisterNamedModel)(_In_ PCWSTR modelName, _In_ IModelObject *modeObject) PURE;
    STDMETHOD(UnregisterNamedModel)(_In_ PCWSTR modelName) PURE;
    STDMETHOD(AcquireNamedModel)(_In_ PCWSTR modelName, _COM_Outptr_ IModelObject **modelObject) PURE;
    //
    // IDataModelManager2:
    //
    STDMETHOD(AcquireSubNamespace)(_In_ PCWSTR modelName, _In_ PCWSTR subNamespaceModelName, _In_ PCWSTR accessName, _In_opt_ IKeyStore *metadata, _COM_Outptr_ IModelObject **namespaceModelObject) PURE;
    STDMETHOD(CreateTypedIntrinsicObjectEx)(_In_opt_ IDebugHostContext* context, _In_ VARIANT* intrinsicData, _In_ IDebugHostType* type, _COM_Outptr_ IModelObject** object) PURE;
}
```

**管理方法**

データモデルをホストしているアプリケーション (例: デバッガー) では、次の一連のメソッドが使用されます。 

```cpp
STDMETHOD(Close)() PURE;
```

[閉じる](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-close)

Close メソッドは、データモデルマネージャーのシャットダウンプロセスを開始するために、データモデルをホストするアプリケーション (例: デバッガー) によって、データモデルマネージャーで呼び出されます。 データモデルマネージャーで最終的な参照をリリースする前に Close メソッドではないデータモデルのホストは、データモデルの管理インフラストラクチャの重大なリークを含むが未定義の動作を引き起こす可能性があります。 

**オブジェクトの作成/ボックス化メソッド**

次の一連のメソッドは、新しいオブジェクトまたはボックスの値を IModelObject に作成するために使用されます。これは、データモデルのコアインターフェイスです。 

```cpp
STDMETHOD(CreateNoValue)(_Out_ IModelObject** object) PURE;
STDMETHOD(CreateErrorObject)(_In_ HRESULT hrError, _In_opt_ PCWSTR pwszMessage, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateTypedObject)(_In_opt_ IDebugHostContext* context, _In_ Location objectLocation, _In_ IDebugHostType* objectType, _COM_Errorptr_ IModelObject** object) PURE;
STDMETHOD(CreateTypedObjectReference)(_In_opt_ IDebugHostContext* context, _In_ Location objectLocation, _In_ IDebugHostType* objectType, _COM_Errorptr_ IModelObject** object) PURE;
STDMETHOD(CreateSyntheticObject)(_In_opt_ IDebugHostContext* context, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateDataModelObject)(_In_ IDataModelConcept* dataModel, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateIntrinsicObject)(_In_ ModelObjectKind objectKind, _In_ VARIANT* intrinsicData, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateTypedIntrinsicObject)(_In_ VARIANT* intrinsicData, _In_ IDebugHostType* type, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateMetadataStore)(_In_opt_ IKeyStore* parentStore, _COM_Outptr_ IKeyStore** metadataStore) PURE;
STDMETHOD(CreateTypedIntrinsicObjectEx)(_In_opt_ IDebugHostContext* context, _In_ VARIANT* intrinsicData, _In_ IDebugHostType* type, _COM_Outptr_ IModelObject** object) PURE;
```

[Creatの値](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-createnovalue)

Creatの値のメソッドは、"no value" オブジェクトを作成し、それを IModelObject にボックス化して、それを返します。 返されるモデルオブジェクトの種類は ObjectNoValue です。 

"値なし" オブジェクトには、いくつかの意味的な意味があります。 

- (言語によって異なります) は、void、null、または undefined と同等のセマンティックと見なすことができます。
- 成功を返すプロパティアクセサーの GetValue メソッドと結果の "no value" オブジェクトは、特定のプロパティが特定のインスタンスに対して値を持たず、その特定のインスタンスに対してプロパティが存在しないかのように処理する必要があることを示します。
- 戻り値が意味のないデータモデルメソッドでは、これを sentinel として使用して、そのようなを示します (メソッドが有効な IModelObject を返す必要があるため)。

[CreateErrorObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-createerrorobject)

CreateErrorObject メソッドは、"error オブジェクト" を作成します。 データモデルには、例外と例外フローの概念がありません。 エラーは、次の2つの方法でプロパティ/メソッドから取得されます。

- 1つの失敗した HRESULT で、拡張エラー情報がありません。 エラーに対して指定できる情報がないか、返された HRESULT からエラー自体の内容がわかります。
- 1つの失敗した HRESULT と拡張エラー情報の組み合わせ。 拡張エラー情報は、プロパティ/メソッドの output 引数で返されるエラーオブジェクトです。

[CreateTypedObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedobject)

CreateTypedObject メソッドは、クライアントがデバッグターゲットのアドレス空間にネイティブ/言語オブジェクトの表現を作成できるようにするメソッドです。 新しく作成されたオブジェクトの型 (objectType 引数によって示される) が、データモデルマネージャーに登録されている1つ以上の型シグネチャと一致する場合、それらのデータモデルは自動的に呼び出し元に返される前に、作成されたインスタンスオブジェクトにアタッチされます。 

[CreateTypedObjectReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedobjectreference)

CreateTypedObjectReference メソッドは、基になるネイティブ/言語構成要素への参照を作成する CreateTypedObject メソッド違うと意味的に似ています。 作成された参照は、ObjectTargetObjectReference の一種を持つオブジェクトです。 これは、基になる言語がサポートしているようなネイティブ参照でC++はありません (例: & や & &)。 C++参照への ObjectTargetObjectReference を完全に使用できます。 ObjectTargetObjectReference という種類のオブジェクトは、IModelObject での逆参照メソッドを使用して、基になる値に変換できます。 適切な言語で値に戻すために、基になるホストの式エバリュエーターに参照を渡すこともできます。 

[オブジェクトのエンコード](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-createsyntheticobject)

このオブジェクトメソッドは、空のデータモデルオブジェクト (キー/値/メタデータの組と概念のディクショナリ) を作成します。 作成時には、オブジェクトにキーや概念はありません。 これは、呼び出し元が使用するためのクリーンなスレートです。 

[CreateDataModelObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-createdatamodelobject)

CreateDataModelObject メソッドは、データモデルであるオブジェクトを作成するための単純なヘルパーラッパーです。これは、他のオブジェクトに親モデルとしてアタッチされるオブジェクトです。 このようなオブジェクトはすべて、IDataModelConcept を介したデータモデルの概念をサポートする必要があります。 このメソッドは、明示的なコンテキストを指定せずに新しい空の合成オブジェクトを作成し、データモデルの概念の新しく作成されたオブジェクトの実装として inpassed れた IDataModelConcept を追加します。 これは、バイナリオブジェクトと SetConcept の呼び出しでも同様に実現できます。 

[CreateIntrinsicObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-createintrinsicobject)

CreateIntrinsicObject メソッドは、組み込み値を IModelObject にボックス化するメソッドです。 呼び出し元は、値を COM VARIANT に配置し、このメソッドを呼び出します。 データモデルマネージャーは、オブジェクトを表す IModelObject を返します。 このメソッドは、プロパティアクセサー、メソッド、コンテキストなどの基本的な IUnknown ベースの型をボックスにするためにも使用されることに注意してください。このような場合、objectKind メソッドは、オブジェクトが表す IUnknown ベースのコンストラクトの種類と、渡されたバリアントの punkVal フィールドが IUnknown 派生型であることを示します。 この型は、プロセス内の適切なモデルインターフェイス (例: IModelPropertyAccessor、IModelMethod、IDebugHostContext など) に対して静的に安定している必要があります。 このメソッドでサポートされているバリアント型は、VT_UI1、VT_I1、VT_UI2、VT_I2、VT_UI4、VT_I4、VT_UI8、VT_I8、VT_R4、VT_R8、VT_BOOL、VT_BSTR、および VT_UNKNOWN です (列挙体の ModelObjectKind によって示される一連の特化された IUnknown 派生型。 

[CreateTypedIntrinsicObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedintrinsicobject)

CreateTypedintrinsicObject メソッドは、CreateIntrinsicObject メソッド違うに似ています。これにより、ネイティブ/言語の型をデータに関連付けて、ボックス化された値と共に渡すことができます。 これにより、データモデルはネイティブの列挙型 (VT_UI 単に * 値または VT_I * 値) などの構造体を表すことができます。 ポインター型も、このメソッドを使用して作成されます。 データモデルのネイティブポインターは、デバッグターゲットの仮想アドレス空間へのオフセットを表す、ゼロの拡張64ビット数量です。 このメソッドは VT_UI8 内にボックス化され、このメソッドと、ネイティブ/言語ポインターを示す型を使用して作成されます。 

[CreateMetadataStore](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-createmetadatastore)

CreateMetadataStore メソッドは、キーストアを作成します。これは、キー/値/メタデータタプルの簡略化されたコンテナーです。これは、プロパティおよびその他のさまざまな値に関連付けることができるメタデータを保持するために使用されます。 メタデータストアには1つの親が存在する場合があります (この場合、1つの親を持つことができます)。 指定されたメタデータキーが特定のストアに存在しない場合は、その親がチェックされます。 ほとんどのメタデータストアには親がありません。 ただし、共通のメタデータを簡単に共有する方法を提供します。 

[CreateTypedIntrinsicObjectEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager2-createtypedintrinsicobjectex)

CreateTypedIntrinsicObjectEx メソッドは、意味的には CreateTypedIntrinsicObject メソッドに似ています。 2つの唯一の違いは、このメソッドでは、呼び出し元が組み込みデータが有効なコンテキストを指定できることです。 コンテキストが渡されない場合、データは、どのコンテキストが型引数から継承される場合でも有効と見なされます (CreateTypedIntrinsicObject の動作)。 これにより、型から継承できるよりも具体的なコンテキストを必要とする、型指定されたポインター値をデバッグターゲットで作成できます。 

**機能拡張/登録メソッド**次の一連のメソッドは、データモデルの機能拡張メカニズムを管理します。これにより、クライアントは既存のモデルを拡張または登録したり、特定の条件に一致するネイティブ型に特定の親モデルを自動的にアタッチするようにデータモデルに要求したりすることができます。

```cpp
    STDMETHOD(GetModelForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _Out_ IModelObject** dataModel) PURE;
    STDMETHOD(GetModelForType)(_In_ IDebugHostType* type, _COM_Outptr_ IModelObject** dataModel, _COM_Outptr_opt_ IDebugHostTypeSignature** typeSignature, _COM_Outptr_opt_ IDebugHostSymbolEnumerator** wildcardMatches) PURE;
    STDMETHOD(RegisterModelForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _In_ IModelObject* dataModel) PURE;
    STDMETHOD(UnregisterModelForTypeSignature)(_In_ IModelObject* dataModel, _In_opt_ IDebugHostTypeSignature* typeSignature) PURE;
    STDMETHOD(RegisterExtensionForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _In_ IModelObject* dataModel) PURE;
    STDMETHOD(UnregisterExtensionForTypeSignature)(_In_ IModelObject* dataModel, _In_opt_ IDebugHostTypeSignature* typeSignature) PURE;
    STDMETHOD(GetRootNamespace)(_COM_Outptr_ IModelObject** rootNamespace) PURE;
    STDMETHOD(RegisterNamedModel)(_In_ PCWSTR modelName, _In_ IModelObject *modeObject) PURE;
    STDMETHOD(UnregisterNamedModel)(_In_ PCWSTR modelName) PURE;
    STDMETHOD(AcquireNamedModel)(_In_ PCWSTR modelName, _COM_Outptr_ IModelObject **modelObject) PURE;
```

[GetModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-getmodelfortypesignature)

GetModelForTypeSignature メソッドは、以前の RegisterModelForTypeSignature メソッドの呼び出しによって特定の型シグネチャに対して登録されたデータモデルを返します。 このメソッドから返されるデータモデルは、渡された型シグネチャに一致する任意の型の正規ビジュアライザーと見なされます。 標準ビジュアライザーとして、そのデータモデルは、型の表示を引き継ぎます。 既定では、表示エンジンは、データモデルによって表示されるオブジェクトのビューを優先して、オブジェクトのネイティブ/言語構成要素を非表示にします。 


[GetModelForType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-getmodelfortype)

GetModelForType メソッドは、指定された型インスタンスの標準ビジュアライザーであるデータモデルを返します。 実際には、このメソッドは、RegisterModelForTypeSignature メソッドの前の呼び出しに登録された最も一致する型シグネチャを検索し、関連付けられたデータモデルを返します。 

[RegisterModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-registermodelfortypesignature)

RegisterModelForTypeSignature メソッドは、呼び出し元が特定の型 (または型のセット) の正規ビジュアライザーを登録するために使用する主要なメソッドです。 標準ビジュアライザーは、指定された型 (または型のセット) の表示を実質的に引き継ぐデータモデルです。 デバッガーのユーザーインターフェイスに表示されている型のネイティブ/言語ビューの代わりに、登録されたデータモデルによって示される型のビューが表示されます (と共に、そのユーザーを必要とするユーザーのネイティブ/言語ビューに戻ることができます)。 

[UnregisterModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-unregistermodelfortypesignature)

UnregisterModelForTypeSignature メソッドは、RegisterModelForTypeSignature メソッドの前の呼び出しを元に戻します。 このメソッドは、特定の型シグネチャに一致する型の正規ビジュアライザーとして指定されたデータモデルを削除することも、特定のデータモデルを、そのデータモデルが登録されているすべての型シグネチャの正規ビジュアライザーとして削除することもできます。 

[RegisterExtensionForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-registerextensionfortypesignature)

RegisterExtensionForTypeSignature メソッドは、RegisterModelForTypeSignature メソッドに似ていますが、主な違いが1つあります。 このメソッドに渡されるデータモデルは、どの型に対しても正規のビジュアライザーではなく、その型のネイティブ/言語ビューの表示には適用されません。 このメソッドに渡されるデータモデルは、指定された型シグネチャに一致する任意の具象型の親として自動的に追加されます。 RegisterModelForTypeSignature メソッドとは異なり、指定された型 (または型のセット) に対する拡張として登録されている同一またはあいまいな型シグネチャには制限がありません。 型シグネチャが特定の具象型のインスタンスと一致するすべての拡張機能は、このメソッドを介して登録されたデータモデルを、親モデルとして新しく作成されたオブジェクトに自動的にアタッチします。 これにより、任意の数のクライアントが、新しいフィールドまたは機能で型 (または型のセット) を拡張できるようになります。 

[UnregisterExtensionForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-unregisterextensionfortypesignature)

UnregisterExtensionForTypeSignature メソッドは、RegisterExtensionForTypeSignature の前の呼び出しを元に戻します。 特定のデータモデルを、特定の型シグネチャの拡張機能として、またはデータモデルが登録されたすべての型シグネチャの拡張として登録解除します。 

[GetRootNamespace](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-getrootnamespace)

GetRootNamespace メソッドは、データモデルのルート名前空間を返します。 これは、データモデルが管理し、デバッグホストが特定のオブジェクトを配置するオブジェクトです。

[RegisterNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager2-registernamedmodel)

RegisterNamedModel メソッドは、指定されたデータモデルを既知の名前で登録することで、それを拡張するクライアントによって検出されるようにします。 これは、API の主要な目的であり、この既知の名前で登録されたモデルを取得し、それに親モデルを追加することによって、データモデルを拡張可能なものとして公開します。 

[UnregisterNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager2-unregisternamedmodel)

UnregisterNamedModel メソッドは、RegisterNamedModel の前の呼び出しを元に戻します。 これにより、データモデルと、それを検索するための名前との間の関連付けが削除されます。

[AcquireNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager-acquirenamedmodel)

呼び出し元は、特定の名前で登録されているデータモデルを拡張する必要がある場合、拡張するデータモデルのオブジェクトを取得するために AcquireNamedModel メソッドを呼び出します。 このメソッドは、以前の RegisterNamedModel メソッドの呼び出しを介して登録されたすべてのデータモデルを返します。 AcquireNamedModel メソッドの主な目的はモデルを拡張することであるため、このメソッドは、指定された名前にまだモデルが登録されていない場合に特別な動作をします。 指定した名前でモデルが登録されていない場合は、スタブオブジェクトが作成され、指定された名前で一時的に登録され、呼び出し元に返されます。 RegisterNamedModel メソッドの呼び出しを使用して実際のデータモデルを登録すると、スタブオブジェクトに対して行われたすべての変更が実質的に実際のモデルに対して行われます。 これにより、互いに拡張されるコンポーネントから、多くの読み込み順序の依存関係の問題が除去されます。 

**ヘルパーメソッド**

次のメソッドは、データモデル内のオブジェクトに対して複雑な操作を実行する際に役立つ一般的なヘルパーメソッドです。 これらの操作は、データモデルまたはそのオブジェクトの他のメソッドを使用して実行できますが、これらの便利なメソッドを使用すると、はるかに簡単になります。 

```cpp
STDMETHOD(AcquireSubNamespace)(_In_ PCWSTR modelName, _In_ PCWSTR subNamespaceModelName, _In_ PCWSTR accessName, _In_opt_ IKeyStore *metadata, _COM_Outptr_ IModelObject **namespaceModelObject) PURE;
```

[AcquireSubNamespace](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelmanager2-acquiresubnamespace)

AcquireSubNamespace メソッドを使用すると、動的言語では、新しいオブジェクトよりも言語の名前空間に似ているようなものを構築できます。 たとえば、呼び出し元が process オブジェクトのプロパティを分類して、プロセスオブジェクトをより整理しやすくし、プロパティを簡単に検出できるようにするには、次の1つの方法として、process オブジェクトの各カテゴリに対してサブオブジェクトを作成し、そのオブジェクト内のこれらのプロパティ。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

このトピックでは、からC++アクセス可能なインターフェイスについて説明し、これらのインターフェイスを使用C++してベースのデバッガー拡張機能を構築する方法、およびC++データモデル拡張機能から他のデータモデル構造 (例: JavaScript または NatVis) を使用する方法について説明します。

[デバッガーデータモデルC++の概要](data-model-cpp-overview.md)

[デバッガーデータモデルC++のインターフェイス](data-model-cpp-interfaces.md)

[デバッガーデータモデルC++の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーデータモデルC++の概念](data-model-cpp-concepts.md)

[デバッガーデータモデルC++のスクリプト](data-model-cpp-scripting.md)
