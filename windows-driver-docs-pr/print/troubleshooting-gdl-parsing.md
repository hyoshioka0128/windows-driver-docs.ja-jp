---
title: GDL 解析のトラブルシューティング
description: GDL 解析のトラブルシューティング
ms.assetid: 8c678a2f-b15b-4693-9bed-0edec06b3485
keywords:
- GDL WDK、パーサー
- パーサー WDK GDL, トラブルシューティングの解析
- GDL データ WDK の解析
- GDL 解析 WDK のトラブルシューティング
- GDL WDK、解析エラー
- GDL WDK、エラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e19438b6320c0ed66083690cfb425d5d7656ecea
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881896"
---
# <a name="troubleshooting-gdl-parsing"></a>GDL 解析のトラブルシューティング

ここでは、GDL ファイルの解析時に発生する可能性がある予期しない動作のいくつかの原因について説明します。

<a href="" id="symptom--you-include-the-schema-file--but-the-parser-emits-an-error-message-that-says---no--root--template-found--gdl-entries-will-not-be--templatized--and-ignores-the-schema---"></a>現象: スキーマファイルが含まれていますが、パーサーは "ルートがありません" テンプレートが見つからないことを示すエラーメッセージを出力し、GDL エントリはテンプレート化されず、スキーマを無視します。   
解決方法: ルートテンプレートが定義されているかどうかを確認します。 このようなテンプレートが定義されている場合は、次の \#が含まれていることを確認します。 gdl ディレクティブは、インスタンスデータの前にあります。 それ以外の場合、パーサーはスキーマを無視します。

<a href="" id="symptom--you-define-an-attribute-multiples-times-in-the-gdl-file--and-i-see-it-appear-in-the-xml-snapshot-only-once---"></a>現象: 属性を GDL ファイルで複数回定義すると、XML スナップショットに1回だけ表示されます。   
解決方法: XML スナップショットに複数回出現する属性については、テンプレートを定義する必要があります。 \*加法ディレクティブを定義する必要があります。 それ以外の場合は、最新の定義のみが表示されます。

<a href="" id="symptom---the-parser-complains-that---production-defined-in-template----template-name---is-not-satisfied-by-actual-construct-----and-it-appears-that-the-number-of-occurrences-of-each-member-is-within-the-bounds-that-the-production-defines-"></a>現象: パーサーは、"テンプレートに定義されている\[運用環境が実際のコンストラクトによって満たされていません" という苦情を示しています。\]"で、各メンバーの出現回数が、実稼働で定義されている境界内にあることが示されます。  
解決方法: まず、GDL パーサーの-i オプションを使用して、各 GDL エントリにバインドされているテンプレートを確認します。 予期したとおりにバインドが行われなかった可能性があります。 バインドが機能しているように見える場合は、実稼働環境で名前が付けられたテンプレートのインスタンスと、名前付きテンプレートから派生した任意のテンプレートの任意のインスタンスによって、実稼働が満たされていることに注意してください。 そのため、実稼働環境で特定のテンプレートのインスタンスが1つしか存在しないことを指定し、実際のデータファイルにそのテンプレートから派生したテンプレートの2つのインスタンスが含まれている場合は、運用環境に違反します。 テンプレートの継承は、派生テンプレートが \*Name ディレクティブを再定義する場合でも追跡されます。

<a href="" id="symptom--you-receive-a-warning-message-that-references-an--invalidcombination-that-does-not-exist-in-the-gdl-file-that-is-being-parsed-"></a>現象: 解析中の GDL ファイルに存在しない \*InvalidCombination を参照する警告メッセージが表示されます。  
解決策: GDL パーサーは、\*制約ディレクティブを内部で \*InvalidCombination ディレクティブに変換します。 そのため、変換後にエラーが検出された場合、メッセージは、\*InvalidCombination として \*制約を参照します。 また、\*InvalidCombination の各要素が内部で格納される順序は、必ずしも GDL ファイルで指定されている順序とは限りません。

<a href="" id="symptom--spurious-trailing-space-appears-when-a-value-macro-reference-is-replaced-with-its-defined-value-"></a>現象: 値のマクロ参照が定義された値に置き換えられると、誤った末尾のスペースが表示されます。  
解決方法: 値マクロ定義には、末尾のコメントが含まれています。 コメントを別の行に移動します。 ほとんどの場合、パーサーは追加のスペース文字が存在することを認識しません。

<a href="" id="symptom---surrounding-non-conforming-syntax-with-a--ignoreblock-construct-does-not-hide-the-content-from-the-parser-as-syntax-errors-are-still-generated-"></a>現象: 非準拠の構文を \*IgnoreBlock コンストラクトと共に使用しても、構文エラーが生成されるため、パーサーのコンテンツは非表示になりません。  
解決方法: \*IgnoreBlock の内容は、引き続き GDL に準拠している必要があります。 \*IgnoreBlock は、その内容が内部データツリーに表示されないようにし、非プリプロセッサディレクティブが実行されないようにします。 本当に何かを非表示にするには、プリプロセッサ条件を使用します。 非表示にするフラグメントに、実行してはいけないプリプロセッサディレクティブが含まれている場合は、プリプロセッサの条件でフラグメントを囲む直前にプリプロセッサのプレフィックスを変更します。

<a href="" id="symptom---features--constructs--and-attributes-that-are-defined-within-files-that-are-designated-with--precompiled-do-not-appear-in-the-xml-snapshot-and-cannot-be-referenced-by-the-host-file-"></a>現象: \*プリコンパイル済みとして指定されたファイル内で定義されている機能、コンストラクト、および属性は、XML スナップショットには表示されず、ホストファイルから参照することもできません。  
解決方法: この現象は、設計によって発生します。 プリコンパイル済みファイル内には、テンプレートとマクロの定義のみを格納できます。

<a href="" id="symptom---you-cannot-reference-templates--preprocessor-defines--macros--or-other-content-that-is-defined-elsewhere-from-within-files-that-are-designated-with--precompiled--"></a>現象: テンプレート、プリプロセッサ定義、マクロ、または他の場所で定義された他のコンテンツを、\*プリコンパイルされたで指定されたファイルから参照することはできません。   
解決方法: この現象は、設計によって発生します。 プリコンパイル済みファイルは、ホストファイルのコンテキストから完全に独立した、自己完結型であるように設計されています。 別のファイルで定義されているテンプレートまたはその他のコンテンツにアクセスするには、そのファイルを \#プリコンパイル済みファイルに直接付ける \#Include ディレクティブを配置する必要があります。 \#インクルードファイル (つまり入れ子になった \#Include ステートメント) 内に含まれている (\#インクルードを使用した) ことによって間接的に含まれているコンテンツは、ルートプリコンパイル済み (\#プリコンパイル済み) ファイルによってアクセスできます。 プリコンパイルされたファイルには、他のプリコンパイル済みファイルを \#インクルードすることによって含めることができます。

<a href="" id="symptom---features-or-options-do-not-appear-in-the-snapshot-in-the-order-that-you-defined-them---or--the-first-option-is-not-assigned-as-the-default-option---"></a>現象: 機能またはオプションは、定義した順序でスナップショットに表示されません。 または、最初のオプションが既定のオプションとして割り当てられていません。   
解決方法: いくつかのオプションは、GDL ファイルの別の部分で定義されている場合や、参照している機能またはオプションの定義の前に処理されたインクルードファイル内で定義されている場合があります。 最初に処理されるオプションは、最初のオプションになります。処理される2番目のオプションは、スナップショットの2番目のオプションになります。

<a href="" id="symptom--you-receive-a-warning-message-that-says-that-the-gdl-parser-cannot-find-a-template-that-is-referenced-by-the--elementtype-directive--but-that-template-is-defined--"></a>現象: \*ElementType ディレクティブによって参照されているが、そのテンプレートが定義されているテンプレートが見つからないことを示す警告メッセージが表示されます。   
解決方法: \*ElementType ディレクティブで参照できるのは、\*Type: DATATYPE として宣言されているテンプレートだけです。

<a href="" id="symptom--values-of-attributes-that-are-defined-to-be--filtertypename---codepage-string--are-not-converted-to-unicode-properly---"></a>現象: \*FilterTypeName: "CODEPAGE\_STRING" として定義されている属性の値は、Unicode に正しく変換されません。   
解決方法: この属性の解析時に \*CodePage ディレクティブが定義されていない場合、パーサーは文字列が既に Unicode に含まれていると想定します。 コードページの\_文字列属性の前に、\*のコードページ定義が表示されていることを確認してください。

<a href="" id="symptom--you-defined-the--requireddelimiter-in-your-array-or-composite-data-type-template-to-be-a-sequence-of-multiple-space-characters-or-tabs--and-the-parser-does-not-seem-to-recognize-the-actual-data-even-though-it-conforms-exactly-to-the-template-definition---"></a>現象: 配列または複合データ型テンプレートの \*RequiredDelimiter を複数のスペース文字またはタブのシーケンスとして定義したため、テンプレート定義に厳密に準拠している場合でも、パーサーは実際のデータを認識しないように思われます。   
解決方法: パーサーは、空白 (スペースまたはタブ文字) の任意の文字列を内部で1つの空白文字に変換します。 そのため、値がチェックされると、テンプレート定義は満たされません。 このような状況を回避するには、\*RequiredDelimiter に空白文字を1つだけ指定するか、\*RequiredDelimiter に空白以外の文字を使用し、\*の省略記号としてスペースとタブ文字を使用します。

<a href="" id="symptom--dom-interface---xpath-query-cannot-find-any-elements-in-the-snapshot---for-example--selectsinglenode---snapshotroot-gdl-attribute----returns-nothing--"></a>現象: DOM interface: Xpath クエリはスナップショット内の要素を見つけることができません (たとえば、selectSingleNode ("/SnapshotRoot/GDL\_ATTRIBUTE") は nothing を返します)。  
解決策: Xpath では、名前空間プレフィックスのない要素名が、既定の名前空間ではなく、null または空の名前空間を参照することを想定しています。 スナップショットは既定の名前空間を定義し、ほとんどの要素は既定の名前空間に属します。

Xpath を使用してこれらの要素にアクセスするには、クライアントはまず、この既定の名前空間を明示的なプレフィックスにマップする必要があります。 この方法で既定の名前空間をマップするには、document pbjects setProperty メソッドを使用します。 設定が必要なプロパティは、SelectionNamespaces です。 このプロパティを使用して、既定の名前空間明示的なプレフィックスを割り当てます。 スナップショットでは、既定の名前空間が[http://schemas.microsoft.com/2002/print/gdl/1.0](https://schemas.microsoft.com/2002/print/gdl/1.0)ため、setProperty の呼び出しは次のコード例のようになります。

```cpp
XMLDoc->setProperty(L"SelectionNamespaces", "xmlns:gdl=\"http://schemas.microsoft.com/2002/print/gdl/1.0\"");
```

前の例の2番目の引数は実際にはバリアントですが、わかりやすくするために、この追加の複雑さは省略されています。 Xpath クエリでは、既定の名前空間の要素を参照するときに、名前空間プレフィックス gdl を明示的に参照する必要があります。 クエリは次のコード例になります。

```cpp
selectSingleNode("/gdl:SnapshotRoot/gdl:GDL_ATTRIBUTE")
```

<a href="" id="symptom--the-dom-interface---nodetypedvalue-property-always-returns-values-as-bstr-types--regardless-of-their-xsi-type--"></a>現象: DOM interface: nodeTypedValue プロパティは、xsi: type に関係なく、常に値を BSTR 型として返します。   
解決方法: MSXML 4.0 の現在の実装では、データ型定義 (DTD) を使用して定義されている場合にのみ、データ型が認識されます。 GDL パーサーは、現在の W3C 勧告である XSD を使用します。

<a href="" id="symptom--quoted-strings-that-contain-characters-with-ansi-values-between-0-and-0x19-cause-xml-parsing-errors---except-for-0x0a--0x0d--and-0x09--"></a>現象: ANSI 値が 0 ~ 0x19 の文字を含む引用符で囲まれた文字列では、XML 解析エラーが発生します (0x0a、0x0d、0x09 を除く)。  
解決方法: このエラーは XML 機能です。 このような文字列は、XML のバイナリまたは binhex データ形式を使用して表す必要があります。 将来のバージョンの XML では、これらの文字を含む文字列を受け入れることができます。

<a href="" id="symptom--some-xml-instance-data-or-schema-that-are-defined-by-using-the-passthrough-or-xsd-defined-data-types-cause-xml-parser-or-validation-error-messages-when-loaded-into-dom-"></a>現象: パススルーまたは XSD\_定義されたデータ型を使用して定義されている XML インスタンスデータまたはスキーマによっては、DOM に読み込まれるときに XML パーサーまたは検証エラーメッセージが発生することがあります。  
解決方法: パススルーまたは XSD の\_定義されたデータ型を使用して独自の XML を作成すると、GDL パーサーの XML 生成コードがバイパスされ、DOM parser での XML の複雑さや特性が明らかになります。 これらのデータ型を使用する前に、XML を使用してこのような問題に対処する必要があります。

<a href="" id="symptom---the-parser-says--preface-cannot-be-used-with-a-precompiled-file---but-the-root-file-does-not-contain-a--precompiled-directive-"></a>現象: パーサーは、"先頭をプリコンパイルされたファイルでは使用できません" と表示されますが、ルートファイルには \#のプリコンパイル済みディレクティブが含まれていません。  
解決方法: \#プリコンパイルされたディレクティブは、実際には先頭に前に配置されている場合があります。 パーサーは、GDL コンテンツが先頭またはルートファイルからのものであるかどうかを区別できません。
