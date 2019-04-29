---
title: GDL 解析のトラブルシューティング
description: GDL 解析のトラブルシューティング
ms.assetid: 8c678a2f-b15b-4693-9bed-0edec06b3485
keywords:
- GDL WDK、パーサー
- パーサー WDK GDL、解析のトラブルシューティング
- WDK GDL データの解析
- WDK の解析 GDL のトラブルシューティング
- GDL WDK、解析エラー
- GDL WDK、エラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8a060a271f712cce685299b3d6b81ce52592cf9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392783"
---
# <a name="troubleshooting-gdl-parsing"></a>GDL 解析のトラブルシューティング


次の情報には、GDL ファイルを解析するときに発生する可能性のある予期しない動作の原因の一部について説明します。

<a href="" id="symptom--you-include-the-schema-file--but-the-parser-emits-an-error-message-that-says---no--root--template-found--gdl-entries-will-not-be--templatized--and-ignores-the-schema---"></a>現象:スキーマ ファイルが含まれますが、パーサーが"'ROOT' テンプレートが見つからない GDL エントリはテンプレート化されていない"ことを示すエラー メッセージを出力し、スキーマを無視します。   
解決策:ルート テンプレートが定義されているかどうかを確認します。 このようなテンプレートが定義されている場合ことを確認します。、 \#Include: schema.gdl ディレクティブは、インスタンス データの前にします。 それ以外の場合、パーサーは、スキーマを無視します。

<a href="" id="symptom--you-define-an-attribute-multiples-times-in-the-gdl-file--and-i-see-it-appear-in-the-xml-snapshot-only-once---"></a>現象:GDL ファイルで属性の複数回を定義して、表示、XML のスナップショットを 1 回だけに表示されます。   
解決策:複数回を XML のスナップショットに表示される任意の属性用のテンプレートを定義する必要があります。 定義する必要があります、\*加法ディレクティブ。 それ以外の場合、最新の定義のみが表示されます。

<a href="" id="symptom---the-parser-complains-that---production-defined-in-template----template-name---is-not-satisfied-by-actual-construct-----and-it-appears-that-the-number-of-occurrences-of-each-member-is-within-the-bounds-that-the-production-defines-"></a>現象:パーサーという苦情"\[テンプレートで定義されている運用環境:「{テンプレート名}」は実際の構成要素によって満たされていない\]"、運用環境を定義する範囲内の各メンバーの出現回数が表示されます。  
解決策:最初に、確認 -i を使用して各 GDL エントリにどのようなテンプレートがバインドされて GDL パーサーのオプション。 バインドしない予想する方法発生した可能性があります。 バインディングが成功したと表示されている場合は、名前付きのテンプレートから派生した任意のテンプレートの任意のインスタンスと、運用環境でという名前のテンプレートのインスタンスによって、運用環境が満たしている注意してください。 そのため、運用環境は、特定のテンプレートの 1 つだけのインスタンスが存在して、実際のデータ ファイルにそのテンプレートから派生したテンプレートの 2 つのインスタンスが含まれている場合、運用環境が違反されることを指定します。 場合でも、派生テンプレートを再定義テンプレート継承が追跡、\*ディレクティブの名前。

<a href="" id="symptom--you-receive-a-warning-message-that-references-an--invalidcombination-that-does-not-exist-in-the-gdl-file-that-is-being-parsed-"></a>現象:参照する警告メッセージが表示されたら、 \*InvalidCombination GDL ファイル解析中に存在しません。  
解決策:GDL パーサーに変換します\*に制約ディレクティブ\*InvalidCombination ディレクティブ内部的にします。 そのため、変換後にエラーが検出されると、メッセージが参照する、\*制約として、 \*InvalidCombination します。 また、注文の各要素を\*InvalidCombination が内部的に格納されている GDL ファイルで指定されている順序とは限りません。

<a href="" id="symptom--spurious-trailing-space-appears-when-a-value-macro-reference-is-replaced-with-its-defined-value-"></a>現象:マクロ参照を値が、定義済みの値に置き換えられます誤った、末尾にスペースが表示されます。  
解決策:値のマクロ定義には、末尾のコメントが含まれています。 個別の行にコメントを移動します。 ほとんどのコンテキストでは、パーサーは追加のスペース文字が存在する機密性の高いではありません。

<a href="" id="symptom---surrounding-non-conforming-syntax-with-a--ignoreblock-construct-does-not-hide-the-content-from-the-parser-as-syntax-errors-are-still-generated-"></a>現象:構文と非準拠の周囲を\*ように構文エラーが引き続き生成 IgnoreBlock コンストラクトは、パーサーからコンテンツを非します。  
解決策:内容\*IgnoreBlock が GDL を準拠したもする必要があります。 \*IgnoreBlock は、その内容が内部データのツリーに表示されないようにし、非プリプロセッサ ディレクティブが実行されていることを防ぐだけです。 本当に何かを非表示に、プリプロセッサ条件を使用します。 非表示に自体をフラグメントには実行されませんがプリプロセッサ ディレクティブが含まれている場合は、プリプロセッサ条件付きでフラグメントの外側の直前にプリプロセッサのプレフィックスを変更します。

<a href="" id="symptom---features--constructs--and-attributes-that-are-defined-within-files-that-are-designated-with--precompiled-do-not-appear-in-the-xml-snapshot-and-cannot-be-referenced-by-the-host-file-"></a>現象:機能、コンストラクト、および属性で指定されているファイル内で定義されている\*プリコンパイル済みの XML スナップショットでは表示されず、ホスト ファイルで参照することはできません。  
解決策:この現象は、デザインによって発生します。 テンプレートとプリコンパイル済みファイル内のマクロ定義のみを格納することができます。

<a href="" id="symptom---you-cannot-reference-templates--preprocessor-defines--macros--or-other-content-that-is-defined-elsewhere-from-within-files-that-are-designated-with--precompiled--"></a>現象:テンプレートを参照することはできません、プリプロセッサの定義、マクロ、またはその他のコンテンツで指定されているファイル内から他の場所で定義されている\*プリコンパイル済み。   
解決策:この現象は、デザインによって発生します。 プリコンパイル済みファイルは自己完結型で、ホスト ファイルのコンテキストの完全に独立して設計されています。 テンプレートまたは別のファイルで定義されているその他のコンテンツにアクセスすることを配置する必要があります、 \#Include ディレクティブ内で直接そのファイルの名前を示す、\#プリコンパイル済みファイル。 含まれるによって間接的に含まれているコンテンツ (を使用して\#Include) 内で、\#インクルード ファイル (つまり、入れ子になった\#ステートメントを含める) プリコンパイル済みのルートからアクセス可能になります (\#プリコンパイル済み) ファイルです。 プリコンパイル済みファイルを含めることができます (を使用して\#Include) その他のプリコンパイル済みファイル。

<a href="" id="symptom---features-or-options-do-not-appear-in-the-snapshot-in-the-order-that-you-defined-them---or--the-first-option-is-not-assigned-as-the-default-option---"></a>現象:機能やオプションは、定義した順序でスナップショットには表示されません。 または、最初のオプションが既定のオプションとして割り当てられていません。   
解決策:いくつかのオプションがありますが定義されていた GDL ファイルの別の部分か、機能する前に処理されたインクルード ファイルまたはが表示されているオプションの定義。 処理される最初のオプションが最初のオプションになり、処理が 2 番目のオプションが、スナップショットでは、2 番目のオプションになります。

<a href="" id="symptom--you-receive-a-warning-message-that-says-that-the-gdl-parser-cannot-find-a-template-that-is-referenced-by-the--elementtype-directive--but-that-template-is-defined--"></a>現象:GDL パーサーによって参照されているテンプレートが見つからないことを示す警告メッセージが表示されたら、 \*ElementType のディレクティブが、そのテンプレートを定義します。   
解決策:として宣言されているテンプレートだけ\*型。データ型を参照できます、 \*ElementType ディレクティブ。

<a href="" id="symptom--values-of-attributes-that-are-defined-to-be--filtertypename---codepage-string--are-not-converted-to-unicode-properly---"></a>現象:定義されている属性の値\*FilterTypeName:"コードページ\_文字列"Unicode に正しく変換されません。   
解決策:場合、 \*CodePage ディレクティブがこの属性は解析時に定義されていない、パーサーは、文字列が Unicode で既にが前提としています。 確認、\*コードページ定義は、任意のコード ページの前に表示されます。\_文字列属性。

<a href="" id="symptom--you-defined-the--requireddelimiter-in-your-array-or-composite-data-type-template-to-be-a-sequence-of-multiple-space-characters-or-tabs--and-the-parser-does-not-seem-to-recognize-the-actual-data-even-though-it-conforms-exactly-to-the-template-definition---"></a>現象:定義した、\*複数の空白文字またはタブ、およびパーサーのシーケンスを配列または複合データ型のテンプレートで RequiredDelimiter は正確にテンプレートの定義に準拠している場合でも、実際のデータを認識していません。   
解決策:パーサーでは、空白 (スペースまたはタブ文字) の任意の文字列が単一の空白文字に内部的に変換します。 その値がオンになっているを満たしていませんテンプレートの定義。 このような状況を避けるためには、指定の 1 つだけの空白文字、 \*RequiredDelimiter、または使用して、空白以外の文字を\*RequiredDelimiter のスペースやタブ文字を使用して、 \*OptionalDelimiter します。

<a href="" id="symptom--dom-interface---xpath-query-cannot-find-any-elements-in-the-snapshot---for-example--selectsinglenode---snapshotroot-gdl-attribute----returns-nothing--"></a>現象:DOM インターフェイス:Xpath クエリでは、スナップショット内の要素が見つからない (たとえば、selectSingleNode ("/SnapshotRoot/GDL\_属性") は何も返しません)。  
解決策:Xpath では、その要素名前なし名前空間プレフィックスを null または空名前空間を参照、既定の名前空間ではないと仮定します。 スナップショットが既定の名前空間を定義し、ほとんどの要素が既定の名前空間に属しています。

Xpath を使用してこれらの要素にアクセスするに、クライアントはこの既定の名前空間を明示的なプレフィックスにマップする必要があります最初。 この方法で既定の名前空間をマップするには、ドキュメントの pbjects setProperty メソッドを使用します。 プロパティを設定する必要があるとは、SelectionNamespaces です。 このプロパティを使用して、既定の名前空間を明示的なプレフィックスを割り当てます。 既定の名前空間には、スナップショットに http://schemas.microsoft.com/2002/print/gdl/1.0ように setProperty への呼び出しは次のコード例のようになります。

```cpp
XMLDoc->setProperty(L"SelectionNamespaces", "xmlns:gdl=\"http://schemas.microsoft.com/2002/print/gdl/1.0\"");
```

前の例では、2 番目の引数が実際にはバリアント型が、この複雑さを増すがわかりやすくするため省略されます。 Xpath クエリする必要があります今すぐを明示的に参照名前空間プレフィックスの gdl 既定の名前空間内の要素を参照するときにします。 クエリには、次のコード例になります。

```cpp
selectSingleNode("/gdl:SnapshotRoot/gdl:GDL_ATTRIBUTE")
```

<a href="" id="symptom--the-dom-interface---nodetypedvalue-property-always-returns-values-as-bstr-types--regardless-of-their-xsi-type--"></a>現象:DOM インターフェイス: nodeTypedValue プロパティは常に、xsi:type に関係なく、BSTR 型として値を返します。   
解決策:MSXML 4.0 の現在の実装は、データ型定義 (DTD) を使用して定義されると、専用のデータ型を認識します。 GDL パーサーでは、XSD で、現在の W3C recommendation を使用します。

<a href="" id="symptom--quoted-strings-that-contain-characters-with-ansi-values-between-0-and-0x19-cause-xml-parsing-errors---except-for-0x0a--0x0d--and-0x09--"></a>現象:ANSI 値 0 と 0x19 の間の文字が含まれている引用符で囲まれた文字列には、XML の解析 (0x0a、0x0d、0x09 以外) のエラーが発生します。  
解決策:このエラーは、XML 機能です。 このような文字列は、XML のバイナリまたは binhex データ形式を使用して表す必要があります。 XML の将来のバージョンでは、これらの文字を含む文字列を受け入れることがあります。

<a href="" id="symptom--some-xml-instance-data-or-schema-that-are-defined-by-using-the-passthrough-or-xsd-defined-data-types-cause-xml-parser-or-validation-error-messages-when-loaded-into-dom-"></a>現象:一部の XML インスタンス データまたはパススルーまたは XSD を使用して定義されているスキーマ\_定義済みのデータ型が XML パーサーや検証 DOM. に読み込まれると、エラー メッセージ  
解決策:パススルーまたは XSD を使用して、独自の XML を作成する\_定義データ型が GDL パーサーの XML の生成コードをバイパスして、複雑な XML や DOM パーサーで quirks を公開しています。 これらのデータ型を使用する前に、このような問題を処理する XML を十分精通している必要があります。

<a href="" id="symptom---the-parser-says--preface-cannot-be-used-with-a-precompiled-file---but-the-root-file-does-not-contain-a--precompiled-directive-"></a>現象:パーサーが「プリコンパイル済みファイルの先頭を使用できません」がルート ファイルを含まない、\#プリコンパイル済みディレクティブ。  
解決策:\#プリコンパイル済みディレクティブ可能性があります、先頭自体内にあります。 パーサーは、先頭またはルート ファイルから GDL コンテンツが付属しているかどうかを区別できません。

 

 




