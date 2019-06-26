---
title: シンボルの使用
description: シンボルの使用
ms.assetid: 1de1441f-b4d7-49e9-87ad-392a75b3d4be
keywords:
- デバッガー エンジン、シンボル
- シンボル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46aca9704ee5a17e310f046187d6828eaf0f704b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368614"
---
# <a name="using-symbols"></a>シンボルの使用


## <span id="ddk_symbols_dbx"></span><span id="DDK_SYMBOLS_DBX"></span>


シンボル、シンボル ファイルとシンボル サーバーの使用などの概要については、次を参照してください。[シンボル](symbols.md)します。

### <a name="span-idsymbolnamesandlocationsspanspan-idsymbolnamesandlocationsspansymbol-names-and-locations"></a><span id="symbol_names_and_locations"></span><span id="SYMBOL_NAMES_AND_LOCATIONS"></span>シンボルの名前と場所

指定した名前のシンボルの場所を検索する使用[ **GetOffsetByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getoffsetbyname)します。 シンボル名を指定するために使用する構文の詳細については、「[シンボルの構文と一致するシンボル](symbol-syntax-and-symbol-matching.md)します。

シンボルの正確な名前が不明、または複数のシンボルが同じ名前を持つ場合[ **StartSymbolMatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-startsymbolmatch)名前を持つ指定したパターンに一致するシンボルの検索を開始します。 構文の詳細については、次を参照してください。[文字列のワイルドカード構文](string-wildcard-syntax.md)します。

その場所が指定されたシンボルの名前を確認する[ **GetNameByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getnamebyoffset)します。 特定の場所の近くのモジュールのシンボルの名前を検索するには使用[ **GetNearNamebyOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getnearnamebyoffset)します。

**注**  可能であれば、たとえばモジュール名 - のシンボルを修飾**mymodule! メイン**します。 それ以外の場合、(たとえば、入力ミス エラー) ため、シンボルが存在しない場合、エンジンが読み込むし、すべてのモジュールのシンボルを検索する必要これは、特にカーネル モードのデバッグ用の低速なプロセスです。 モジュールの名前のシンボル名を修飾すると場合、エンジンのみをモジュールのシンボルを検索する必要があります。

 

シンボルの構造を使用して、一意に識別[**デバッグ\_モジュール\_AND\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_module_and_id)します。 この構造体は、メソッドによって返される[ **GetSymbolEntriesByName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentriesbyname)と[ **GetSymbolEntriesByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentriesbyoffset)、検索します。それぞれの名前と場所に基づく記号。

メソッド[ **GetSymbolEntryInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentryinformation)を使用して、シンボルの説明を返します、 [**デバッグ\_シンボル\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_symbol_entry)構造体。

構造体のフィールドのオフセットを確認する[ **GetFieldOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols-getfieldoffset)します。 指定されたインデックス構造内のフィールドの名前を確認する[ **GetFieldName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getfieldname)します。 その値を指定された列挙定数の名前を確認する[ **GetConstantName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getconstantname)します。

メソッド[ **GetSymbolInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-getsymbolinformation)シンボルに関する情報をいくつかの要求を実行できます。

### <a name="span-idsymboloptionsspanspan-idsymboloptionsspansymbol-options"></a><span id="symbol_options"></span><span id="SYMBOL_OPTIONS"></span>シンボルのオプション

さまざまなオプションは、シンボルが読み込まれ、アンロードする方法を制御します。 これらのオプションの説明は、次を参照してください。[シンボル オプションを設定](symbol-options.md)します。

使用してシンボル オプションを有効に[ **AddSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-addsymboloptions)を使用してになっていると[ **RemoveSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-removesymboloptions)します。

[**GetSymbolOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymboloptions)現在のシンボル オプションを返します。 一度にすべてのシンボル オプションを設定するには、使用[ **SetSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-setsymboloptions)します。

### <a name="span-idreloadingsymbolsspanspan-idreloadingsymbolsspanreloading-symbols"></a><span id="reloading_symbols"></span><span id="RELOADING_SYMBOLS"></span>シンボルの再読み込み

シンボル ファイルを読み込んだ後は、エンジンは、内部キャッシュにシンボル情報を格納します。 このキャッシュをフラッシュするには使用[**再読み込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-reload)します。 これらのシンボルは、もう一度今すぐまたは後で読み込まれる必要があります。

### <a name="span-idsyntheticsymbolsspanspan-idsyntheticsymbolsspan-synthetic-symbols"></a><span id="synthetic_symbols"></span><span id="SYNTHETIC_SYMBOLS"></span> 合成のシンボル

*代理シンボル*は簡単に参照を任意のアドレスにラベルを付ける方法です。 任意の既存のモジュールでは、合成のシンボルを作成できます。 メソッド[ **AddSyntheticSymbol** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-addsyntheticsymbol)新しい代理記号を作成します。 使用して代理のシンボルを削除できる[ **RemoveSyntheticSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-removesyntheticsymbol)します。 モジュールのシンボルを再読み込み、そのモジュールに関連付けられているすべての合成シンボルを削除します。

### <a name="span-idsymbolpathspanspan-idsymbolpathspansymbol-path"></a><span id="symbol_path"></span><span id="SYMBOL_PATH"></span>シンボル パス

シンボル パスには、ディレクトリまたはシンボル サーバーを追加するには、メソッドを使用して[ **AppendSymbolPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-appendsymbolpath)します。 全体のシンボル パスがによって返される[ **GetSymbolPath** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolpath)を使用して変更できる[ **SetSymbolPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-setsymbolpath)します。

 

 





