---
title: JavaScript 拡張機能のネイティブデバッガーオブジェクト-型オブジェクト
description: ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構成要素を表します。 JavaScript 拡張機能は、基になる言語の型システムに直接アクセスできます。 このアクセスは、型オブジェクトの概念によって表されます。
ms.assetid: D87AB19B-26E4-4C2C-94C8-DB4297880E0B
ms.date: 01/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: f9d020322ce72d447732ab183748a2bb4f111afb
ms.sourcegitcommit: 8dd886d4be2c21c6b19ace5ff0521b1bcaf5b383
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76521808"
---
# <a name="native-debugger-objects-in-javascript-extensions---type-objects"></a>JavaScript 拡張機能のネイティブデバッガーオブジェクト-型オブジェクト

 ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構成要素を表します。 JavaScript 拡張機能は、基になる言語の型システムに直接アクセスできます。 このアクセスは、*型オブジェクト*の概念によって表されます。 このトピックでは、型オブジェクトに関連付けられているプロパティについて説明します。

ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構造と動作を表します。 オブジェクトは、デバッガーの状態を操作するために (またはで取得した) JavaScript 拡張機能に渡すことができます。

デバッガーオブジェクトの JavaScript 拡張機能の詳細については、「 [Javascript 拡張機能のネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)」を参照してください。

JavaScript の使用に関する一般的な情報については、「 [Javascript デバッガースクリプト](javascript-debugger-scripting.md)」を参照してください。

## <a name="type-objects"></a>型オブジェクト

型オブジェクトは、さまざまな方法で取得できます。

- オブジェクトから: スクリプトに JavaScript 内にネイティブオブジェクトがある場合、ネイティブオブジェクトの静的な型を表す*型オブジェクト*を取得するために、そのオブジェクトの*targetType*プロパティにアクセスできます。
- ホストから: *getModuleType* API を呼び出して、特定のモジュールで定義されている任意の型の*型オブジェクト*を返すことができます。

型オブジェクトを取得すると、次のプロパティがあります。

<table>
<tr><td><b>名前</b></td><td><b>折本</b></td><td><b>説明</b></td></tr>

<tr><td>名前</td><td>プロパティ</td><td>型の名前を返します。</td></tr>

<tr><td>size</td><td>プロパティ</td><td>型のサイズを64ビット値として返します。</td></tr>

<tr><td>typeKind</td><td>プロパティ</td><td>型の種類を文字列として返します。  次のいずれかの値を指定できます: "udt"、"pointer"、"memberPointer"、"array"、"function"、"typedef"、"enum"、または "組み込み"。</td></tr>

<tr><td>baseType</td><td>プロパティ</td><td>この型の基になる型の型オブジェクトを返します。  これは継承をC++表していません。  ポインター型の場合、これはポイントされているの型です。  配列型の場合、これは配列に格納されている型です。</td></tr>

<tr><td>フィールド</td><td>プロパティ</td><td>名前付きプロパティとしてアクセスできる型のすべての名前付きフィールドを持つオブジェクトを返します。  各プロパティの値は、以下に説明する<i>フィールドオブジェクト</i>です。</td></tr>

<tr><td>baseClasses ・・・・・・・ライン</td><td>プロパティ</td><td>型のすべての直接の基底クラスの配列を返します。  配列内の各オブジェクトは、以下に説明する<i>基底クラスのオブジェクト</i>です。</td></tr>

<tr><td>functionReturnType</td><td>プロパティ</td><td>関数型の場合は、関数の戻り値の型を表す型オブジェクトを返します。</td></tr>

<tr><td>functionParameterTypes</td><td>プロパティ</td><td>関数型の場合は、関数のパラメーターの型を表す型オブジェクトの配列が返されます。</td></tr>

<tr><td>functionCallingConvention</td><td>プロパティ</td><td>関数型の場合は、関数の呼び出し規約が文字列として返されます。  "Unknown"、"__cdecl"、"fastcall"、"stdcall"、または "thiscall" のいずれかの値を指定できます。</td></tr>

<tr><td>ポインターの種類</td><td>プロパティ</td><td>ポインター型の場合は、ポインターの種類が文字列として返されます。  次のいずれかの値を指定できます: "standard"、"reference"、"rValueReference"、または "cxHat"。</td></tr>

<tr><td>memberType</td><td>プロパティ</td><td>メンバーポインターであるポインター型の場合は、メンバークラスを表す type オブジェクトを返します。</td></tr>

<tr><td>isGeneric</td><td>プロパティ</td><td>型がジェネリックかどうかを返します。  これにより、テンプレートの型に対して true が返されます。</td></tr>

<tr><td>genericArguments</td><td>プロパティ</td><td>ジェネリックである型の場合、ジェネリック引数の配列が返されます。  このような引数には型引数を指定することも、定数値を指定することもできます。</td></tr>

<tr><td>isBitField</td><td>プロパティ</td><td>型のストレージがビットフィールドであるかどうかを返します。</td></tr>

<tr><td>bitFieldPositions</td><td>プロパティ</td><td>ビットフィールド storage を表す型の場合、ビットフィールドの位置を示すビットフィールドの説明の型が返されます。</td></tr>

</table>

これらのエントリはすべて、フェーズ2の初期化中に存在します。

## <a name="field-objects"></a>Field オブジェクト

型内の各フィールドは、次のようにプロパティを持つフィールドオブジェクトによって記述されます。

<table>

<tr><td><b>名前</b></td><td><b>折本</b></td><td><b>説明</b></td></tr>

<tr><td>名前</td><td>プロパティ</td><td>フィールドの名前を返します。</td></tr>

<tr><td>type</td><td>プロパティ</td><td>フィールドの静的な型を表す型オブジェクトを返します。</td></tr>

<tr><td>locationKind</td><td>プロパティ</td><td>フィールドの場所の種類 (ストレージ) を文字列として返します。  次のいずれかの値を指定できます: "member"、"static"、"constant"、または "none"。</td></tr>

<tr><td>offset</td><td>プロパティ</td><td>オフセットを示す場所の種類 (例: "member") を持つフィールドの場合、これにより、それを含む型内のフィールドのオフセットが64ビット値として返されます。</td></tr>

<tr><td>インストール先</td><td>プロパティ</td><td>場所 (例: "static") を示す場所の種類を持つフィールドの場合、場所オブジェクトとしてフィールドの場所が返され<i>ます。</i></td></tr>

<tr><td>value</td><td>プロパティ</td><td>値 (例: "constant") を示す場所の種類を持つフィールドの場合は、フィールドの値が返されます。</td></tr>

</table>

これらのエントリはすべて、フェーズ2の初期化中に存在します。

## <a name="base-class-objects"></a>基底クラスオブジェクト

型内の各基底クラスは、次のようにプロパティを持つ基底クラスのオブジェクトによって記述されます。

<table>

<tr><td><b>名前</b></td><td><b>折本</b></td><td><b>説明</b></td></tr>

<tr><td>名前</td><td>プロパティ</td><td>基底クラスの名前を返します。</td></tr>

<tr><td>offset</td><td>プロパティ</td><td>この基底クラスが含まれている型内のオフセットを返します。</td></tr>

<tr><td>type</td><td>プロパティ</td><td>基底クラスの静的な型を表す型オブジェクトを返します。</td></tr>

</table>

これらのエントリはすべて、フェーズ2の初期化中に存在します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[JavaScript 拡張機能のネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)

[JavaScript 拡張機能のネイティブデバッガーオブジェクト-設計とテストに関する考慮事項](native-objects-in-javascript-extensions-design-considerations.md)

[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

[JavaScript デバッガーのサンプルスクリプト](javascript-debugger-example-scripts.md)
