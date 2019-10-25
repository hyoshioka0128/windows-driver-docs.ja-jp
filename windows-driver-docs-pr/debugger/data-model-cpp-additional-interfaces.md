---
title: Debugger Data Model C++ のその他のインターフェイス
description: このトピックでは、メタデータ、概念C++ 、オブジェクトの列挙など、デバッガーデータモデルに関連付けられている追加のインターフェイスについて説明します。
ms.date: 09/12/2018
ms.openlocfilehash: e2878f090f3ad8bd2bcd2e0cf10f9fd52884fc73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837814"
---
# <a name="debugger-data-model-c-additional-interfaces"></a>Debugger Data Model C++ のその他のインターフェイス

このトピックでは、メタデータ、概念、 C++オブジェクトの列挙など、デバッガーデータモデルに関連付けられているいくつかの追加のインターフェイスについて説明します。

## <a name="span-idmetadatainterfacesspan-debugger-data-model-metadata-interfaces"></a><span id="metadatainterfaces"></span>デバッガーデータモデルのメタデータインターフェイス

データモデルの主要な概念の1つは、オブジェクト (特に合成型) が、キー/値/メタデータの組のディクショナリであることです。 各キーには、関連付けられているメタデータのストア全体を含めることができます。これにより、キーとその可能性のある値を囲むさまざまな要素が記述されます。 メタデータは、どのような方法でもキーの値を変更しないことに注意してください。 キーとその値に関連付けられている補助的な情報のみが、キーとその値のプレゼンテーションやその他の関連属性に影響を与える可能性があります。 

いくつかの点で、メタデータストアは、データモデル内のオブジェクトの本質であるキー/値/メタデータタプルとは異なるものではありません。 ただし、このビューでは簡略化されています。 メタデータストアは、IKeyStore ストアインターフェイスによって表されます。 また、キー/値/メタデータの組のコレクションでも、メタデータキーストアとモデルオブジェクトを使用して実行できることには制限があります。 

- キーストアには、親ストアを1つだけ含めることができます。親モデルの任意のチェーンを持つことはできません。
- キーストアには概念がありません。 キー/値/メタデータタプルの辞書のみを持つことができます。 これは、キーストアに存在するキーが静的であることを意味します。 動的言語システムで要求時に作成することはできません。
- 規則により、メタデータで定義されたキーストア内の値は、基本値 (組み込みおよびプロパティアクセサー) に制限されます。

キーストアはキーの任意の数 (および任意の名前付け) を持つことができますが、セマンティック値が定義されている特定の名前があります。 現在、これらの名前は次のとおりです。 

キー名 | 値の種類 | 説明
|--------------|------------------|--------------|
PreferredRadix | 整数: 2、8、10、または16 | 序数値を表示する基数を示します。
PreferredFormat | 整数: PreferredFormat 列挙体で定義されているとおり | 値の表示に適した書式設定の種類を示します。
PreferredLength | 整数型 | 配列とその他のコンテナーについては、既定で表示される要素の数を示します。
FindDerivation | Boolean | を使用する前に、デバッグホストが値に対して派生型の分析を実行する必要があるかどうかを示します (例: 表示)
Help | String | ツールヒントスタイルユーザーインターフェイスによって適切に表示できるキーのヘルプテキスト。
ActionName | String | 指定されたメソッド (引数を取らず、値を返さないメソッド) がアクションであることを示します。 アクションの名前はメタデータで指定されます。 ユーザーインターフェイスは、この名前を使用して、コンテキストメニューやその他の適切なインターフェイスにオプションを表示することができます。
ActionIsDefault | Boolean | ActionName キーが指定されている場合にのみ有効です。は、これがオブジェクトの既定のアクションであることを示します。
ActionDescription | String | ActionName キーが指定されている場合にのみ有効です。これにより、アクションのツールヒントスタイルの説明が提供されます。 このようなテキストは、適切な方法でユーザーインターフェイスに表示できます。

メタデータストア内のキーには独自のメタデータ (ad infiniteum) を含めることができますが、現時点ではこのような機能は使用されていないことに注意してください。 ほとんどの呼び出し元は、IKeyStore ストアインターフェイスのメソッドのメタデータパラメーターに null を指定します。 

**コアメタデータインターフェイス: IKeyStore ストア**

IKeyStore ストアインターフェイスは、次のように定義されています。 

```cpp
DECLARE_INTERFACE_(IKeyStore, IUnknown)
{
   STDMETHOD(GetKey)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(SetKey)(_In_ PCWSTR key, _In_opt_ IModelObject* object, _In_opt_ IKeyStore* metadata) PURE;
   STDMETHOD(GetKeyValue)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(SetKeyValue)(_In_ PCWSTR key, _In_ IModelObject* object) PURE;
   STDMETHOD(ClearKeys)() PURE;
}
```

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-getkey)

GetKey メソッドは、IModelObject の GetKey メソッドに似ています。 キーストアまたはキーストアの親ストアに存在する場合は、指定されたキーの値が返されます。 キーの値がプロパティアクセサーの場合は、プロパティアクセサーで GetValue メソッドが呼び出されないことに注意してください。 IModelObject にボックス化された実際の IModelPropertyAccessor が返されます。 通常は、クライアントがこの理由で GetKeyValue を呼び出すことになります。 

[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-setkey)

SetKey メソッドは、IModelObject の SetKey メソッドに似ています。 キーを作成し、メタデータをキーストア内で関連付けることができる唯一の方法です。 

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-getkeyvalue)

GetKeyValue メソッドは、メタデータストア内の特定のキーの値を検索するためにクライアントが最初に実行するメソッドです。 キー引数で指定されたキーがストア (またはその親ストア) 内に存在する場合、そのキーの値とそれに関連付けられているメタデータが返されます。 キーの値がプロパティアクセサー (IModelObject にボックス化された IModelPropertyAccessor) である場合は、プロパティアクセサーの GetValue メソッドが GetKeyValue によって自動的に呼び出され、返されるプロパティの基になる値が返されます。 

[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-setkeyvalue)

SetKeyValue メソッドは、IModelObject の SetKeyValue メソッドに似ています。 このメソッドでは、メタデータストア内に新しいキーを作成することはできません。 キー引数で示されているような既存のキーがある場合、その値は示すように設定されます。 キーがプロパティアクセサーの場合は、基になる値を設定するために、プロパティアクセサーで SetValue メソッドが呼び出されます。 メタデータは、通常、作成されると静的であることに注意してください。 メタデータキーストアでこのメソッドを使用することは、頻繁に行わないようにしてください。 

[ClearKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-clearkeys)

ClearKeys メソッドは、IModelObject の ClearKeys メソッドに似ています。 このメソッドは、指定されたメタデータストアからすべてのキーを削除します。 このメソッドは、どの親ストアにも影響しません。 


## <a name="span-idobjectspan-object-enumeration-in-the-data-model"></a><span id="object"></span>データモデルのオブジェクト列挙型

**データモデル内のオブジェクトの列挙**

データモデルには、IKeyEnumerator と Ikeyenumerator の2つのコアキー列挙インターフェイスがあります。 これらは2つのコアインターフェイスですが、次の3つのスタイルのいずれかでオブジェクトを列挙するために使用できます。 

*Keys* -IKeyEnumerator インターフェイスは、基になるプロパティアクセサーを解決せずに、オブジェクトのキーとその値/メタデータを列挙するために、EnumerateKeys の呼び出しによって取得できます。 この列挙型は、IModelObjects にボックス化された生の IModelPropertyAccessor 値を返すことができます。

*値*-ikeyenumerator インターフェイスと ikeyenumerator インターフェイスは、オブジェクトのキー/生の値とその値/メタデータを列挙するために、EnumerateKeyValues または列挙値のいずれかの呼び出しによって取得できます。 列挙体に存在するプロパティアクセサーは、そのような列挙中に基になる GetValue メソッドの呼び出しによって自動的に解決されます。

*参照*-ikeyenumerator インターフェイスと ikeyenumerator インターフェイスは、オブジェクトのキー/生の値への参照を列挙するために、EnumerateKeyReferences または列挙のいずれかの参照を使用して取得できます。 このような参照を保存し、後で使用して基になるキーまたは生の値を取得または設定することができます。

**KeyEnumerator: 統合キーの列挙**

IKeyEnumerator インターフェイスは、インスタンスオブジェクト内のすべてのキー (キー、値、または参照) の列挙型の単一のインターフェイスで、親モデルチェーン内のすべての関連付けられた親モデルに対応しています。 インターフェイスは次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IKeyEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_ BSTR* key, _COM_Errorptr_opt_ IModelObject** value, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeyenumerator-reset)

Reset メソッドは、列挙子を最初に取得した位置 (たとえば、列挙体の最初の要素の前) にリセットします。 次に GetNext を呼び出すと、最初に列挙されたキーが返されます。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeyenumerator-getnext)

GetNext メソッドは、列挙子を前方に移動し、列挙体のその位置にあるキーを返します。


**IRawEnumerator: ネイティブまたは基になる言語 (CC++/) コンストラクトの列挙体**

IRawEnumerator インターフェイスは、デバッグターゲットのアドレス空間内のネイティブコンストラクトを表すオブジェクト内のすべてのネイティブ/言語コンストラクト (値または参照) の列挙体の単一のインターフェイスです。 インターフェイスは次のように定義されます。 

```cpp
DECLARE_INTERFACE_(IRawEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_opt_ BSTR* name, _Out_opt_ SymbolKind *kind, _COM_Errorptr_opt_ IModelObject** value) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-irawenumerator-reset)

Reset メソッドは、列挙子を最初に取得した位置 (たとえば、列挙体の最初の要素の前) にリセットします。 次に GetNext を呼び出すと、最初に列挙されたネイティブ/言語構成体が返されます。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-irawenumerator-getnext)

GetNext メソッドは、両方とも列挙子を前方に移動し、列挙体のその位置にあるネイティブ/言語コンストラクトを返します。 

---

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

このトピックは、からC++アクセス可能なインターフェイス、それらを使用してC++ベースのデバッガー拡張機能を構築する方法、およびC++データモデル拡張機能から他のデータモデル構造 (JavaScript や NatVis など) を使用する方法について説明したシリーズの一部です.

[デバッガーデータモデルC++の概要](data-model-cpp-overview.md)

[デバッガーデータモデルC++のインターフェイス](data-model-cpp-interfaces.md)

[デバッガーデータモデルC++オブジェクト](data-model-cpp-objects.md)

[デバッガーデータモデルC++の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーデータモデルC++の概念](data-model-cpp-concepts.md)

[デバッガーデータモデルC++のスクリプト](data-model-cpp-scripting.md)
