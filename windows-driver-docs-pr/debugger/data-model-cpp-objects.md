---
title: デバッガーのデータ モデルの C++ オブジェクト
description: このトピックでは、デバッガーのデータ モデルの C++ オブジェクトを使用する方法と、デバッガーの機能を拡張する方法について説明します。
ms.date: 10/08/2018
ms.openlocfilehash: df747dd779761f71a07ec23085f991287c36f518
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550645"
---
# <a name="debugger-data-model-c-objects"></a>デバッガーのデータ モデルの C++ オブジェクト

このトピックでは、デバッガーのデータ モデルの C++ オブジェクトを使用する方法と、デバッガーの機能を拡張する方法について説明します。

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

[コア デバッガー オブジェクト モデル](#core)

[デバッガーのデータ モデルの中核となるオブジェクトの種類](#objecttypes)

[デバッガー データ モデルのマネージャー](#modelmanager)

---

## <a name="span-idcore--the-core-debugger-object-model"></a><span id="core">  コア デバッガー オブジェクト モデル

データ モデルの最も基本的かつ強力な点の 1 つは、どのようなオブジェクトおよびオブジェクトと対話するいずれかの方法の定義を標準化します。 そのことです。 *IModelObject*インターフェイスは、そのオブジェクトは、整数、浮動小数点値、文字列、デバッガーのターゲット アドレス空間にいくつかの複合型またはなどのいくつかのデバッガーの概念に--オブジェクトの概念をカプセル化しますプロセスまたはモジュールの概念です。

いくつかの異なる方法で保持されている (またはできるにボックス化)、 *IModelObject*:

-   **組み込まれている値**- *IModelObject*の基本的な種類のコンテナーを指定できます。8、16、32、または 64 ビット符号付きまたは符号なしの整数、ブール値、文字列、エラー、または空の概念です。

-   **ネイティブ オブジェクト**- *IModelObject*は複合型 (デバッガーの型システムで定義) されたデバッガーが対象とする任意のアドレス空間内 
    
-   **合成オブジェクト**- *IModelObject*場合は、動的オブジェクト--ディクショナリであることができます: キーのコレクション/値/メタデータの組と一連の**概念**動作を定義するします。単にキーによって表される/値のペア。

-   **プロパティ**- *IModelObject*プロパティを表すことができます。 何かの値を取得またはメソッドの呼び出しで変更されることができます。 内のプロパティ、 *IModelObject*は実質的には、 *IModelPropertyAccessor*にボックス化されたインターフェイス、 *IModelObject*

-   **メソッド**- *IModelObject*メソッドを表すことができます。 何かできるを呼び出し一連の引数と戻り値を取得します。 内のメソッド、 *IModelObject*は実質的には、 *IModelMethod*にボックス化されたインターフェイス、 *IModelObject*

### <a name="extensibility-within-the-object-model"></a>オブジェクト モデル内の機能拡張

*IModelObject*分離オブジェクトではありません。 上記のオブジェクトの種類のいずれかを表す、だけでなくは、各オブジェクトは、データ モデルの親のチェーンの概念を持ちます。 このチェーンの動作と同様、 [JavaScript プロトタイプ チェーン](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)します。
プロトタイプのリニア チェーンではなく JavaScript ように、各データ モデル オブジェクトを定義のリニア チェーン**モデルの親**します。 これらの親モデルのそれぞれは、親の set のもう 1 つのリニア チェーンにあります。 基本的には、各オブジェクトは、自体とこのツリーのすべてのオブジェクトの両方の機能 (プロパティなど) の集計が。 特定のプロパティを照会すると、クエリが実行オブジェクトがそのプロパティをサポートしていない場合は、ときに、クエリに渡されます線形な順序で各親順番。 これには、集計のツリーの深さ優先検索でプロパティの検索を解決する、動作が作成されます。

このオブジェクト モデル内の機能拡張は、すべてのオブジェクトがそれ自体の集計と親モデルのツリーがある概念を与え非常に単純です。 拡張機能にでき、自体の別のオブジェクトの親モデルの一覧に追加することができます。 これを行う**拡張**オブジェクト。 何も上に機能を追加することは、この方法で: オブジェクトまたは値、ネイティブ型、どのようなプロセスまたはスレッドのデバッガーの概念の特定のインスタンス、または「すべての反復可能なオブジェクト」の概念です。

### <a name="context-context-and-context-the-this-pointer-the-address-space-and-implementation-private-data"></a>コンテキスト、コンテキスト、およびコンテキスト:**この**ポインター、アドレス空間、および実装のプライベート データ

3 つの概念がある**コンテキスト**オブジェクト モデルのコンテキスト内で深く理解するために必要であります。

#### <a name="context-the-this-pointer"></a>コンテキスト:**この**ポインター

メソッドまたは元のオブジェクトにアクセスできるプロパティの実装に必要な特定のプロパティまたはメソッドは、データ モデルのツリーの任意のレベルで実装される場合があります、ため (と呼ばれるもの、**この**C++ でのポインターまたは**この**JavaScript のオブジェクト。 さまざまな方法を最初の引数としてにそのインスタンスのオブジェクトが渡されると呼ばれる**コンテキスト**で説明した方法でします。

#### <a name="context-the-address-space"></a>コンテキスト:アドレス空間

ことが重要以前の拡張機能とは異なり where をモデル化、**コンテキスト**(ターゲット、プロセス、スレッドが表示されている) 現在の UI に相対状態では、データのモデル インターフェイスは、通常はこのコンテキストすべての Api を使用した UI の概念明示的または暗黙的として、 *IDebugHostContext*インターフェイス。 各*IModelObject*モデル、データ内でこの種のコンテキスト情報と共に実行し、オブジェクトを返しますには、そのコンテキストを伝達することができます。 つまり、ネイティブの値またはキーの値を読み取るときに、 *IModelObject*ターゲットとオブジェクトを最初から取得したプロセスから読み取られます。

明示的な定数値がある**使用\_現在\_ホスト\_コンテキスト**、かかるメソッドに渡すこと、 *IDebugHostContext*引数。 この値は、コンテキストは実際にする必要があります、デバッガーの現在の UI 状態にすることを示します。 この概念は、ただし、明示的に指定する必要があります。

#### <a name="context-implementation-private-data"></a>コンテキスト:実装のプライベート データ

データ モデル内の各オブジェクトがオブジェクト インスタンスの集計では実際には、接続されている親モデルのツリーのことに注意してください。
インスタンスの任意のオブジェクトとその親モデル (これらを多数の異なるオブジェクトのチェーンでリンクできます) の各プライベートな実装のデータを関連付けることができます。 各*IModelObject*特定の親モデルからで定義されたプライベート インスタンス データにマップするハッシュ テーブルを概念的には作成されますが、 *IUnknown*インターフェイス。 これによりすべてのインスタンスで情報をキャッシュするか、それ以外の場合、親モデルを任意に関連付けデータ。

この種類のコンテキストは、 *GetContextForDataModel*と*SetContextForDataModel*メソッド*IModelObject*します。




## <a name="span-idimodelobjectspan-the-core-debugger-object-interface-imodelobject"></a><span id="imodelobject"></span> コア デバッガー オブジェクト インターフェイス:**IModelObject**

-------------------------------------------

*IModelObject*インターフェイスは次のように定義されます。

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

**基本的な方法**

次に、IModelObject によって表されるオブジェクトの任意の種類に該当する一般的な方法を示します。 

```cpp
STDMETHOD(GetKind)(_Out_ ModelObjectKind *kind) PURE;
STDMETHOD(GetContext)(_COM_Outptr_result_maybenull_ IDebugHostContext** context) PURE;
STDMETHOD(GetIntrinsicValue)(_Out_ VARIANT* intrinsicData);
STDMETHOD(GetIntrinsicValueAs)(_In_ VARTYPE vt, _Out_ VARIANT* intrinsicData) PURE;
STDMETHOD(Compare)(_In_ IModelObject* other, _COM_Outptr_opt_result_maybenull_ IModelObject **ppResult) PURE;
STDMETHOD(IsEqualTo)(_In_ IModelObject* other, _Out_ bool* equal) PURE;
STDMETHOD(Dereference)(_COM_Errorptr_ IModelObject** object) PURE;
```

[GetKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkind) 

GetKind メソッドは、IModelObject 内でどのような種類のオブジェクトがボックス化を返します。 

[GetContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getcontext)

GetContext メソッドは、オブジェクトに関連付けられているホスト コンテキストを返します。 

[GetIntrinsicValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getintrinsicvalue)

GetIntrinsicValue メソッドは、IModelObject 内をボックス化することを返します。 このメソッドは、IModelObject インターフェイスを表すボックス化された合法的にのみ呼び出すことが組み込みまたはボックス化されますが、特定のインターフェイス。 ネイティブ オブジェクト、値のないオブジェクトには、合成のオブジェクトで呼び出すことはできませんし、オブジェクトを参照します。 GetIntrinsicValueAs メソッドは、後、例外を GetIntrinsicValue メソッドが値に変換指定されたバリアント型と同様に動作します。 変換を実行できない場合、メソッドはエラーを返します。

[IsEqualTo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-isequalto)

IsEqualTo メソッドでは、2 つのモデル オブジェクトを比較し、値が等しいかどうかを返します。 順序付けと、オブジェクト、true を返すこのメソッドは、0 を返す Compare メソッドと同じです。 順序付けありませんが、等値性をオブジェクトの場合、Compare メソッドは失敗するが動作しません。 値に基づく比較の意味は、オブジェクトの型によって定義されます。 現時点ではこれのみ、組み込み型とエラー オブジェクトに定義されます。 Equatability の現在のデータ モデルの概念はありません。 

[逆参照します。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-dereference)

逆参照するメソッドには、オブジェクトが逆参照します。 このメソッドは、データ モデルの参照 (ObjectTargetObjectReference、ObjectKeyReference) またはネイティブ言語リファレンス (ポインターまたは言語リファレンス) を逆参照に使用できます。 このメソッドが、オブジェクトに対する参照セマンティクスの 1 つのレベルを削除することに注意してください。 重要です。 たとえば、言語リファレンスへのデータ モデル参照を含めることは可能になります。 このような場合は、初めて逆参照メソッドを呼び出すことはデータ モデル参照を削除し、言語リファレンスのままに。 その結果として得られるオブジェクトの逆参照を呼び出すことは、その後言語参照を削除し、下を参照するネイティブの値を返します。 


**キー操作メソッド**

キー、値、およびメタデータの組のディクショナリである任意の合成オブジェクトが、一連のこれらのキー、値、およびそれらに関連付けられているメタデータを操作するメソッド。 

Api のベース値フォームは次のとおりです。 

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

Api のベース参照の形式は次のとおりです。 

```cpp
STDMETHOD(GetKeyReference)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** objectReference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
STDMETHOD(EnumerateKeyReferences)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
```

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkeyvalue)

GetKeyValue メソッドの値 (とそれに関連付けられているメタデータ) を取得するために、クライアントを有効にする最初のメソッドは、名前によって指定されたキー。 キーは、その値をこれはボックス化された IModelPropertyAccessor IModelObject としては、プロパティのアクセサー--GetKeyValue メソッドは、実際の値を取得するためにプロパティ アクセサーの GetValue メソッドを呼び出す自動的にします。

[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setkeyvalue)

SetKeyValue メソッドは、キーの値を設定するには、クライアントを有効にする最初の方法です。 このメソッドは、オブジェクトに新しいキーを作成するのには使用できません。 既存のキーの値のみ設定されます。 多くのキーには読み取り専用に注意してください (例:: E_NOT_IMPL を SetValue メソッドから返すプロパティのアクセサーによって実装されます)。 このメソッドが呼び出されたときに、読み取り時のみキーは失敗します。 

[EnumerateKeyValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeyvalues)

EnumerateKeyValues メソッドは、クライアントは (親モデルのツリーで任意の場所に実装されているすべてのキーを含む)、オブジェクトのキーのすべてを列挙するために有効にする最初の方法です。 EnumerateKeyValues がオブジェクト ツリーで重複する名前で定義されたすべてのキーを列挙ことに注意してください。ただし--深さ優先検査により検出された、GetKeyValue と SetKeyValue などのメソッドは指定した名前のキーの最初のインスタンスを操作のみです。 

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkey)

GetKey メソッドの値が取得されます (とメタデータに関連付けられている) 名で指定されたキー。 ほとんどのクライアントは、代わりに GetKeyValue メソッドを使用する必要があります。 キーは、プロパティ アクセサーは、このメソッドを呼び出すことは、IModelObject にボックス化されたプロパティのアクセサー (IModelPropertyAccessor インターフェイス) を返します。 異なり、GetKeyValue、GetValue メソッドを呼び出すことによって、キーの基になる値がこのメソッドに自動的に解決されることはできません。 その役割、呼び出し元のことです。 

[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setkey)

SetKey メソッドは、クライアント メソッドを (と可能性のあるメタデータを作成したキーに関連付ける) オブジェクトにキーを作成するためになります。 指定したオブジェクトが既に指定した名前のキーを使用して、2 つの動作のいずれかが発生します。 これによって指定されたインスタンスにキーがある場合、元のキーが存在しなかった場合、そのキーの値が置き換えられます。 その一方で、キーがこので指定されたインスタンスのデータ モデルの親のチェーンにある場合、指定した名前の新しいキーがこので指定されたインスタンスで作成されます。 これを実際が原因で、オブジェクトが、同じ名前 (基本クラスと同じ名前のメンバーをシャドウする派生クラスに似ています) の 2 つのキー。 

[EnumerateKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeys)

EnumerateKeys メソッドの動作オブジェクトのプロパティ アクセサーが自動的に解決できないドキュメントを除く EnumerateKeyValues メソッドに似ています。 つまり、キーの値がプロパティのアクセサーの場合は、EnumerateKeys メソッドによって、プロパティ アクセサー (IModelPropertyAccessorInterface、) GetValue メソッドを自動的に呼び出すのではなく、IModelObject にボックス化返すされます。 これは、GetKey と GetKeyValue の違いに似ています。 

[ClearKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-clearkeys)

ClearKeys メソッドは、こので指定されたオブジェクトのインスタンスからすべてのキーおよび関連付けられている値とメタデータを削除します。 このメソッドは、特定のオブジェクトのインスタンスに接続されている親モデルに影響を与えません。 

[GetKeyReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkeyreference)

GetKeyReference メソッドは、オブジェクト (またはその親モデルのチェーン) に指定した名前のキーを検索して、IModelObject にボックス化 IModelKeyReference インターフェイスで指定されたキーへの参照を返します。 その参照は、キーの値の設定を取得または後で使用できます。 

[EnumerateKeyReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeyreferences)

EnumerateKeyReferences メソッドの動作、キーの値ではなく (、IModelObject にボックス化 IModelKeyReference インターフェイスで指定) が列挙キーへの参照が返されるドキュメントを除く EnumerateKeyValues メソッドに似ています。 このような参照を取得またはキーの基になる値を設定するができます。 


**操作方法の概念**

メタデータ/キー/値のタプルのディクショナリをされているモデル オブジェクト、に加えても概念のコンテナー。 概念は抽象オブジェクトでまたはを実行できます。 概念は基本的には、オブジェクトをサポートするインターフェイスの動的なストアです。 さまざまな概念は、現在のデータ モデルで定義されます。 

インターフェイスの概念 | 説明
------------------|-------------
IDataModelConcept | 概念は、親モデルです。 このモデルは自動的に登録されているタイプの署名を使用してネイティブ型にアタッチされている、このような種類の新しいオブジェクトがインスタンス化されるたびに、InitializeObject メソッドが呼び出さ自動的にします。
IStringDisplayableConcept  | オブジェクトは、表示目的での文字列に変換できます。
IIterableConcept  | オブジェクトはコンテナーであり、反復処理されることができます。
IIndexableConcept  | オブジェクトはコンテナーであり、インデックスを作成できます (ランダム アクセスを使用してアクセスされる) 1 つまたは複数のディメンションでします。
IPreferredRuntimeTypeConcept  | オブジェクトでは、基になる型システムが提供することのできると、ランタイム型を静的から独自の変換を処理するよりも、それから派生した種類の詳細については理解します。
IDynamicKeyProviderConcept | オブジェクトは、動的なキーのプロバイダーであり、コア データ モデルからのすべてのキー クエリを実行したいです。 このインターフェイスは通常、JavaScript などの動的言語へのブリッジとして使用します。
IDynamicConceptProviderConcept  | オブジェクトは概念の動的なプロバイダーであり、コア データ モデルからすべての概念のクエリを実行したいです。 このインターフェイスは通常、JavaScript などの動的言語へのブリッジとして使用します。

IModelObject で次のメソッドを使用して、オブジェクトをサポートする概念を操作します。 

```cpp
STDMETHOD(GetConcept)(_In_ REFIID conceptId, _COM_Outptr_ IUnknown** conceptInterface, _COM_Outptr_opt_result_maybenull_ IKeyStore** conceptMetadata) PURE;
STDMETHOD(SetConcept)(_In_ REFIID conceptId, _In_ IUnknown* conceptInterface, _In_opt_ IKeyStore* conceptMetadata) PURE;
STDMETHOD(ClearConcepts)() PURE;
```

[GetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getconcept)

GetConcept メソッドでは、オブジェクト (またはその親モデルのチェーン) 上の概念を検索し、概念インターフェイスにインターフェイス ポインターを返します。 動作と概念のインターフェイスのメソッドは、各概念に固有です。 ただし、必要なコンテキスト オブジェクトを明示的に渡す呼び出し元が概念インターフェイスの多くすることが重要 (どのような 1 つ呼び出すことができます従来、このまたはポインター)。 すべての概念のインターフェイスを適切なコンテキスト オブジェクトが渡されることを確認する重要です。

[SetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setconcept)

SetConcept メソッドでは、指定された概念は、これによって指定されたオブジェクトのインスタンスに配置のポインター。 これで指定されたオブジェクトのインスタンスに接続されている親モデルは、概念をサポートしても、インスタンス内の実装が上書きを親モデル。 

[ClearConcepts](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-clearconcepts)

ClearConcepts メソッドは、すべての概念をこので指定されたオブジェクトのインスタンスから削除されます。 


**ネイティブ オブジェクトのメソッド**

中に、多くのモデル オブジェクトは、組み込み関数を参照してください (例:: 整数、文字列) または統合は、(キー/値/メタデータの組と概念の辞書) を構築、モデル オブジェクトのネイティブ コンストラクトに可能性がありますも参照してください (例:: デバッグのアドレス空間内のユーザー定義型ターゲットの場合)。 IModelObject インターフェイスには、一連のようなネイティブ オブジェクトに関する情報にアクセスすることでメソッドがあります。 これらのメソッドは次のとおりです。 

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

[GetRawValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getrawvalue)

GetRawValue メソッドは、特定のオブジェクト内でネイティブの構造を検索します。 このようなコンス トラクターには、フィールド、基底クラス、基底クラス、メンバー関数などのフィールドがあります. 

[EnumerateRawValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeraterawvalues)

EnumerateRawValues メソッドは、ネイティブのすべての子を列挙します (例:: フィールド、基底クラスなど) の指定したオブジェクト。 


[TryCastToRuntimeType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-trycasttoruntimetype)

TryCastToRuntimeType メソッドは、分析を実行し、実際の実行時の種類を特定のデバッグ ホストを求められます (例:: 最も派生クラス) の指定したオブジェクト。 オブジェクト、またはその他の V Table(virtual function table) 構造を調べることで、ホスト使用率の正確な分析はデバッグ ホストに固有であり RTTI (C++ の実行時型情報) を含めることができます、使用して動的/ランタイムを確実に決定できます静的な型から入力します。 ランタイム型に変換する障害では、このメソッドの呼び出しが失敗するとは限りません。 このような場合、メソッドは、指定したオブジェクトを返します (、このポインター) の出力引数。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getlocation) 

GetLocation メソッドでは、ネイティブ オブジェクトの場所を返します。 このような場所は通常、デバッグ対象のアドレス空間内の仮想アドレスが、必ずしもそうです。 このメソッドによって返される場所は、抽象場所は、仮想のアドレスがあります、登録またはサブレジスタ、内の位置を示す場合がありますまたはデバッグ ホストで定義されているその他の任意のアドレス空間の一部を示す場合があります。 結果として得られる場所オブジェクトの HostDefined フィールドが 0 の場合は、場所が実際には仮想アドレスを示します。 このような仮想アドレスを結果の場所のオフセット フィールドを調べることで取得できます。 HostDefined フィールドの 0 以外の値では、オフセット フィールドがそのアドレス空間内のオフセットを別のアドレス空間を示します。 ここで HostDefined 値が 0 以外の厳密な意味は、デバッグ ホストにプライベートです。 

[GetTypeInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-gettypeinfo)

GetTypeInfo メソッドでは、指定したオブジェクトのネイティブな型を返します。 オブジェクトが関連付けられているネイティブの型情報を持たないかどうか (例:: は、組み込みなど...)、呼び出しがまだは成功しますが、null が返されます。 

[GetTargetInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-gettargetinfo)

GetTargetInfo メソッドは、実質的に、両方の抽象場所だけでなく、指定したオブジェクトのネイティブな型を返す GetLocation と GetTypeInfo メソッドの組み合わせです。 

[GetRawReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getrawreference)

GetRawReference メソッドは、特定のオブジェクト内でネイティブの構造を検索してへの参照を返します。 このようなコンス トラクターには、フィールド、基底クラス、基底クラス、メンバー関数などのフィールドがあります.言語リファレンスからここ (ObjectTargetObjectReference 型のオブジェクト) に返される参照を区別するために重要です (例:: C++ & または (& a) (& a) スタイルの参照)。 

[EnumerateRawReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeraterawreferences)

EnumerateRawReferences メソッドは、ネイティブのすべての子への参照を列挙します (例:: フィールド、基底クラスなど) の指定したオブジェクト。 


**拡張メソッド**

前述のように、モデル オブジェクトは JavaScript オブジェクトとプロトタイプ チェーンによく似ていますは動作します。 指定された IModelObject インターフェイスによって表されるインスタンスに加えて、任意の数 (それぞれの必要があります、さらに、任意の数が割り当てられている親モデルの) オブジェクトにアタッチされている親モデルの可能性があります。 これは、データ モデル内の機能拡張の主要な手段です。 特定のプロパティ、または概念には、特定のインスタンス内に存在することはできません、インスタンスで root 化 (親モデルによって定義される)、オブジェクト ツリーの深さ優先の検索が実行されます。 

次のメソッドは操作 IModelObject インスタンスに関連付けられている親モデルのチェーンです。 

```cpp
STDMETHOD(GetNumberOfParentModels)(_Out_ ULONG64* numModels) PURE;
STDMETHOD(GetParentModel)(_In_ ULONG64 i, _COM_Outptr_ IModelObject **model, _COM_Outptr_result_maybenull_ IModelObject **contextObject) PURE;
STDMETHOD(AddParentModel)(_In_ IModelObject* model, _In_opt_ IModelObject* contextObject, _In_ bool override) PURE;
STDMETHOD(RemoveParentModel)(_In_ IModelObject* model) PURE;
STDMETHOD(SetContextForDataModel)(_In_ IModelObject* dataModelObject, _In_ IUnknown* context) PURE;
STDMETHOD(GetContextForDataModel)(_In_ IModelObject* dataModelObject, _Out_ IUnknown** context) PURE;
```

[GetNumberOfParentModels](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getnumberofparentmodels)

GetNumberOfParentModels メソッドは、指定したオブジェクトのインスタンスに接続されている親モデルの数を返します。 親モデルでは、モデルの親チェインの順序付けの線形の深さ優先のプロパティが検索されます。 

[GetParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getparentmodel)

GetParentModel メソッドは、指定したオブジェクトの親モデルのチェーンに、i 番目の親モデルを返します。 親モデルは、プロパティ、または概念が追加または列挙線形な順序で検索されます。 インデックス i+1 の親モデルする前に (階層) では、インデックス i が 0 の親モデルが検索されます。 

[AddParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-addparentmodel)

AddParentModel メソッドでは、指定したオブジェクトを新しい親モデルを追加します。 (オーバーライド引数が false として指定された) 検索チェーンの最後に、または (オーバーライド引数が true として指定された) 検索チェーンの先頭にある、このようなモデルを追加することがあります。 さらに、各親モデルは、コンテキスト必要に応じて調整 (セマンティック this ポインター) の任意のプロパティまたは指定した親 (またはその親階層内のすべてのユーザー) の概念です。 コンテキストの調整では、めったに使用が可能オブジェクトを埋め込むなどのいくつかの強力な概念など、名前空間を作成する. 

[RemoveParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-removeparentmodel)

RemoveParentModel は、指定した親モデルを指定したオブジェクトの親の検索のチェーンから削除されます。 

[SetContextForDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setcontextfordatamodel)

SetContextForDataModel メソッドは、インスタンス オブジェクトの実装のデータを配置するデータ モデルの実装によって使用されます。 概念的には、各 IModelObject (主役インスタンスわかりやすくするため) の状態のハッシュ テーブルが含まれています。 ハッシュ テーブルはインスタンスの親モデル階層内にある別の IModelObject (わかりやすくするためにこのデータをモデルの呼び出し) でインデックスを作成します。 このハッシュに含まれている値は、IUnknown インスタンスによって表される状態情報をカウントされた参照のセットです。 データ モデルでは、プロパティ get アクセス操作子などの中に取得できる任意の実装のデータを格納するインスタンスをこの状態を設定します。 

[GetContextForDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getcontextfordatamodel)

GetContextForDataModel メソッドを使用して、SetContextForDataModel を呼び出す前に設定されたコンテキスト情報を取得します。 データ モデルによって、インスタンス オブジェクトに設定されている状態情報を取得するインスタンス オブジェクトの親モデル階層内でさらにします。 このコンテキストの/状態とその意味の詳細については、SetContextForDataModel のマニュアルを参照してください。 




## <a name="span-idobjecttypesspan-debugger-data-model-core-object-types"></a><span id="objecttypes"></span> デバッガーのデータ モデルの中核となるオブジェクトの種類


データ モデル内のオブジェクトは、オブジェクトを .NET での概念に似ています。 これは、データ モデルを理解する構成要素のボックス化を汎用コンテナーです。 ネイティブ オブジェクトと代理 (動的) オブジェクトに加え、一連の配置 (またはボックス化)、IModelObject のコンテナーに中核となるオブジェクトの種類があります。 これらの値のほとんどの配置のコンテナーは、そのバリアントに含めることができますに対して COM/OLE VARIANT 追加の制限の数が適用される標準です。 これらの最も基本的な種類があります。

- 8 ビット符号なしと署名値 (VT_UI1、VT_I1)
- 16 ビット符号なしと署名値 (VT_UI2、VT_UI2)
- 32 ビット符号なしと署名値 (VT_UI4、VT_I4)
- 64 ビット符号なしと署名値 (VT_UI8、VT_I8)
- 一重引用符と二重の単精度浮動小数点値 (VT_R4、VT_R8)
- 文字列 (VT_BSTR)
- ブール値 (VT_BOOL)

だけでなく、これらの基本的な型は、複数のコア データ モデル オブジェクトは IModelObject ストアド IUnknown が特定のインターフェイスを実装するために保証されて VT_UNKNOWN によって定義されたに配置されます。 これらの型は次のとおりです。 

- プロパティ アクセサー (IModelPropertyAccessor)
- メソッドのオブジェクト (IModelMethod)
- キー参照オブジェクト (IModelKeyReference または IModelKeyReference2)
- コンテキスト オブジェクト (IDebugModelHostContext)

**プロパティ アクセサー。*IModelPropertyAccessor***

データ モデルのプロパティのアクセサーは、IModelObject にボックス化 IModelPropertyAccessor インターフェイスの実装です。 モデル オブジェクトは戻ります ObjectPropertyAccessor 照会されたときの一種で、組み込みの値は IModelPropertyAccessor のクエリを実行することが保証される VT_UNKNOWN です。 プロセスでは、IModelPropertyAccessor を静的にキャストできるに保証されます。 

プロパティ アクセサーは、取得、およびデータ モデルにキー値を設定するためのメソッドの呼び出しを取得する間接的な方法です。 指定されたキーの値がプロパティのアクセサーの場合は、GetKeyValue と SetKeyValue メソッドは自動的にこれを通知し、プロパティ アクセサーの基になるか、GetValue と SetValue は適切なメソッドを呼び出します。 

IModelPropertyAccessor インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IModelPropertyAccessor, IUnknown)
{
    STDMETHOD(GetValue)(_In_ PCWSTR key, _In_opt_ IModelObject* contextObject, _COM_Outptr_ IModelObject** value) PURE;
    STDMETHOD(SetValue)(_In_ PCWSTR key, _In_opt_ IModelObject* contextObject, _In_ IModelObject* value) PURE; 
}
```

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelpropertyaccessor-getvalue)

GetValue メソッドは、プロパティ アクセサーを取得します。 クライアントが基になるプロパティの値をフェッチする必要があるたびに呼び出されます。 プロパティ アクセサーを直接取得する呼び出し元が、キー名と正確なインスタンス オブジェクト (このポインター) をプロパティ アクセサーの GetValue メソッドに渡す責任を負うことに注意してください。 

[SetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelpropertyaccessor-setvalue)

SetValue メソッドは、プロパティ アクセサーの set アクセス操作子です。 クライアントが、基になるプロパティに値を代入するときに呼び出されます。 多くのプロパティとは、読み取り専用です。 SetValue メソッドを呼び出すことと、このような場合は E_NOTIMPL を返されます。 プロパティ アクセサーを直接取得する呼び出し元が、キー名と正確なインスタンス オブジェクト (このポインター) をプロパティ アクセサーの SetValue メソッドに渡す責任を負うことに注意してください。 


**方法:*IModelMethod***

データ モデル内のメソッドは、IModelObject にボックス化 IModelMethod インターフェイスの実装です。 モデル オブジェクトは戻ります ObjectMethod 照会されたときの一種で、組み込みの値は IModelMethod のクエリを実行することが保証される VT_UNKNOWN です。 プロセスでは、IModelMethod を静的にキャストできるに保証されます。 データ モデルのすべてのメソッドは動的に変化します。 受け取るとして 0 または複数の引数のセットを入力し、1 つの出力値を返します。 オーバー ロード解決策はありません、パラメーター名、型、または期待に関するメタデータがありません。 

IModelMethod インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IModelMethod, IUnknown)
{
    STDMETHOD(Call)(_In_opt_ IModelObject *pContextObject, _In_ ULONG64 argCount, _In_reads_(argCount) IModelObject **ppArguments, _COM_Errorptr_ IModelObject **ppResult, _COM_Outptr_opt_result_maybenull_ IKeyStore **ppMetadata) PURE;
}
```

[呼び出し](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelmethod-call)

Call メソッドは、モデル データで定義されたどのメソッドが呼び出される方法です。 呼び出し元が、正確なインスタンス オブジェクト (このポインター) と任意の一連の引数を渡す責任を負います。 メソッドとその結果に関連付けられた任意の省略可能なメタデータの結果が返されます。 まだを論理的に値を返さないメソッドは、有効な IModelObject を返す必要があります。 このような場合も、IModelObject はボックス化された値はありません。 メソッドが失敗すると、イベント (返された HRESULT は、失敗した) 場合でも、入力引数の省略可能なエラーの詳細情報を返すこと可能性があります。 この呼び出し元を確認することが不可欠です。 


**キーの参照。*IModelKeyReference または IModelKeyReference2***

キー参照は基本的には、特定のオブジェクトのキーを識別するハンドルです。 クライアントでは、GetKeyReference などのメソッドを使用してこのようなハンドルを取得でき、後で取得または必ずしも元のオブジェクトに保持することがなくキーの値を設定するハンドルを使用することができます。 この種類のオブジェクトは、IModelObject にボックス化 IModelKeyReference または IModelKeyReference2 インターフェイスの実装です。 モデル オブジェクトはある種の照会されたときに ObjectKeyReference を返し、IModelKeyReference のクエリを実行することが保証される VT_UNKNOWN 固有の値になります。 プロセスでは、IModelKeyReference を静的にキャストできるに保証されます。 

キー参照インターフェイスの定義は次のとおりです。 

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

[GetKeyName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getkeyname)

られてメソッドは、このキーの参照がハンドルをキーの名前を返します。 返される文字列は、標準の BSTR で SysFreeString への呼び出しを使用して解放する必要があります。 

[GetOriginalObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getoriginalobject)

GetOriginalObject メソッドは、キー参照の作成元となるインスタンス オブジェクトを返します。 可能性のある、キー自体では、インスタンス オブジェクトの親モデルに注意してください。 

[GetContextObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getcontextobject)

GetContextObject メソッドは、対象のキー プロパティのアクセサーを指す場合、プロパティ アクセサーの GetValue または SetValue メソッドに渡されるコンテキスト (このポインター) を返します。 ここで返されるコンテキスト オブジェクトは、可能性があります。 または GetOriginalObject からフェッチされた元のオブジェクトと同じである可能性がありますされません。 キーは、親モデルの場合に、コンテキスト清算人がその親モデルに関連付けられている場合は、元のオブジェクト、GetKeyReference または EnumerateKeyReferences が呼び出されたインスタンス オブジェクトです。 コンテキスト オブジェクトは、元のオブジェクトとキーをこのキーの参照を識別するハンドルを含む親モデルの最終的なコンテキスト清算人から来るでしょう。 コンテキストの査定がない場合は、元のオブジェクトとコンテキスト オブジェクトは同じです。 

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getkey)

GetKey メソッドは、キー参照は、IModelObject GetKey メソッドと同様に動作します。 基になるキーとキーに関連付けられたメタデータの値を返します。 キーの値は、プロパティ アクセサーを使用する場合に、これは、IModelObject にボックス化 (IModelPropertyAccessor) プロパティのアクセサーを返します。 このメソッドはプロパティのアクセサーに、基になる GetValue メソッドまたは SetValue メソッドを呼び出しません。 

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getkeyvalue)

IModelObject GetKeyValue メソッドと同様、キー参照で GetKeyValue メソッドの動作はします。 基になるキーとキーに関連付けられたメタデータの値を返します。 キーの値は、プロパティ アクセサーを使用する場合に、この基になる GetValue メソッド プロパティのアクセサーに自動的に呼び出します。 


[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-setkey)

IModelObject SetKey メソッドと同様、キー参照で SetKey メソッドの動作はします。 これにより、キーの値が割り当てられます。 元のキーがプロパティのアクセサーの場合は、このプロパティのアクセサーは置き換えられます。 プロパティのアクセサーに SetValue メソッドを呼び出すことができません。 


[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-setkeyvalue)

IModelObject SetKeyValue メソッドと同様、キー参照で SetKeyValue メソッドの動作はします。 これにより、キーの値が割り当てられます。 元のキーがプロパティのアクセサーの場合は、このプロパティのアクセサー自体を置き換えるのではなく、プロパティ アクセサーに基になる SetValue メソッドを呼び出します。 

[OverrideContextObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference2-overridecontextobject)

OverrideContextObject メソッド (IModelKeyReference2 にのみ存在する) は、永久的にこのキーの参照が、基になるプロパティ アクセサーの GetValue または SetValue メソッドに渡すコンテキスト オブジェクトを変更するために使用する高度な方法です。 このメソッドに渡されるオブジェクトが、GetContextObject への呼び出しからも返されます。 このメソッドは、特定の動的言語の動作をレプリケートするスクリプトのプロバイダーで使用できます。 ほとんどのクライアントは、このメソッドを呼び出さないでください。 


**コンテキスト オブジェクト。*IDebugHostContext***

コンテキスト オブジェクトは、すべてのオブジェクトに関連付けます (データ モデルとの連携) でのデバッグ ホスト情報の非透過 blob です。 情報は、プロセスのコンテキストまたはアドレス空間などなどの可能性があります.コンテキスト オブジェクトは、IDebugHostContext、IModelObject 内にボックス化の実装です。 IDebugHostContext が定義されているホスト インターフェイスであることに注意してください。 クライアントは、このインターフェイスを実装しないされます。 

コンテキスト オブジェクトの詳細については、[デバッガー データ モデルの C++ ホスト インターフェイス](data-model-cpp-interfaces.md#hostinterface)デバッガー データ モデルの C++ インターフェイスにを参照してください。 


## <a name="span-idmodelmanager-the-data-model-manager"></a><span id="modelmanager"> データ モデルのマネージャー  

データ モデル マネージャー、IDataModelManager2 (またはそれ以前の IDataModelManager) に、主要なインターフェイスの定義は次のとおりです。 

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

次の一連のメソッドが、アプリケーションで使用される (例:: デバッガー)、データ モデルをホストしています。 

```cpp
STDMETHOD(Close)() PURE;
```

[閉じる](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-close)

アプリケーションでデータ モデルのマネージャーの Close メソッドが呼び出されます (例:: デバッガー)、データ モデルのマネージャーのシャット ダウン プロセスを開始するには、データ モデルをホストします。 データ モデルのマネージャーの最終的な参照を解放する前に閉じるメソッドではなく、データ モデルのホストでは、未定義の動作を含む、発生する可能性がありますが、データ モデルの管理インフラストラクチャの重要なリークに限定されません。 

**オブジェクトの作成]、[メソッドのボックス化**

次の一連のメソッドを使用して新しいオブジェクトを作成または、IModelObject - データ モデルの中核となるインターフェイスにボックスの値にします。 

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

[CreateNoValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createnovalue)

CreateNoValue メソッドは、"no value"オブジェクトを作成し、IModelObject にボックスに、それを返します。 返されたモデル オブジェクトには、ある種の ObjectNoValue があります。 

"No value"のオブジェクトには、いくつかのセマンティックな意味があります。 

- (言語) に応じて、見なすことができます、void 型、null または未定義の意味と同じ
- 特定のプロパティは、指定されたインスタンスの値がないと、特定のインスタンスのプロパティが存在しなかったかのように扱う必要がある成功し、結果として"no value"のオブジェクトを返すすべてプロパティ アクセサーの GetValue メソッドを示すです。
- データ モデルのメソッド戻り値を意味がない場合がこれを使用して sentinel としてなどを示します (など、メソッドは、有効な IModelObject を返す必要があります)。

[CreateErrorObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createerrorobject)

CreateErrorObject メソッドは、"error"オブジェクトを作成します。 データ モデルには、例外と例外のフローの概念はありません。 2 つの方法でプロパティまたはメソッドは失敗します。

- 1 つの HRESULT を拡張エラー情報なしで失敗します。 以上のエラーのある情報があるか、またはエラー自体が返された HRESULT から見ればすぐにわかります。
- HRESULT を組み合わせて 1 つの障害は拡張エラー情報です。 拡張エラー情報は、プロパティまたはメソッドの出力引数で返されるエラー オブジェクトです。

[CreateTypedObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedobject)

CreateTypedObject メソッドは、これにより、クライアントは、デバッグ対象のアドレス空間でネイティブ/言語のオブジェクトの表現を作成する方法です。 自動的にはデータ モデルに一致するもの (objectType 引数によって示されます) として新しく作成されたオブジェクトの種類は、正規のビジュアライザーまたは拡張機能のいずれかとして、データ モデルのマネージャーに登録されている 1 つまたは複数の型シグネチャに一致する場合に、呼び出し元に返される前に作成されたインスタンスのオブジェクトにアタッチされます。 

[CreateTypedObjectReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedobjectreference)

CreateTypedObjectReference メソッドは、基になるネイティブ/言語構成要素への参照を作成後、例外、CreateTypedObject メソッドに意味的に似ています。 作成した参照は、ある種の ObjectTargetObjectReference のあるオブジェクトです。 ネイティブの参照を基になる言語をサポート可能性があります (例: C++ & または (& a) (& a))。 C++ 参照の ObjectTargetObjectReference が可能になります。 Kind ObjectTargetObjectReference のオブジェクトは、IModelObject の逆参照メソッドを使用して基になる値に変換できます。 バックを割り当てるには、参照が、基になるホストの式エバリュエーターに渡すこともできますように適切な言語の値にします。 

[CreateSyntheticObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createsyntheticobject)

CreateSyntheticObject メソッドは、空のデータ モデル オブジェクト - メタデータ/キー/値のタプルと概念のディクショナリを作成します。 作成時にがないキーも、オブジェクトの概念です。 利用する、呼び出し元のクリーンな状態になります。 

[CreateDataModelObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createdatamodelobject)

CreateDataModelObject メソッドは、その他のオブジェクトへの親モデルとして接続しようとしているオブジェクトであるデータ モデルであるオブジェクトを作成する簡単なヘルパー ラッパーです。 このようなすべてのオブジェクトには、IDataModelConcept 経由でデータ モデルの概念をサポートする必要があります。 このメソッドは、明示的なコンテキストなしで新しい空白の合成オブジェクトを作成し、データ モデルの概念を新しく作成されたオブジェクトの実装として inpassed IDataModelConcept を追加します。 これは、CreateSyntheticObject および SetConcept への呼び出しと同様に実現できます。 

[CreateIntrinsicObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createintrinsicobject)

CreateIntrinsicObject メソッドは、値が組み込み IModelObject にボックス化する方法です。 呼び出し元は COM バリアント型の値が配置され、このメソッドを呼び出します。 データ モデルのマネージャーは、オブジェクトを表す、IModelObject を返します。 このメソッドは、基本的な IUnknown ベース型のボックスを使用しても: プロパティ アクセサー、メソッド、コンテキストなどしています.このような場合は、objectKind メソッドは、IUnknown ベースの種類、オブジェクトの構築を表し、渡された variant punkVal フィールドは、IUnknown の派生型を示します。 モデルの適切なインターフェイスに静的にキャストできる型でなければなりません (例。IModelPropertyAccessor、IModelMethod、IDebugHostContext..)。で処理します。 このメソッドでサポートされている VARIANT 型、VT_UI1、VT_I1、VT_UI2、VT_I2、VT_UI4、VT_I4、VT_UI8、VT_I8、VT_R4、VT_R8、VT_BOOL、VT_BSTR、および VT_UNKNOWN (ModelObjectKind 列挙体によって示されるように IUnknown の派生型の特殊なセット。 

[CreateTypedIntrinsicObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedintrinsicobject)

CreateTypedintrinsicObject メソッドは、ネイティブ/言語の種類のデータに関連付けられているし、ボックス化された値に付随することができるドキュメントを除く、CreateIntrinsicObject メソッドに似ています。 これにより、(これは、単に VT_UI * または VT_I * 値) のネイティブ列挙型などの構造を表すデータ モデルです。 ポインター型は、このメソッドを使用しても作成されます。 データ モデルでのネイティブ ポインターをゼロ拡張 64 ビット数量がデバッグ対象の仮想アドレス空間にオフセットを表します。 VT_UI8 内をボックス化し、このメソッドと、ネイティブ/言語のポインターを示す型が作成されます。 

[CreateMetadataStore](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createmetadatastore)

CreateMetadataStore メソッドは、プロパティおよびその他の値のさまざまな使用に関連付けることができるメタデータを保持するために使用されるキー ストア - メタデータ/キー/値の組の簡略化されたコンテナー--を作成します。 メタデータ ストアが 1 つの親 (さらに、単一の親であることができます) 必要があります。 特定のメタデータのキーが指定されたストアにない場合は、その親がチェックされます。 ほとんどのメタデータ ストアには、親はありません。 共通のメタデータを簡単に共有する方法は、提供。 

[CreateTypedIntrinsicObjectEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager2-createtypedintrinsicobjectex)

CreateTypedIntrinsicObjectEx メソッドは、意味的 CreateTypedIntrinsicObject メソッドと似ています。 2 つの唯一の違いは、このメソッドにより、送信者の組み込みのデータの有効なコンテキストを指定することです。 コンテキストが渡されない場合は、データが (CreateTypedIntrinsicObject の動作方法) 型の引数から継承はどのようなコンテキストで有効と見なされます。 これにより、型から継承できるよりも詳細なコンテキストを必要とする、デバッグ対象の型指定されたポインター値を作成できます。 

**拡張機能/登録メソッド**次の一連のメソッドは、クライアントで指定した親モデルを自動的にアタッチするデータ モデルを拡張または既存のモデルを登録するかをできるように、データ モデルの拡張メカニズムを管理指定された条件に一致するネイティブの型。

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

[GetModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getmodelfortypesignature)

GetModelForTypeSignature メソッドは、RegisterModelForTypeSignature メソッドを呼び出す前を使用して特定の型シグネチャに対して登録されているデータ モデルを返します。 このメソッドから返されるデータ モデルには、渡された型シグネチャに一致する任意の型の標準的なビジュアライザーと見なされます。 標準ビジュアライザー、としてそのデータ モデル型の表示が引き継ぎます。 表示エンジンは、既定では、非表示にデータ モデルによって提示されるオブジェクトのビューを優先してオブジェクトのネイティブ/言語構成要素。 


[GetModelForType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getmodelfortype)

GetModelForType メソッドは、データ モデルは、指定した型のインスタンスの標準的なビジュアライザーを返します。 実際には、このメソッドは、最も適した RegisterModelForTypeSignature メソッドを呼び出す前に登録されたされ、関連付けられているデータ モデルを返します型シグネチャを見つけます。 

[RegisterModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-registermodelfortypesignature)

RegisterModelForTypeSignature メソッドは、特定の型 (または型のセット) の標準的なビジュアライザーを登録する呼び出し元を利用する主な方法です。 正規のビジュアライザーは、これは実際には、指定された型 (または型のセット) の表示データ モデルです。 デバッガー ユーザー インターフェイスに表示されている型のネイティブ/言語ビューではなく、(ことを希望するユーザーのネイティブ/言語ビューに戻るのでは意味) と共に登録されているデータ モデルによって表される型のビューが表示されます。 

[UnregisterModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-unregistermodelfortypesignature)

UnregisterModelForTypeSignature メソッド元 RegisterModelForTypeSignature メソッドを呼び出す前に戻します。 このメソッドが特定の型シグネチャに一致する型の標準的なビジュアライザーとして指定されたデータ モデルを削除するか、またはそのデータ モデルが登録されているすべての型シグネチャの標準的なビジュアライザーとして指定されたデータ モデルを削除できます。 

[RegisterExtensionForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-registerextensionfortypesignature)

RegisterExtensionForTypeSignature メソッドは、1 つ大きな違いがあります RegisterModelForTypeSignature メソッドに似ています。 このメソッドに渡されるデータ モデルは任意の型の正規のビジュアライザーではなく、その型のネイティブ言語/ビューの表示にはなりません。 このメソッドに渡されるデータ モデルは、指定された型のシグネチャと一致する任意の具象型を親として自動的に追加されます。 RegisterModelForTypeSignature メソッドとは異なり制限はありませんで同一またはあいまいな型のシグネチャが指定された型 (または型のセット) に対する拡張として登録されています。 型シグネチャを持つには、特定の具象型のインスタンスが一致するすべての拡張機能には、親モデルとして新しく作成されたオブジェクトに自動的に接続するには、このメソッドを使用して登録されているデータ モデルが発生します。 これには、実際には、任意の数のクライアントが新しいフィールドまたは機能を使用して、型 (または型のセット) を拡張するを許可します。 

[UnregisterExtensionForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-unregisterextensionfortypesignature)

UnregisterExtensionForTypeSignature メソッドでは、RegisterExtensionForTypeSignature 前回の呼び出し元に戻します。 特定の型シグネチャの拡張機能として、または対象となるデータ モデルが登録されているすべての型シグネチャの拡張機能として、特定のデータ モデルが登録解除します。 

[GetRootNamespace](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getrootnamespace)

GetRootNamespace メソッドは、データ モデルのルート名前空間を返します。 これは、オブジェクトは、特定のオブジェクトがデバッグ ホストによって格納されるデータ モデルを管理します。 

[RegisterNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getrootnamespace)

RegisterNamedModel メソッドは、それを拡張したいクライアントが検出できる既知の名前で指定されたデータ モデルを登録します。 この既知の名前で登録されているモデルを取得することによって拡張できるものとしてのデータ モデルを発行する - API の主な目的は、これを親モデルを追加します。 

[UnregisterNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-unregisternamedmodel)

UnregisterNamedModel メソッドでは、RegisterNamedModel 前回の呼び出し元に戻します。 データ モデルと名前を検索できるの間の関連付けを削除します。 

[AcquireNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-acquirenamedmodel)

呼び出し元が指定された名前で登録されているデータ モデルを拡張したいユーザーは、拡張したいデータ モデルのオブジェクトを取得するために AcquireNamedModel メソッドを呼び出します。 このメソッドでは、RegisterNamedModel メソッドを呼び出す前を使用して登録された任意のデータ モデルを返します。 AcquireNamedModel メソッドの主な目的は、モデルを拡張するのには、このメソッドはモデルが登録されていない指定した名前でまだ特別な動作を使用します。 モデルが登録されていない指定した名前でまだの場合、スタブ オブジェクトを作成、一時的に指定した名前の下に登録し、呼び出し元に返されます。 RegisterNamedModel メソッドの呼び出しを使用して、実際のデータ モデルが登録されると、スタブ オブジェクトに対して行われたすべての変更は、実際には、実際のモデルに加えられました。 これにより、ロード順序依存関係の多くの問題が互いを拡張するコンポーネントから削除します。 


**ヘルパー メソッド**

次のメソッドは、データ モデルのオブジェクトに対する複雑な操作の実行を支援する一般的なヘルパー メソッドです。 データ モデルまたはそのオブジェクトで他のメソッドを使用してこれらのアクションを実行することはできますが、これらのメソッドが大幅に簡素化します。 

```cpp
STDMETHOD(AcquireSubNamespace)(_In_ PCWSTR modelName, _In_ PCWSTR subNamespaceModelName, _In_ PCWSTR accessName, _In_opt_ IKeyStore *metadata, _COM_Outptr_ IModelObject **namespaceModelObject) PURE;
```

[AcquireSubNamespace](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager2-acquiresubnamespace)

AcquireSubNamespace メソッドは、動的言語で新しいオブジェクトよりも言語の名前空間が例より従来だものの構築に役立ちます。 かどうかより整理されたプロセス オブジェクトを作成するプロセス オブジェクトのプロパティと簡単に検出すると、このプロセス オブジェクトの各カテゴリの下位のオブジェクトを作成する方法と配置の 1 つのメソッドのプロパティを分類するなど、呼び出し元がそのオブジェクト内でこれらのプロパティ。 




---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバッガー データ モデルの C++ の概要](data-model-cpp-overview.md)

[デバッガーのデータ モデルの C++ インターフェイス](data-model-cpp-interfaces.md)

[デバッガーのデータ モデルの C++ オブジェクト](data-model-cpp-objects.md)

[デバッガーのデータ モデルの C++ の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーのデータ モデルの C の概念](data-model-cpp-concepts.md)

[デバッガー データ モデルの C++ のスクリプト](data-model-cpp-scripting.md)
