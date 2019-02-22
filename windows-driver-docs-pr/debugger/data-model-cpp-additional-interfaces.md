---
title: デバッガーのデータ モデルの C++ の追加インターフェイス
description: このトピックでは、メタデータ、概念とオブジェクトの列挙など、デバッガーの C++ のデータ モデルに関連付けられている追加のインターフェイスについて説明します。
ms.date: 10/05/2018
ms.openlocfilehash: 3c0a9f9f11accd8d78a90b110cfae38d77257412
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557054"
---
# <a name="debugger-data-model-c-additional-interfaces"></a>デバッガーのデータ モデルの C++ の追加インターフェイス

このトピックでは、メタデータ、概念とオブジェクトの列挙など、デバッガーの C++ のデータ モデルに関連付けられているいくつか追加のインターフェイスについて説明します。

このトピックでは、C、C++ ベースのデバッガーの拡張機能の構築に使用する方法および作成する方法からアクセスできるインターフェイスについて説明するシリーズのパートの他のデータ モデルの構成要素を使用して (例。JavaScript または NatVis) C データ モデルの拡張機能から。

---

[デバッガー データ モデルの C++ の概要](data-model-cpp-overview.md)

[デバッガーのデータ モデルの C++ インターフェイス](data-model-cpp-interfaces.md)

[デバッガーのデータ モデルの C++ オブジェクト](data-model-cpp-objects.md)

[デバッガーのデータ モデルの C++ の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーのデータ モデルの C の概念](data-model-cpp-concepts.md)

[デバッガー データ モデルの C++ のスクリプト](data-model-cpp-scripting.md)

---

## <a name="topic-sections"></a>トピックのセクション

このトピックは次のセクションで構成されます。

[デバッガーのデータ モデルのメタデータ インターフェイス](#metadatainterfaces)

[データ モデルのオブジェクトの列挙](#object)

---

## <a name="span-idmetadatainterfacesspan-debugger-data-model-metadata-interfaces"></a><span id="metadatainterfaces"></span> デバッガーのデータ モデルのメタデータ インターフェイス

データ モデルの中核となる概念の 1 つは、オブジェクト (特に代理 1) が組のキー/値/メタデータのディクショナリです。 各キーには、ストア全体のさまざまなキーとその潜在的な値を囲むことを説明する、関連付けられているメタデータのことができます。 メタデータ、何らかの方法で変わらないこと、キーの値に注意してください。 キーと、プレゼンテーションやキーの関連付けられているその他の属性に影響を与える可能性があります、値とその値に関連付けられた補助的な情報のみになります。 

ある意味のメタデータ ストアは、データ モデル内のオブジェクトの最も重要な部分であるメタデータ/キー/値のタプルを変わりありません。 ただし、このビューから簡略化します。 メタデータ ストアは IKeyStore インターフェイスによって表されます。 メタデータ/キー/値の組のコレクションも、中には、モデル オブジェクトとメタデータのキー ストアと何ができるには制限があります。 

- キー ストアでは、1 つの親ストアを持つことができますのみ - 親モデルの任意のチェーンを持つことはできません。
- キー ストアには、概念がありません。 メタデータ/キー/値の組のディクショナリのみができます。 つまり、キー ストアに存在するキーは静的です。 作成できませんオンデマンドで動的言語システムで。
- 慣例としてのみ、定義されているメタデータのキー ストア内の値が (組み込み関数とプロパティのアクセサー) の基本的な値に制限されます。

キー ストアには、キーの任意の数 (と任意の名前付け) ことができますが、セマンティックの値が定義されている特定の名前があります。 現在、その名前には。 

キー名 | 値の種類 | 説明
|--------------|------------------|--------------|
PreferredRadix | 整数:2、8、10、または 16 | 序数値を表示するか、どのような基数を示します
PreferredFormat | 整数: PreferredFormat 列挙体によって定義されています。 | 値の表示優先書式設定の種類を示します
PreferredLength | 整数型 | 配列とその他のコンテナーは、既定では、要素の数を表示するかを示します
FindDerivation | ブール値 | デバッグ ホストが使用する前に、値の派生型の分析を実行する必要があるかどうかを示します (例:: を表示する)
Help | String | スタイルのヘルプに関するツールヒントのテキストを適切に便利な方法でユーザー インターフェイスで表示可能なキー。
アクション名 | String | (1 つの引数を受け取らないし、値は返されませんが) 特定のメソッドがアクションであることを示します。 アクションの名前は、メタデータで指定されます。 ユーザー インターフェイスは、コンテキスト メニューまたはその他の適切なインターフェイスのオプションを表示するには、この名前を利用できます。
ActionIsDefault | ブール値 | キーを指定すると、アクション名は、これは、オブジェクトの既定のアクションであることを示している場合にのみ有効です。
ActionDescription | String | 唯一の有効なアクションのツール ヒントのスタイルの説明は、この ActionName キーが指定されている場合。 そのようなテキストは、適切に便利な方法で、ユーザー インターフェイスで表示できます。

このような使用は現在ありませんの間は、メタデータ ストアのキーは、独自のメタデータ (ad infiniteum) を設定できます。 ほとんどの呼び出し元は、メタデータ パラメーター IKeyStore インターフェイスのメソッドの null を指定します。 

**コア メタデータ インターフェイス:IKeyStore**

IKeyStore インターフェイスの定義は次のとおりです。 

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

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-getkey)

GetKey メソッドは、IModelObject GetKey メソッドに似ています。 キー ストアまたはキー ストアの親ストアに存在する場合は、指定したキーの値を返します。 キーの値がプロパティのアクセサーの場合は、GetValue メソッドは呼び出されませんプロパティのアクセサーに注意してください。 実際の IModelPropertyAccessor、IModelObject にボックス化が返されます。 クライアントがこのため GetKeyValue を呼び出すことが一般的です。 

[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-setkey)

SetKey メソッドは、IModelObject SetKey メソッドに似ています。 キーの作成と、キー ストア内でそのメタデータを関連付けることのできる唯一の方法になります。 

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-getkeyvalue)

GetKeyValue メソッドは、最初のメソッドが、クライアントは、メタデータ ストア内で特定のキーの値を検索するために移動します。 キーの引数で指定されたキーが存在する場合、ストア (または親ストア) 内でそのキーとそれに関連付けられたメタデータの値が返されます。 キーの値がプロパティのアクセサー (、IModelObject にボックス化 IModelPropertyAccessor) の場合は、プロパティ アクセサーの GetValue メソッドに自動的に GetKeyValue して返されるプロパティの値を基になると呼ばれます。 

[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-setkeyvalue)

SetKeyValue メソッドは、IModelObject SetKeyValue メソッドに似ています。 このメソッドでは、メタデータ ストア内の新しいキーを作成することはできません。 キーの引数で示されている既存のキーがある場合は、記載されてその値が設定されます。 キーがプロパティのアクセサーの場合は、SetValue メソッドが基になる値を設定するにはプロパティのアクセサーに呼び出されます。 そのメタデータは、作成すると通常は静的に注意してください。 メタデータのキー ストアでは、このメソッドの使用が頻繁にあります。 

[ClearKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-clearkeys)

ClearKeys メソッドは、IModelObject ClearKeys メソッドに似ています。 特定のメタデータ ストアからのすべてのキーが削除されます。 このメソッドには、任意の親ストアへの影響がありません。 


## <a name="span-idobjectspan-object-enumeration-in-the-data-model"></a><span id="object"></span> データ モデルのオブジェクトの列挙

**データ モデル内のオブジェクトを列挙します。**

データ モデルには、2 つの中核となるキーの列挙体インターフェイスがあります。IKeyEnumerator IRawEnumerator. 2 つのコア インターフェイスのうちには、3 つのスタイルのいずれかでオブジェクトを列挙するために使用できます。 

*キー* -EnumerateKeys すべて基になるプロパティ アクセサーを解決せず、オブジェクトとその値/メタデータのキーを列挙するための呼び出しを使用して、IKeyEnumerator インターフェイスを取得できます。 列挙体のこのスタイルでは、IModelObjects にボックス化された生の IModelPropertyAccessor 値を返すことができます。

*値*-EnumerateKeyValues または EnumerateRawValues オブジェクトとその値/メタデータ/生のキー値を列挙するための呼び出しを使用して、IKeyEnumerator および IRawEnumerator インターフェイスを取得できます。 列挙体に存在するすべてのプロパティ アクセサーは、このような列挙体の中に、基になる GetValue メソッドの呼び出しを使用して自動的に解決されます。

*参照*-EnumerateKeyReferences または EnumerateRawReferences オブジェクトのキー/生の値への参照を列挙するための呼び出しを使用して、IKeyEnumerator および IRawEnumerator インターフェイスを取得できます。 このような参照を保存して後で取得または基になるキーまたは生の値を設定するために使用できます。

**KeyEnumerator:代理キーの列挙**

IKeyEnumerator インターフェイスは、インスタンス オブジェクトとその親モデル チェーン内のすべての関連付けられている親モデル内の (キー、値、または参照) をすべてのキーの列挙体の 1 つのインターフェイスです。 インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IKeyEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_ BSTR* key, _COM_Errorptr_opt_ IModelObject** value, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeyenumerator-reset)

Reset メソッドに最初に取得した位置に、列挙子をリセットします (例:: 列挙型の最初の要素の前に)。 GetNext 後続の呼び出しでは、最初に列挙されたキーを返します。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeyenumerator-getnext)

GetNext メソッドは、列挙子を前方に移動し、列挙体では、その位置にあるキーを返します。


**IRawEnumerator:ネイティブまたは基になる言語 (C/C++) の列挙型を構築します**

IRawEnumerator インターフェイスは、(値または参照) によって、デバッグ対象のアドレス空間内にネイティブ コンストラクトを表すオブジェクト内のすべてのネイティブ/言語コンストラクトの列挙体の 1 つのインターフェイスです。 インターフェイスの定義は次のとおりです。 

```cpp
DECLARE_INTERFACE_(IRawEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_opt_ BSTR* name, _Out_opt_ SymbolKind *kind, _COM_Errorptr_opt_ IModelObject** value) PURE;
}
```

[リセット](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-irawenumerator-reset)

Reset メソッドに最初に取得した位置に、列挙子をリセットします (例:: 列挙型の最初の要素の前に)。 GetNext 後続の呼び出しでは、最初列挙型のネイティブ/言語構成要素を返します。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-irawenumerator-getnext)

GetNext メソッド両方は、列挙子を前方に移動し、列挙体では、その位置にあるネイティブ/言語構成要素を返します。 


---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[デバッガー データ モデルの C++ の概要](data-model-cpp-overview.md)

[デバッガーのデータ モデルの C++ インターフェイス](data-model-cpp-interfaces.md)

[デバッガーのデータ モデルの C++ オブジェクト](data-model-cpp-objects.md)

[デバッガーのデータ モデルの C++ の追加インターフェイス](data-model-cpp-additional-interfaces.md)

[デバッガーのデータ モデルの C の概念](data-model-cpp-concepts.md)

[デバッガー データ モデルの C++ のスクリプト](data-model-cpp-scripting.md)

