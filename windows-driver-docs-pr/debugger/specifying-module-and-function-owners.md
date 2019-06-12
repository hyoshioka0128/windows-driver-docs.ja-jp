---
title: モジュールおよび関数所有者の指定
description: モジュールおよび関数所有者の指定
ms.assetid: be227712-7f70-4e74-b090-ca8b3ecd1e13
keywords:
- 実行可能ファイルとパス、モジュールの所有者を指定します。
- 関数の所有者
- モジュールと関数の所有者
- triage.ini ファイル
- triage.ini ファイル、構文
- 拡張機能、triage.ini ファイルを分析します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f27077d9553a11a96755abf3eb6897496bad6040
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368081"
---
# <a name="specifying-module-and-function-owners"></a>モジュールおよび関数所有者の指定


## <span id="ddk_specifying_module_and_function_owners_dbg"></span><span id="DDK_SPECIFYING_MODULE_AND_FUNCTION_OWNERS_DBG"></span>


**! 分析**と **! 所有者**拡張機能は、デバッガーがシンボルの所有者を決定する Triage.ini がという名前のファイルを使用します。

これらの拡張機能を使用する場合は、「フォロー アップ」という単語の後、関数またはモジュールの所有者の id が表示されます。

Triage.ini ファイルはテキスト ファイル内にある、\\ツールを Windows のデバッグ インストールのサブディレクトリをトリアージします。 Triage.ini ファイルのサンプルは、Windows のツールをデバッグ パッケージの一部として含まれています。

**警告**   Triage.ini を含めて、そのディレクトリ内のファイルのすべてが上書きされますが、現在のバージョンと同じディレクトリ内の Windows 内のデバッグ ツールの更新バージョンをインストールする場合。 変更するサンプル Triage.ini ファイルを置換するか後、は、別のディレクトリに、そのコピーを保存します。 デバッガーを再インストールした後は、既定のバージョンを保存した Triage.ini をコピーできます。

 

### <a name="span-idformatofthetriageinifilespanspan-idformatofthetriageinifilespanformat-of-the-triageini-file"></a><span id="format_of_the_triage_ini_file"></span><span id="FORMAT_OF_THE_TRIAGE_INI_FILE"></span>Triage.ini ファイルの形式

デバッガーに分割する関数の所有者を判断するのに役立つ Triage.ini ファイルが意図したものがこのファイル内の「所有者」文字列はデバッグに役立つ任意に指定できます。 文字列には、記述したコードの管理人の名前を指定できます。 または、文字列が短い手順モジュールまたは関数でエラーが発生したときに操作できる内容についての説明を指定できます。

このファイル内の各行には、次の構文があります。

```dbgcmd
Module[!Function]=Owner 
```

アスタリスクを追加することができます (\*) モジュールまたは関数名の末尾でのみです。 別の場所が表示される場合は、リテラル文字として解釈されます。

所有者の文字列では、空間を追加することはできません。 スペース、所有者の文字列で存在する場合は無視されます。

構文オプションの詳細については、特別な Triage.ini 構文を参照してください。

次の例では、Triage.ini ファイルのサンプルを示します。

```ini
module1=Person1
module2!functionA=Person2
module2!functionB=Person3
module2!funct*=Person4
module2!*=Person5
module3!singleFunction=Person6
mod*!functionC=Person7
```

### <a name="span-idtriageiniandownerspanspan-idtriageiniandownerspan-triageini-and-owner"></a><span id="triage_ini_and__owner"></span><span id="TRIAGE_INI_AND__OWNER"></span> Triage.ini と! 所有者

モジュールまたは関数の名前を渡す場合、 [ **! 所有者**](-owner.md)拡張機能では、デバッガー、モジュールまたは関数の所有者の名前の後に「フォロー アップ」という単語が表示されます。

次の例では、前のサンプル Triage.ini ファイルを使用します。

```dbgcmd
0:000> !owner module2!functionB
Followup:  Person3
```

"Person3"を所有するファイルによる**module2! functionB**、"Person4"所有している**module2! 関数\\** <em>します。これらの文字列の両方の一致に渡される引数 * *! 所有者</em>* のでより完全な一致を使用します。

### <a name="span-idtriageiniandanalyzespanspan-idtriageiniandanalyzespan-triageini-and-analyze"></a><span id="triage_ini_and__analyze"></span><span id="TRIAGE_INI_AND__ANALYZE"></span> Triage.ini と! 分析

使用すると、 [ **! 分析**](-analyze.md)拡張機能では、デバッガーはエラーのスタック フレームの上部にある検索し、このフレームの関数、モジュールの所有者を特定しようとしています。 デバッガーでは、所有者を決定できます、所有者の情報が表示されます。

デバッガーが、所有者を識別できない場合、デバッガーは、次のスタック フレームに渡すし、に、デバッガーは、所有者またはスタックを判断するまでは完全に確認します。

デバッガーでは、所有者を決定できます、「フォロー アップ」という単語の後、所有者名が表示されます。 デバッガーでは、スタック全体を検索、情報を検索することがなく、名前は表示されません。

次の例では、このトピックで既に指定されているサンプル Triage.ini ファイルを使用します。

最初のスタック フレームが**MyModule! someFunction**します。 デバッガーが見つからない**MyModule** Triage.ini ファイル。 次に、スタック上の 2 つ目のフレームを続行します。

2 番目のフレームが**module3! anotherFunction**します。 エントリが表示されますが、デバッガー **module3**に一致するものはありませんが、 **anotherFunction**このモジュールにします。 次に、デバッガーは、3 つ目のフレームが続行されます。

3 番目のフレームが**module2! 関数 c**します。 デバッガーは最初に、完全に一致するが、一致するものが存在しません。 デバッガーは関数名のトリムし、検出**module2! 関数\\** * Triage.ini でします。 この照合は、デバッガーは、所有者が"Person4"を指定するために、検索を終了します。

デバッガーでは、次の例では、次のような出力が表示されます。

```dbgcmd
0:000> !analyze
*******************************************************************************
*                                                                             *
*                        Exception Analysis                                   *
*                                                                             *
*******************************************************************************

Use !analyze -v to get detailed debugging information.

Probably caused by : module2 ( module2!functionC+15a )

Followup: Person4
---------
```

完全な一致より短い一致よりも優先されます。 ただし、モジュールの名前の一致では、関数名と一致するをお勧めは常にします。 場合**module2! 関数\\** * していないのデバッガーは選択したこの Triage.ini ファイルで**module2!\\** * が一致しています。 どちらの場合と**module2! 関数\\** * と**module2!\\** * 削除された**mod\*! 関数 c**に選択します。

### <a name="span-idspecialtriageinisyntaxspanspan-idspecialtriageinisyntaxspanspecial-triageini-syntax"></a><span id="special_triage_ini_syntax"></span><span id="SPECIAL_TRIAGE_INI_SYNTAX"></span>特別な Triage.ini 構文

感嘆符と関数名を省略するか、追加かどうか **!\\** * モジュール名の後に、そのモジュール内のすべての関数が示されます。 このモジュール内で関数が個別に指定されてより正確な仕様が優先されます。

モジュールまたは関数名として"default"を使用する場合は、ワイルドカード文字と同じです。 たとえば、 **nt!\\** * と同じ**nt! 既定**、および**既定**と同じでは、* *\*!\\***.

単語が、一致が行われた場合**無視**デバッガーが、スタック内の次のフレームを引き続き等号 (=) の右側に表示されます。

追加することができます**最後\_** または**かもしれません\_** 所有者の名前の前にします。 このプレフィックスが優先所有者以下を実行すると **! 分析**します。 デバッガーが経由でスタックの下位にある確実な一致を選択、**かもしれません\_** スタックの上位に対応します。 デバッガーが選択することも、**かもしれません\_** 経由でスタックの下位にある一致、**最後\_** スタックの上位に対応します。

### <a name="span-idsampletriageinispanspan-idsampletriageinispansample-triageini"></a><span id="sample_triage_ini"></span><span id="SAMPLE_TRIAGE_INI"></span>サンプル Triage.ini

Triage.ini テンプレートのサンプルは、Windows のツールをデバッグ パッケージに含まれます。 このファイルには、任意のモジュールとする関数の所有者を追加できます。 グローバルな既定値がない場合は、削除、**既定 = MachineOwner**このファイルの先頭行。

 

 





