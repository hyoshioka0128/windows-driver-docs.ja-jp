---
title: JavaScript 拡張機能のネイティブ デバッガー オブジェクト - デバッガー オブジェクトの詳細
description: ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構成要素を表します。 このトピックでは、JavaScript 拡張機能のネイティブデバッガーオブジェクトに関する追加の詳細について説明します。
ms.assetid: A8E12564-D083-43A7-920E-22C4D627FEE9
ms.date: 01/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: a96d0222a5715394edbdf924ab2dda506f53922d
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76315112"
---
# <a name="native-debugger-objects-in-javascript-extensions---debugger-object-details"></a>JavaScript 拡張機能のネイティブ デバッガー オブジェクト - デバッガー オブジェクトの詳細

このトピックでは、JavaScript 拡張機能でのネイティブデバッガーオブジェクトの使用に関する追加の詳細について説明します。

ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構造と動作を表します。 オブジェクトは、デバッガーの状態を操作するために (またはで取得した) JavaScript 拡張機能に渡すことができます。

デバッガーオブジェクトの JavaScript 拡張機能の詳細については、「 [Javascript 拡張機能のネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)」を参照してください。

JavaScript の使用に関する一般的な情報については、「 [Javascript デバッガースクリプト](javascript-debugger-scripting.md)」を参照してください。

## <a name="span-iddebugger-objectsspanspan-iddebugger-objectsspanspan-iddebugger-objectsspandebugger-objects-in-javascript-extensions"></a><span id="Debugger-Objects"></span><span id="debugger-objects"></span><span id="DEBUGGER-OBJECTS"></span>JavaScript 拡張機能におけるデバッガーオブジェクト

**渡す (ネイティブオブジェクトを)**

デバッガーオブジェクトは、さまざまな方法で JavaScript 拡張に渡すことも、取得することもできます。

-   JavaScript の関数またはメソッドに渡すことができます。
-   JavaScript プロトタイプのインスタンスオブジェクトにすることができます (たとえば、ビジュアライザーとして)。
-   これらは、ネイティブデバッガーオブジェクトを作成するように設計されたホストメソッドから返すことができます。
-   これらは、デバッガーのネイティブオブジェクトを作成するように設計されたホストメソッドから返すことができます。

JavaScript 拡張機能に渡されるデバッガーオブジェクトには、このセクションで説明されている一連の機能があります。

-   プロパティアクセス
-   プロジェクション名
-   ネイティブデバッガーオブジェクトに関連する特別な型
-   追加の属性

**プロパティアクセス**

JavaScript プロバイダー自体によって配置されるオブジェクトにはいくつかのプロパティがありますが、JavaScript を入力するネイティブオブジェクトのプロパティの大部分は、データモデルによって提供されます。 これは、プロパティアクセス---オブジェクト propertyname またはオブジェクト\[propertyName\]の場合、次のようになります。

-   *PropertyName*が JavaScript プロバイダー自体によってオブジェクトに投影されたプロパティの名前である場合、この値は最初に解決されます。それ以外
-   *PropertyName*がデータモデル (別のビジュアライザー) によってオブジェクトに投影されたキーの名前である場合、この名前は2番目の名前に解決されます。それ以外
-   *PropertyName*がネイティブオブジェクトのフィールドの名前である場合、この名前は3番目の名前に解決されます。それ以外
-   オブジェクトがポインターである場合、ポインターは逆参照され、上記のサイクルは続行されます (逆参照されたオブジェクトの射影されたプロパティと、その後にネイティブフィールドが続くキー)

JavaScript でのプロパティアクセスの通常の方法である、オブジェクト. propertyName と object\[propertyName\]--デバッガー内の ' dx ' コマンドと同様に、オブジェクトの基になるネイティブフィールドにアクセスします。

**プロジェクション名**

次のプロパティ (およびメソッド) は、JavaScript を入力するネイティブオブジェクトに投影されます。

| 認証方法             | Signature                  | 説明                                                                                                                                |
|--------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| hostContext        | プロパティ                   | オブジェクトが含まれているコンテキスト (アドレス空間、デバッグターゲットなど) を表すオブジェクトを返します。                              |
| targetLocation     | プロパティ                   | オブジェクトがアドレス空間 (仮想アドレス、レジスタ、サブレジスタなど) 内にあることを抽象化したオブジェクトを返します。 |
| targetSize         | プロパティ                   | オブジェクトのサイズ (実質的には sizeof (オブジェクト&gt;の&lt;型) を返します。                                                                |
| addParentModel     | .addParentModel(object)    | 新しい親モデル (JavaScript プロトタイプに似ていますが、データモデル側) をオブジェクトに追加します。                                          |
| removeParentModel  | .removeParentModel(object) | 指定された親モデルをオブジェクトから削除します。                                                                                               |
| runtimeTypedObject | プロパティ                   | オブジェクトに対して分析を実行し、それをランタイム (最派生) 型に変換しようとします。                                                 |
| targetType         | プロパティ                   | JavaScript 拡張機能は、基になる言語の型システムに直接アクセスできます。 このアクセスは、型オブジェクトの概念によって表されます。 詳細については、「 [JavaScript 拡張機能のネイティブデバッガーオブジェクト-型オブジェクト](native-objects-in-javascript-extensions-type-objects.md)」を参照してください。  |

オブジェクトがポインターの場合、次のプロパティ (およびメソッド) が、JavaScript に入るポインターに投影されます。

| プロパティ名 | Signature      | 説明                                                                    |
|---------------|----------------|--------------------------------------------------------------------------------|
| 追加           | 。追加 (値)    | ポインターと指定した値の間でポインターの数値演算を実行します。     |
| address       | プロパティ       | ポインターのアドレスを64ビットの序数オブジェクト (ライブラリ型) として返します。 |
| 間接   | .dereference() | ポインターを逆参照し、基になるオブジェクトを返します。                     |
| isNull        | プロパティ       | ポインター値が nullptr (0) かどうかを返します。                        |

**ネイティブデバッガーオブジェクトに関連する特別な型**

**ロケーションオブジェクト**

ネイティブオブジェクトの targetLocation プロパティから返される location オブジェクトには、次のプロパティ (およびメソッド) が含まれています。

| プロパティ名 | Signature        | 説明                                          |
|---------------|------------------|------------------------------------------------------|
| 追加           | 。追加 (値)      | 位置に絶対バイトオフセットを追加します。        |
| 減算 (subtract)      | . 減算 (値) | 位置から絶対バイトオフセットを減算します。 |

**追加の属性**

**機能**

データモデルによって反復可能なとして認識される任意のオブジェクト (ネイティブ配列の場合、またはビジュアライザー (NatVis またはそれ以外の場合は反復可能な) がある場合は、そのオブジェクトに配置された反復子関数 (ES6 標準シンボルの反復子を使用してインデックスが付けられます)。 これは、次のように JavaScript でネイティブオブジェクトを反復処理できることを意味します。

```javascript
function iterateNative(nativeObject)
{
    for (var val of nativeObject)
    {
        // 
        // val will contain each element iterated from the native object.  This would be each element of an array,
        // each element of an STL structure which is made iterable through NatVis, each element of a data structure
        // which has a JavaScript iterator accessible via [Symbol.iterator], or each element of something
        // which is made iterable via support of IIterableConcept in C/C++.
        //
    }
}
```

**インデックス**

序数 (たとえば、ネイティブ配列) を使用して1つのディメンションでインデックス可能として認識されるオブジェクトは、標準プロパティアクセス演算子--object\[index\]を使用して JavaScript でインデックスを作成できます。 オブジェクトが名前によってインデックス可能な場合、または複数の次元でインデックスを付けられる場合は、JavaScript コードがインデクサーを利用できるように、getValueAt メソッドと setValueAt メソッドがオブジェクトに投影されます。

```javascript
function indexNative(nativeArray)
{
    var first = nativeArray[0];
}
```

**文字列変換**

IStringDisplayableConcept または NatVis DisplayString 要素のサポートによる表示文字列変換を含むネイティブオブジェクトでは、標準の JavaScript toString メソッドを使用して、その文字列変換にアクセスできます。

```javascript
function stringifyNative(nativeObject)
{
    var myString = nativeObject.toString();
}
```

## <a name="span-idcreating_native_debugger_objectsspanspan-idcreating_native_debugger_objectsspanspan-idcreating_native_debugger_objectsspancreating-native-debugger-objects"></a><span id="Creating_Native_Debugger_Objects"></span><span id="creating_native_debugger_objects"></span><span id="CREATING_NATIVE_DEBUGGER_OBJECTS"></span>ネイティブデバッガーオブジェクトの作成

前述のように、JavaScript スクリプトは、複数の方法のいずれかで JavaScript に渡されるか、またはホストライブラリの呼び出しを通じて作成できるようにすることで、ネイティブオブジェクトにアクセスできます。 ネイティブデバッガーオブジェクトを作成するには、次の関数を使用します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">認証方法</th>
<th align="left">Signature</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>getModuleSymbol</p></td>
<td align="left"><p>getModuleSymbol (moduleName, symbolName, [contextInheritor])</p>
<p>getModuleSymbol (moduleName, symbolName, [typeName], [contextInheritor])</p></td>
<td align="left"><p>特定のモジュール内のグローバルシンボルのオブジェクトを返します。 モジュール名とシンボル名は文字列です。</p>
<p>省略可能な<em>Contextinheritor は</em>引数を指定した場合、モジュールとシンボルは、渡されたオブジェクトと同じコンテキスト (アドレス空間、デバッグターゲット) 内で検索されます。 引数が指定されていない場合は、デバッガーの現在のコンテキストでモジュールとシンボルが検索されます。 1回限りのテストスクリプトではない JavaScript 拡張機能は、常に明示的なコンテキストを提供する必要があります。</p>
<p>省略可能な<em>typeName</em>引数を指定すると、シンボルは渡された型であると見なされ、シンボルで示されている型は無視されます。 モジュールのパブリックシンボルを操作する呼び出し元は、常に明示的な型名を指定する必要があることに注意してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ホストの Createポインターオブジェクト</p></td>
<td align="left"><p>Createポインターオブジェクト (address、moduleName、typeName、[contextInheritor])</p></td>
<td align="left"><p>指定したアドレスまたは場所にポインターオブジェクトを作成します。 モジュール名と型名は文字列です。</p>
<p>省略可能な<em>Contextinheritor は</em>引数を指定した場合、モジュールとシンボルは、渡されたオブジェクトと同じコンテキスト (アドレス空間、デバッグターゲット) 内で検索されます。 引数が指定されていない場合は、デバッガーの現在のコンテキストでモジュールとシンボルが検索されます。 1回限りのテストスクリプトではない JavaScript 拡張機能は、常に明示的なコンテキストを提供する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ホストの createTypedObject</p></td>
<td align="left"><p>createTypedObject (location、moduleName、typeName、[contextInheritor])</p></td>
<td align="left"><p>指定した位置にあるデバッグターゲットのアドレス空間内にある、ネイティブに型指定されたオブジェクトを表すオブジェクトを作成します。 モジュール名と型名は文字列です。</p>
<p>省略可能な<em>Contextinheritor は</em>引数を指定した場合、モジュールとシンボルは、渡されたオブジェクトと同じコンテキスト (アドレス空間、デバッグターゲット) 内で検索されます。 引数が指定されていない場合は、デバッガーの現在のコンテキストでモジュールとシンボルが検索されます。 1回限りのテストスクリプトではない JavaScript 拡張機能は、常に明示的なコンテキストを提供する必要があります。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idhost-apisspanspan-idhost-apisspanspan-idhost-apisspanhost-apis-for-javascript-extensions"></a><span id="Host-APIs"></span><span id="host-apis"></span><span id="HOST-APIS"></span>JavaScript 拡張機能用のホスト Api

JavaScript プロバイダーは、ホストと呼ばれるオブジェクトを、読み込まれるすべてのスクリプトのグローバル名前空間に挿入します。 このオブジェクトを使用すると、スクリプトの重要な機能に加えて、デバッガーの名前空間にアクセスできます。 2つのフェーズで設定されています。

-   **フェーズ 1**: スクリプトを実行する前に、ホストオブジェクトには、スクリプトがそれ自体を初期化し、機能拡張ポイント (プロデューサーとコンシューマーの両方) を登録するために必要な最小限の機能のみが含まれています。 ルートおよび初期化コードは、デバッグターゲットの状態を操作したり、複雑な操作を実行したりするためのものではありません。そのため、initializeScript メソッドが返されるまで、ホストは完全には設定されません。

-   **フェーズ 2**: initializeScript がを返した後、ホストオブジェクトには、デバッグターゲットの状態を操作するために必要なすべてのものが格納されます。

**ホストオブジェクトレベル**

いくつかの重要な機能は、ホストオブジェクトの直下にあります。 残りの部分は、サブ空間です。 名前空間には、次のものが含まれます。

| 名前空間   | 説明                                                              |
|-------------|--------------------------------------------------------------------------|
| 診断 | スクリプトコードの診断とデバッグに役立つ機能    |
| memory      | デバッグターゲット内でメモリの読み取りと書き込みを有効にする機能 |

**ルートレベル**

ホストオブジェクト内で直接、次のプロパティ、メソッド、およびコンストラクターを見つけることができます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名前</th>
<th align="left">Signature</th>
<th align="left">フェーズ存在</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Createポインターオブジェクト</td>
<td align="left"><p>Createポインターオブジェクト (address、moduleName、typeName、[contextInheritor])</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">指定したアドレスまたは場所にポインターオブジェクトを作成します。 モジュール名と型名は文字列です。 省略可能な<strong>Contextinheritor は</strong>引数は、getModuleSymbol と同様に機能します。</td>
</tr>
<tr class="even">
<td align="left">createTypedObject</td>
<td align="left"><p>createTypedObject (location、moduleName、typeName、[contextInheritor])</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">指定した位置にあるデバッグターゲットのアドレス空間内にある、ネイティブに型指定されたオブジェクトを表すオブジェクトを作成します。 モジュール名と型名は文字列です。 省略可能な contextInheritor は引数は、getModuleSymbol と同様に機能します。</td>
</tr>
<tr class="odd">
<td align="left">currentProcess</td>
<td align="left"><p>プロパティ</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">デバッガーの現在のプロセスを表すオブジェクトを返します。</td>
</tr>
<tr class="even">
<td align="left">currentSession</td>
<td align="left"><p>プロパティ</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">デバッガーの現在のセッション (ターゲット、ダンプなど) を表すオブジェクトをデバッグしています</td>
</tr>
<tr class="odd">
<td align="left">currentThread</td>
<td align="left"><p>プロパティ</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">デバッガーの現在のスレッドを表すオブジェクトを返します。</td>
</tr>
<tr class="even">
<td align="left">evaluateExpression</td>
<td align="left"><p>evaluateExpression (式、[contextInheritor])</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、デバッグホストが呼び出され、デバッグターゲットの言語のみを使用して式が評価されます。 省略可能な<em>Contextinheritor は</em>引数を指定した場合、式は引数のコンテキスト (例: アドレス空間およびデバッグターゲット) で評価されます。それ以外の場合は、デバッガーの現在のコンテキストで評価されます。</td>
</tr>
<tr class="odd">
<td align="left">評価 Ate式 Incontext</td>
<td align="left"><p>Evaluate式 Incontext (コンテキスト、式)</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、デバッグホストが呼び出され、デバッグターゲットの言語のみを使用して式が評価されます。 Context 引数は、評価に使用する暗黙的な this ポインターを示します。 式はコンテキストで評価されます (例: アドレス空間とデバッグターゲット)。<em>コンテキスト</em>引数によって示されます。</td>
</tr>
<tr class="even">
<td align="left">getModuleSymbol</td>
<td align="left"><p>getModuleSymbol (moduleName, symbolName, [contextInheritor])</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">特定のモジュール内のグローバルシンボルのオブジェクトを返します。 モジュール名とシンボル名は文字列です。 省略可能な<em>Contextinheritor は</em>引数を指定した場合、モジュールとシンボルは、渡されたオブジェクトと同じコンテキスト (アドレス空間、デバッグターゲット) 内で検索されます。 引数が指定されていない場合は、デバッガーの現在のコンテキストでモジュールとシンボルが検索されます。 1回限りのスクリプトではない JavaScript 拡張機能は、常に明示的なコンテキストを提供する必要があります</td>
</tr>
<tr class="odd">
<td align="left">getNamedModel</td>
<td align="left"><p>getNamedModel (modelName)</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">指定された名前に対して登録されたデータモデルを返します。 これは、まだ登録されていない名前を使用して呼び出すことができることに注意してください。 これにより、その名前のスタブが作成され、登録時にスタブの操作が実際のオブジェクトに対して行われます。</td>
</tr>
<tr class="even">
<td align="left">indexedValue</td>
<td align="left"><p>new indexedValue(value, indicies)</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">決まっの既定のセットを反復される値に割り当てるために JavaScript 反復子から返すことができるオブジェクトのコンストラクター。 決まっのセットは、JavaScript 配列として表現する必要があります。</td>
</tr>
<tr class="odd">
<td align="left">Int64</td>
<td align="left"><p>新しい Int64 (value, [highValue])</p></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、ライブラリ Int64 型が構築します。 1つの引数のバージョンは、(変換せずに) Int64 にパックしてそのに配置できる任意の値を受け取ります。 省略可能な2番目の引数を指定すると、最初の引数の変換が下位の32ビットにパックされ、2番目の引数の変換が上位32ビットにパックされます。</td>
</tr>
<tr class="even">
<td align="left">namedModelParent</td>
<td align="left"><p>新しい namedModelParent (オブジェクト、名前)</p></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left"><strong>InitializeScript</strong>から返された配列に配置することを目的としたオブジェクトのコンストラクター。これは、指定された名前を持つデータモデルのデータモデルの親拡張として JavaScript プロトタイプまたは ES6 クラスを使用することを表します。</td>
</tr>
<tr class="odd">
<td align="left">namedModelRegistration</td>
<td align="left"><p>新しい namedModelRegistration (オブジェクト、名前)</p></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left"><strong>InitializeScript</strong>から返された配列に配置することを目的としたオブジェクトのコンストラクター。これは、他の拡張機能が検索および拡張できるように、既知の名前を使用して JavaScript プロトタイプまたは ES6 クラスをデータモデルとして登録することを表します。</td>
</tr>
<tr class="even">
<td align="left">名前空間</td>
<td align="left"><p>プロパティ</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">デバッガーのルート名前空間への直接アクセスを提供します。 たとえば、最初のデバッグターゲットのプロセスリストに、ホスト. 名前空間. Debugger. Sessions. First () を使用してアクセスできます。このプロパティを使用するプロセス</td>
</tr>
<tr class="odd">
<td align="left">registerNamedModel</td>
<td align="left"><p>registerNamedModel (object, modelName)</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、JavaScript プロトタイプまたは ES6 クラスが、指定された名前でデータモデルとして登録されます。 このような登録により、プロトタイプまたはクラスを他のスクリプトまたはその他のデバッガー拡張機能によって特定し、拡張することができます。 スクリプトでは、これを強制的に実行するのではなく、 <strong>initializeScript</strong>メソッドから<strong>namedmodelregistration</strong>オブジェクトを返すようにする必要があることに注意してください。 変更を強制的に行うすべてのスクリプトは、クリーンアップするために<strong>initializeScript</strong>メソッドを持つ必要があります。</td>
</tr>
<tr class="even">
<td align="left">registerExtensionForTypeSignature</td>
<td align="left"><p>registerExtensionForTypeSignature (object, typeSignature)</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、指定された型シグネチャによって指定されたネイティブ型の拡張データモデルとして、JavaScript プロトタイプまたは ES6 クラスが登録されます。 スクリプトでは、これを強制的に実行するのではなく、 <strong>initializeScript</strong>メソッドから<strong>typeSignatureExtension</strong>オブジェクトを返すようにする必要があることに注意してください。 変更を強制的に行うすべてのスクリプトは、クリーンアップするために<strong>initializeScript</strong>メソッドを持つ必要があります。</td>
</tr>
<tr class="odd">
<td align="left">registerPrototypeForTypeSignature</td>
<td align="left"><p>registerPrototypeForTypeSignature (object, typeSignature)</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、指定された型シグネチャによって指定されたネイティブ型の正規データモデル (例: ビジュアライザー) として JavaScript プロトタイプまたは ES6 クラスが登録されます。 スクリプトでは、これを強制的に実行するのではなく、 <strong>initializeScript</strong>メソッドから<strong>typeSignatureRegistration</strong>オブジェクトを返すようにする必要があることに注意してください。 変更を強制的に行うすべてのスクリプトは、クリーンアップするために<strong>uninitializeScript</strong>メソッドを持つ必要があります。</td>
</tr>
<tr class="even">
<td align="left">Languageprimitives.parseint64</td>
<td align="left"><p>Languageprimitives.parseint64 (string, [radix])</p></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">このメソッドは、標準の JavaScript parseInt メソッドと同様に機能しますが、代わりにライブラリ Int64 型を返す点が異なります。 基数が指定されている場合、解析は、示されているように、基数2、8、10、または16のいずれかで行われます。</td>
</tr>
<tr class="odd">
<td align="left">typeSignatureExtension</td>
<td align="left"><p>new typeSignatureExtension (object, typeSignature, [moduleName], [minVersion], [maxVersion])</p></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left"><strong>InitializeScript</strong>から返された配列に配置することを目的としたオブジェクトのコンストラクター。これは、JavaScript プロトタイプまたは ES6 クラスによって型シグネチャを介して記述されるネイティブ型の拡張を表します。 このような登録では、完全に使用するのではなく、シグネチャに一致する任意の型のデバッガーの視覚化に "フィールドを追加" します。 オプションのモジュール名とバージョンでは、登録を制限できます。 バージョンは、"1.2.3.4" スタイルの文字列として指定されます。</td>
</tr>
<tr class="even">
<td align="left">typeSignatureRegistration</td>
<td align="left"><p>new typeSignatureRegistration (object, typeSignature, [moduleName], [minVersion], [maxVersion])</p></td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left"><strong>InitializeScript</strong>から返された配列に配置することを目的としたオブジェクトのコンストラクター。これは、ネイティブな型シグネチャに対する JavaScript プロトタイプまたは ES6 クラスの正規登録を表します。 このような登録は、拡張するだけではなく、シグネチャと一致する任意の型のデバッガーの視覚化を引き継ぎます。 オプションのモジュール名とバージョンでは、登録を制限できます。 バージョンは、"1.2.3.4" スタイルの文字列として指定されます。</td>
</tr>
<tr class="odd">
<td align="left">unregisterNamedModel</td>
<td align="left"><p>unregisterNamedModel(modelName)</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、指定された名前によるルックアップからデータモデルの登録を解除し、 <strong>Registernamedmodel</strong>によって実行される操作を元に戻すことがする</td>
</tr>
<tr class="even">
<td align="left">unregisterExtensionForTypeSignature</td>
<td align="left"><p>unregisterExtensionForTypeSignature (object, typeSignature, [moduleName], [minVersion], [maxVersion])</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、指定された型シグネチャによって指定されたネイティブ型の拡張データモデルとして、JavaScript プロトタイプまたは ES6 クラスの登録が解除されます。 これは、registerExtensionForTypeSignature の論理的な undo です。 スクリプトでは、これを強制的に実行するのではなく、 <strong>initializeScript</strong>メソッドから<strong>typeSignatureExtension</strong>オブジェクトを返すようにする必要があることに注意してください。 変更を強制的に行うすべてのスクリプトは、クリーンアップするために<strong>initializeScript</strong>メソッドを持つ必要があります。 オプションのモジュール名とバージョンでは、登録を制限できます。 バージョンは、"1.2.3.4" スタイルの文字列として指定されます。</td>
</tr>
<tr class="odd">
<td align="left">unregisterPrototypeForTypeSignature</td>
<td align="left"><p>unregisterPrototypeForTypeSignature (object, typeSignature, [moduleName], [minVersion], [maxVersion])</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、指定された型シグネチャによって指定されたネイティブ型の正規データモデル (例: ビジュアライザー) から JavaScript プロトタイプまたは ES6 クラスが登録解除されます。 これは、registerPrototypeForTypeSignature の論理的な undo です。 スクリプトでは、これを強制的に実行するのではなく、 <strong>initializeScript</strong>メソッドから<strong>typeSignatureRegistration</strong>オブジェクトを返すようにする必要があることに注意してください。 変更を強制的に行うすべてのスクリプトは、クリーンアップするために<strong>uninitializeScript</strong>メソッドを持つ必要があります。 オプションのモジュール名とバージョンでは、登録を制限できます。 バージョンは、"1.2.3.4" スタイルの文字列として指定されます。</td>
</tr>
</tbody>
</table>

**診断機能**

ホストオブジェクトの診断サブ名前空間には、次のものが含まれます。

| 名前     | Signature           | フェーズ存在 | 説明                                                                                                                                                                                                                                                                                                                                                   |
|----------|---------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| debugLog | debugLog (オブジェクト...) | 1 で保護されたプロセスとして起動されました             | これにより、スクリプト拡張機能に対する printf スタイルのデバッグが提供されます。 現時点では、debugLog からの出力は、デバッガーの出力コンソールにルーティングされます。 後で、この出力を柔軟にルーティングする計画があります。 注: これは、コンソールにユーザー出力を印刷する手段としては使用しないでください。 今後、このファイルがルーティングされることはありません。 |

**メモリの機能**

ホストオブジェクトのメモリサブ名前空間には、次のものが含まれます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名前</th>
<th align="left">Signature</th>
<th align="left">フェーズ存在</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">readMemoryValues</td>
<td align="left"><p>readMemoryValues (location、numElements、[elementSize]、[isSigned]、[contextInheritor])</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、デバッグターゲットのアドレス空間から生の値の配列が読み取られ、このメモリのビューの上に型指定された配列が配置されます。 指定された場所には、アドレス (64 ビット値)、場所オブジェクト、またはネイティブポインターを指定できます。 配列のサイズは、 <em>Numelements</em>引数によって示されます。 配列の各要素のサイズ (および型) は、オプションの<em>Elementsize</em>および<em>issigned</em>引数によって指定されます。 このような引数が指定されていない場合、既定値は byte (符号なし/1 バイト) です。 省略可能な<em>Contextinheritor</em>は引数を指定した場合、引数で指定されたコンテキスト (例: アドレス空間およびデバッグターゲット) でメモリが読み取られます。それ以外の場合は、デバッガーの現在のコンテキストから読み込まれます。 8、16、および32ビットの値に対してこのメソッドを使用すると、読み取りメモリに高速に型指定されたビューが配置されることに注意してください。 64ビットの値に対してこのメソッドを使用すると、64ビットのライブラリ型の配列が構築されるため、大幅にコストが高くなります。</td>
</tr>
<tr class="even">
<td align="left">readString</td>
<td align="left"><p>readString (location、[contextInheritor])</p>
<p>readString (location、[length]、[contextInheritor])</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、デバッグターゲットのアドレス空間からナロー (現在のコードページ) 文字列が読み込まれ、UTF-16 に変換され、結果が JavaScript 文字列として返されます。 メモリを読み取ることができなかった場合、例外がスローされる可能性があります。 指定された場所には、アドレス (64 ビット値)、場所オブジェクト、またはネイティブ char<em>を指定できます。 省略可能な<em>Contextinheritor</em>は引数を指定した場合、引数で指定されたコンテキスト (例: アドレス空間およびデバッグターゲット) でメモリが読み取られます。それ以外の場合は、デバッガーの現在のコンテキストから読み込まれます。 省略可能な<em>長さ</em>の引数を指定すると、読み取り文字列は指定した長さになります。</td>
</tr>
<tr class="odd">
<td align="left">readWideString</td>
<td align="left"><p>readWideString (location、[contextInheritor])</p>
<p>readWideString (location、[length]、[contextInheritor])</p></td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">これにより、デバッグターゲットのアドレス空間からワイド (UTF-16) 文字列が読み込まれ、結果が JavaScript 文字列として返されます。 メモリを読み取ることができなかった場合、例外がスローされる可能性があります。 指定された場所には、アドレス (64 ビット値)、場所オブジェクト、またはネイティブ wchar_t</em>を指定できます。 省略可能な<em>Contextinheritor</em>は引数を指定した場合、引数で指定されたコンテキスト (例: アドレス空間およびデバッグターゲット) でメモリが読み取られます。それ以外の場合は、デバッガーの現在のコンテキストから読み込まれます。 省略可能な<em>長さ</em>の引数を指定すると、読み取り文字列は指定した長さになります。</td>
</tr>
</tbody>
</table>

## <a name="span-iddata-modelspanspan-iddata-modelspanspan-iddata-modelspandata-model-concepts-in-javascript"></a><span id="Data-Model"></span><span id="data-model"></span><span id="DATA-MODEL"></span>JavaScript におけるデータモデルの概念

**データモデルマッピング**

次のデータモデルの概念は、JavaScript にマップされます。

| 概念                 | ネイティブインターフェイス             | 同じ JavaScript                                                |
|-------------------------|------------------------------|----------------------------------------------------------------------|
| 文字列変換       | IStringDisplayableConcept    | standard: toString (...){...}                                         |
| 機能             | IIterableConcept             | standard: \[Symbol. iterator\]() {...}                                 |
| インデックス            | IIndexableConcept            | プロトコル: getDimensionality (...)/getValueAt (...)/setValueAt (...) |
| ランタイム型の変換 | IPreferredRuntimeTypeConcept | プロトコル: getPreferredRuntimeTypedObject (...)                        |

**文字列変換**

文字列変換の概念 (IStringDisplayableConcept) は、標準の JavaScript **toString**メソッドに直接変換されます。 すべての JavaScript オブジェクトには、(オブジェクトによって提供される) 文字列変換があるため、データモデルに返されるすべての JavaScript オブジェクトを表示文字列に変換できます。 文字列変換をオーバーライドするには、独自の toString を実装する必要があります。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IStringDisplayableConcept::ToDisplayString(...)
    //
    toString()
    { 
        return "This is my own string conversion!";
    }
}
```

**機能**

オブジェクトが反復可能なであるかどうかを ES6 プロトコルに直接マップするかどうかを、データモデルの概念として反復可能なます。 \[Symbol. iterator\] メソッドを持つオブジェクトは、反復可能なと見なされます。 このようなの実装により、オブジェクトが反復可能なされます。

反復可能なのみのオブジェクトは、次のような実装を持つことができます。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIterableConcept::GetIterator
    //
    *[Symbol.iterator]()
    {
        yield "First Value";
        yield "Second Value";
        yield "Third Value";
    }
}
```

反復子から返されるオブジェクトには、特殊な戻り値の型を使用してインデックスと値を含める必要があるため、反復可能なとインデックス可能の両方のオブジェクトには特別な考慮が必要です。

**反復可能なとインデックス可能**

反復可能なおよびインデックス可能なオブジェクトは、反復子からの特別な戻り値を必要とします。 反復子は、値を生成する代わりに、indexedValue のインスタンスを生成します。 決まっは、2番目の引数の配列として indexedValue コンストラクターに渡されます。 多次元にすることはできますが、インデクサープロトコルで返される次元と一致する必要があります。

このコードは、実装例を示しています。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIterableConcept::GetIterator
    //
    *[Symbol.iterator]()
    {
        //
        // Consider this a map which mapped 42->"First Value", 99->"Second Value", and 107->"Third Value"
        //
        yield new host.indexedValue("First Value", [42]);
        yield new host.indexedValue("Second Value", [99]);
        yield new host.indexedValue("Third Value", [107]);
    }
}
```

**インデックス**

JavaScript とは異なり、データモデルでは、プロパティアクセスとインデックス作成の間で非常に明確な区別が行われます。 データモデルでインデックスを可能なものとして提示する JavaScript オブジェクトは、インデクサーの次元を返す getDimensionality メソッドで構成されるプロトコルを実装する必要があります。また、getValueAt メソッドと setValueAt メソッドのオプションのペアを指定された決まっでオブジェクトの読み取りと書き込みを実行します。 オブジェクトが読み取り専用または書き込み専用の場合は、getValueAt メソッドまたは setValueAt メソッドを省略できます。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIndexableConcept::GetDimensionality or IIterableConcept::GetDefaultIndexDimensionality
    //
    getDimensionality()
    {
        //
        // Pretend we are a two dimensional array.
        //
        return 2;
    } 

    //
    // This method will be called whenever any native code calls IIndexableConcept::GetAt
    //
    getValueAt(row, column)
    {
        return this.__values[row * this.__columnCount + column];
    }

    //
    // This method will be called whenever any native code calls IIndexableConcept::SetAt
    //
    setValueAt(value, row, column)
    {
        this.__values[row * this.__columnCount + column] = value;
    }
}
```

**ランタイム型の変換**

これは、型システム (ネイティブ) 型に対して登録されている JavaScript プロトタイプ/クラスにのみ関連します。 デバッガーは多くの場合、分析 (たとえば、ランタイム型情報 (RTTI)/v テーブル分析) を実行して、コードで表現された静的な型からオブジェクトの実際のランタイム型を特定できます。 ネイティブ型に対して登録されたデータモデルは、IPreferredRuntimeTypeConcept の実装によってこの動作をオーバーライドできます。 同様に、ネイティブオブジェクトに対して登録された JavaScript クラスまたはプロトタイプは、getPreferredRuntimeTypedObject メソッドで構成されるプロトコルの実装によって独自の実装を提供できます。

このメソッドは技術的に何でも返すことができますが、実際にはランタイム型または派生型ではないものを返すために、不正な形式と見なされることに注意してください。 このような場合、デバッガーのユーザーに大きな混乱が生じる可能性があります。 ただし、このメソッドをオーバーライドすることは、C スタイルのヘッダーや実装のオブジェクトスタイルなどに役立ちます。

```javascript
class myNativeModel
{
    //
    // This method will be called whenever the data model calls IPreferredRuntimeTypeConcept::CastToPreferredRuntimeType
    //
    getPreferredRuntimeTypedObject()
    {
        var loc = this.targetLocation;

        //
        // Perform analysis...
        //
        var runtimeLoc = loc.Add(runtimeObjectOffset);
  
        return host.createTypedObject(runtimeLoc, runtimeModule, runtimeTypeName);
    }
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[JavaScript 拡張機能のネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)

[JavaScript 拡張機能のネイティブデバッガーオブジェクト-設計とテストに関する考慮事項](native-objects-in-javascript-extensions-design-considerations.md)

[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

[JavaScript デバッガーのサンプルスクリプト](javascript-debugger-example-scripts.md)
