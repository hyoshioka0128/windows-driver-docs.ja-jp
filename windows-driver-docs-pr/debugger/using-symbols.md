---
title: シンボルの使用
description: シンボルの使用
ms.assetid: 1de1441f-b4d7-49e9-87ad-392a75b3d4be
keywords:
- デバッガーエンジン、シンボル
- 文字
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8763269c8fd8a8d17996879b54ca494d46cf37d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838801"
---
# <a name="using-symbols"></a>シンボルの使用


## <span id="ddk_symbols_dbx"></span><span id="DDK_SYMBOLS_DBX"></span>


シンボルファイルやシンボルサーバーの使用など、シンボルの概要については、「[シンボル](symbols.md)」を参照してください。

### <a name="span-idsymbol_names_and_locationsspanspan-idsymbol_names_and_locationsspansymbol-names-and-locations"></a><span id="symbol_names_and_locations"></span><span id="SYMBOL_NAMES_AND_LOCATIONS"></span>シンボル名と場所

名前を指定してシンボルの場所を検索するには、 [**GetOffsetByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getoffsetbyname)を使用します。 シンボル名の指定に使用される構文の詳細については、「[シンボルの構文とシンボルの一致](symbol-syntax-and-symbol-matching.md)」を参照してください。

シンボルの正確な名前がわからない場合、または複数の記号が同じ名前の場合、 [**Startsymbol match**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-startsymbolmatch)は、指定されたパターンに一致する名前を持つシンボルの検索を開始します。 構文の詳細については、「[文字列ワイルドカード構文](string-wildcard-syntax.md)」を参照してください。

場所を指定してシンボルの名前を検索するには、 [**Getnamebyoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getnamebyoffset)を使用します。 指定された場所付近のモジュールのシンボル名を検索するには、 [**GetNearNamebyOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getnearnamebyoffset)を使用します。

**注**   できる限り、シンボルをモジュール名で修飾してください (例: **mymodule! main**)。 そうしないと、シンボルが存在しない場合 (たとえば、タイポグラフィエラーが発生した場合)、エンジンはすべてのモジュールのシンボルを読み込んで検索する必要があります。これは、特にカーネルモードのデバッグでは、処理が遅くなることがあります。 シンボル名がモジュール名で修飾されている場合、エンジンはそのモジュールのシンボルのみを検索する必要があります。

 

シンボルは、structure [**DEBUG\_MODULE\_と\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_module_and_id)を使用して一意に識別されます。 この構造体は、メソッド[**GetSymbolEntriesByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentriesbyname)と[**Getsymbols byoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentriesbyoffset)によって返されます。このメソッドは、それぞれの名前と場所に基づいてシンボルを検索します。

[**Getsymbol Entryinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentryinformation)メソッドは、[**デバッグ\_シンボル\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_symbol_entry)構造を使用してシンボルの説明を返します。

構造体内のフィールドのオフセットを調べるには、 [**GetFieldOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols-getfieldoffset)を使用します。 構造体内でインデックスが指定されているフィールドの名前を検索するには、 [**Getfieldname**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getfieldname)を使用します。 値を指定して列挙定数の名前を検索するには、 [**GetConstantName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getconstantname)を使用します。

[**Getsymbols information**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-getsymbolinformation)メソッドは、シンボルに関する情報に対して複数の要求を実行できます。

### <a name="span-idsymbol_optionsspanspan-idsymbol_optionsspansymbol-options"></a><span id="symbol_options"></span><span id="SYMBOL_OPTIONS"></span>シンボルのオプション

いくつかのオプションで、シンボルの読み込みとアンロードの方法を制御します。 これらのオプションの詳細については、「[シンボルオプションの設定](symbol-options.md)」を参照してください。

シンボルオプションは、 [**AddSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-addsymboloptions)を使用して有効にし、 [**RemoveSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-removesymboloptions)を使用して無効にすることができます。

[**GetSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymboloptions)は、現在のシンボルオプションを返します。 すべてのシンボルオプションを一度に設定するには、 [**SetSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setsymboloptions)を使用します。

### <a name="span-idreloading_symbolsspanspan-idreloading_symbolsspanreloading-symbols"></a><span id="reloading_symbols"></span><span id="RELOADING_SYMBOLS"></span>再読み込み (シンボルを)

シンボルファイルを読み込んだ後、エンジンはシンボル情報を内部キャッシュに格納します。 このキャッシュをフラッシュするには、 [**Reload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-reload)を使用します。 これらのシンボルは、後で再度読み込むか、後で読み込む必要があります。

### <a name="span-idsynthetic_symbolsspanspan-idsynthetic_symbolsspan-synthetic-symbols"></a><span id="synthetic_symbols"></span><span id="SYNTHETIC_SYMBOLS"></span>合成シンボル

*合成シンボル*は、簡単に参照できるように任意のアドレスにラベルを付ける方法です。 合成シンボルは、任意の既存のモジュールで作成できます。 新しい合成[**シンボルが作成され**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-addsyntheticsymbol)ます。 合成シンボルは、 [**RemoveSyntheticSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-removesyntheticsymbol)を使用して削除できます。 モジュールのシンボルを再読み込みすると、そのモジュールに関連付けられているすべての合成シンボルが削除されます。

### <a name="span-idsymbol_pathspanspan-idsymbol_pathspansymbol-path"></a><span id="symbol_path"></span><span id="SYMBOL_PATH"></span>シンボルパス

シンボルパスにディレクトリまたはシンボルサーバーを追加するには、 [**Appendsymbol path**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-appendsymbolpath)メソッドを使用します。 シンボルパス全体は[**Getsymbol path**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolpath)によって返され、 [**setsymbol path**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setsymbolpath)を使用して変更できます。

 

 





