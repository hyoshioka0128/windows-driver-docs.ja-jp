---
title: Windows デバッガーのシンボル パス
description: シンボル パスには、Windows デバッガー (WinDbg、KD、CDB、NTST) がシンボル ファイルを検索する場所を指定します。
ms.assetid: 705df98f-717f-40ad-a424-101826970691
keywords: シンボル ファイルとパス、記号、遅延のシンボルの読み込み、遅延のシンボルの読み込み、シンボル パス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b9b2751df0473c1ddf8f840aa6b705b4de435f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574314"
---
# <a name="symbol-path-for-windows-debuggers"></a>Windows デバッガーのシンボル パス


シンボル パスには、Windows デバッガー (WinDbg、KD、CDB、NTST) がシンボル ファイルを検索する場所を指定します。 シンボルとシンボル ファイルの詳細については、[シンボル](symbols.md)を参照してください。

(Microsoft Visual Studio) などの一部のコンパイラでは、バイナリ ファイルと同じディレクトリにシンボル ファイルを配置します。 シンボル ファイルとバイナリ ファイルがチェックされているパスとファイル名の情報が含まれています。 この情報は、デバッガー シンボル ファイルを自動的に検出を頻繁に使用できます。 実行可能ファイルが作成されたコンピューター上のユーザー モード プロセスをデバッグしている場合、およびシンボル ファイルが元の場所にまだの場合は、デバッガーがシンボル パスを設定することがなく、シンボル ファイルを検索できます。

他のほとんどの場合は、シンボル ファイルの場所を指すシンボル パスを設定する必要があります。

## <a name="span-idsymbolpathsyntaxspanspan-idsymbolpathsyntaxspanspan-idsymbolpathsyntaxspansymbol-path-syntax"></a><span id="Symbol_Path_Syntax"></span><span id="symbol_path_syntax"></span><span id="SYMBOL_PATH_SYNTAX"></span>シンボル パスの構文


デバッガーのシンボル パスは、セミコロンで区切られた複数のディレクトリ パスで構成される文字列です。

相対パスがサポートされています。 ただし、常に同じディレクトリから、デバッガーを起動する場合を除きする必要がありますを追加するドライブ文字またはネットワークの各パスの前に共有します。 ネットワーク共有もサポートされます。

シンボル パスの各ディレクトリに対して、デバッガーは、3 つのディレクトリで検索します。 たとえば、シンボル パスが含まれている場合、`c:\MyDir`ディレクトリ、およびデバッガーが DLL のシンボル情報を探すことで、デバッガーが最初検索`c:\MyDir\symbols\dll`、次に`c:\MyDir\dll`、最後にで`c:\MyDir`。 デバッガーは、シンボル パス内の各ディレクトリにし、このプロセスを繰り返します。 デバッガーが、現在のディレクトリ、現在のディレクトリで次を検索する最後に、`..\dll`が追加されます。 (デバッガーを追加します`..\dll`、 `..\exe` 、または`..\sys`に応じてどのバイナリをデバッグします)。

シンボル ファイルには、日付と時刻のタイムスタンプがあります。 このシーケンスで、最初に検出できるを正しくない記号が、デバッガーを使用するかを心配する必要はありません。 デバッグ バイナリのファイルのタイムスタンプに一致するシンボルを常に検索します。 応答の詳細についてはシンボル ファイルが使用できない場合を参照してください[の問題の一致するシンボル補正](matching-symbol-names.md)します。

シンボル パスを設定する方法の 1 つは、入力して、 [ **.sympath** ](-sympath--set-symbol-path-.md)コマンド。 シンボル パスを設定する他の方法では、[シンボル パスを制御する](#controlling-the-symbol-path)このトピックで後述を参照してください。

## <a name="span-idcachingsymbolslocallyspanspan-idcachingsymbolslocallyspanspan-idcachingsymbolslocallyspancaching-symbols-locally"></a><span id="Caching_Symbols_Locally"></span><span id="caching_symbols_locally"></span><span id="CACHING_SYMBOLS_LOCALLY"></span>ローカル キャッシュにシンボル


常にローカルにシンボルをキャッシュすることを強くお勧めします。 シンボルをキャッシュする方法の 1 つローカルでは、`cache*;`または`cache*localsymbolcache;*`シンボル パス。

文字列を含める場合`cache*;`ローカル コンピューター上の既定のシンボル キャッシュ ディレクトリにシンボル パスにこの文字列の右側に表示される任意の要素から読み込まれたシンボルが格納されています。 次のコマンドがネットワーク共有からシンボルを取得するデバッガーに指示するなど、`\\someshare`し、ローカル コンピューターの既定の場所でシンボルをキャッシュします。

```dbgcmd
.sympath cache*;\\someshare
```

文字列を含める場合`cache*localsymbolcache;`にシンボル パスにこの文字列の右側に表示される任意の要素から読み込まれたシンボルが格納されている、 *localsymbolcache*ディレクトリ。

次のコマンドがネットワーク共有からシンボルを取得するデバッガーに指示するなど、`\\someshare`でシンボルをキャッシュし、`c:\MySymbols`ディレクトリ。

```dbgcmd
.sympath cache*c:\MySymbols;\\someshare
```

## <a name="span-idusingasymbolserverspanspan-idusingasymbolserverspanspan-idusingasymbolserverspanusing-a-symbol-server"></a><span id="Using_a_Symbol_Server"></span><span id="using_a_symbol_server"></span><span id="USING_A_SYMBOL_SERVER"></span>シンボル サーバーの使用


インターネットまたは企業ネットワークに接続している場合、シンボルにアクセスする最も効率的な方法は、シンボル サーバーを使用します。 使用して、シンボル サーバーを使用することができます、 `srv*`、 `srv*symbolstore`、または`srv*localsymbolcache*symbolstore`シンボル パス文字列。

文字列を含める場合`srv*`シンボル パスに、デバッガーは既定のシンボル ストアからシンボルを取得するシンボル サーバーを使用しています。 たとえば、次のコマンドは、シンボル サーバーを使用して、既定のシンボル ストアからシンボルを取得するデバッガーを示します。 これらのシンボルは、ローカル コンピューターではキャッシュされません。

```dbgcmd
.sympath srv*
```

文字列を含める場合`srv*symbolstore`デバッガー シンボル パスからシンボルを取得するシンボル サーバーを使用して、 *symbolstore*を格納します。 次のコマンドがシンボル ストアでからシンボルを取得するシンボル サーバーを使用するデバッガーに指示するなど、 https://msdl.microsoft.com/download/symbolsします。 これらのシンボルは、ローカル コンピューターではキャッシュされません。

```dbgcmd
.sympath srv*https://msdl.microsoft.com/download/symbols
```

文字列を含める場合`srv*localcache*symbolstore`デバッガー シンボル パスからシンボルを取得するシンボル サーバーを使用して、 *symbolstore*を格納し、キャッシュに、 *localcache*ディレクトリ。 次のコマンドがシンボル ストアでからシンボルを取得するシンボル サーバーを使用するデバッガーに指示するなど、 https://msdl.microsoft.com/download/symbolsでシンボルをキャッシュおよび`c:\MyServerSymbols`します。

```dbgcmd
.sympath srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

シンボルを手動で配置するコンピューターにディレクトリがある場合では、キャッシュとそのディレクトリは使用しないでシンボルをシンボル サーバーから取得します。 代わりに、2 つのディレクトリを使用します。 内のシンボルを手動で配置するなど、`c:\MyRegularSymbols`し指定`c:\MyServerSymbols`サーバーから取得されたシンボルのキャッシュとして。 次の例では、シンボル パスの両方のディレクトリを指定する方法を示します。

```dbgcmd
.sympath c:\MyRegularSymbols;srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

シンボル サーバーの詳細については、[シンボル ストアとシンボル サーバー](symbol-stores-and-symbol-servers.md)を参照してください。

## <a name="span-idcombiningcacheandsrvspanspan-idcombiningcacheandsrvspanspan-idcombiningcacheandsrvspancombining-cache-and-srv"></a><span id="Combining_cache__and_srv_"></span><span id="combining_cache__and_srv_"></span><span id="COMBINING_CACHE__AND_SRV_"></span>キャッシュを組み合わせて\*や srv\*


文字列を含める場合`cache*;`ローカル コンピューター上の既定のシンボル キャッシュ ディレクトリにシンボル パスにこの文字列の右側に表示される任意の要素から読み込まれたシンボルが格納されています。 次のコマンドにストアからシンボルを取得するシンボル サーバーを使用するデバッガーに指示など https://msdl.microsoft.com/download/symbolsし、既定のシンボルのキャッシュ ディレクトリにキャッシュします。

```dbgcmd
.sympath cache*;srv*https://msdl.microsoft.com/download/symbols
```

文字列を含める場合`cache*localsymbolcache;`にシンボル パスにこの文字列の右側に表示される任意の要素から読み込まれたシンボルが格納されている、 *localsymbolcache*ディレクトリ。

次のコマンドにストアからシンボルを取得するシンボル サーバーを使用するデバッガーに指示など https://msdl.microsoft.com/download/symbolsでシンボルをキャッシュし、`c:\MySymbols`ディレクトリ。

```dbgcmd
.sympath cache*c:\MySymbols;srv*https://msdl.microsoft.com/download/symbols
```

## <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>AgeStore を使用して、キャッシュのサイズを小さくには


AgeStore ツールを使用して、指定した日付より古いキャッシュ ファイルを削除するか、キャッシュの結果のサイズは、指定した量よりも少ないための十分な古いファイルを削除することができます。 ダウン ストリーム ストアが大きすぎる場合に役立ちます。 ことができます。 詳細については、[AgeStore](agestore.md)を参照してください。

シンボル サーバーとシンボル ストアの詳細については、[シンボル ストアとシンボル サーバー](symbol-stores-and-symbol-servers.md)を参照してください。

## <a name="span-idlazysymbolloadingspanspan-idlazysymbolloadingspanlazy-symbol-loading"></a><span id="lazy_symbol_loading"></span><span id="LAZY_SYMBOL_LOADING"></span>シンボルの遅延読み込み


デバッガーの既定の動作が使用するには*シンボルの遅延読み込み*(とも呼ばれます*シンボルの読み込みの遅延*)。 このタイプの読み込みでは、必要になるまでシンボルが読み込まれなかったことを意味します。

たとえばを使用して、シンボル パスが変更されたときに、 [ `.sympath` ](-sympath--set-symbol-path-.md)エクスポート シンボルを使用したコマンド、読み込まれたすべてのモジュールが限定的に再読み込みします。

完全な PDB シンボルを使用したモジュールのシンボルは遅延を再読み込みする場合は、新しいパスが PDB シンボルの読み込みに使用された元のパスには含まれていません。 まだ、新しいパスには、PDB シンボル ファイルを元のパスが含まれているこれらのシンボルは遅れて読み込まれません。

シンボルの遅延読み込みの詳細については、[シンボルの読み込みの遅延](deferred-symbol-loading.md)を参照してください。

遅延のシンボルを使用して、KD、CDB で読み込みをオフにすることができます、 `-s` [コマンド ライン オプション](command-line-options.md)します。 使用して、シンボルの読み込みを強制することもできます、 `ld` [ **(シンボルの読み込み)** ](ld--load-symbols-.md)コマンドまたはを使用して、 `.reload` [ **(モジュールの再読み込み)** 。](-reload--reload-module-.md)コマンドと共に、`/f`オプション。

## <span id="ddk_symbol_path_dbg"></span><span id="DDK_SYMBOL_PATH_DBG"></span>


### <a name="span-idcontrolling-the-symbol-pathspanspan-idcontrolling-the-symbol-pathspancontrolling-the-symbol-path"></a><span id="controlling-the-symbol-path"></span><span id="CONTROLLING-THE-SYMBOL-PATH"></span>シンボル パスを制御します。

シンボル パスを制御するには、次のいずれかの操作を行います。

-   使用して、 [ `.sympath` ](-sympath--set-symbol-path-.md)コマンドを表示、設定、変更、またはパスに追加します。 `.symfix` [ **(シンボル ストア パスの設定)** ](-symfix--set-symbol-store-path-.md)コマンド`.sympath`が、一部の入力を保存します。

-   使用して、デバッガーを開始する前に、`_NT_SYMBOL_PATH`と`_NT_ALT_SYMBOL_PATH`[環境変数](environment-variables.md)パスを設定します。 シンボル パスが追加することによって作成された`_NT_SYMBOL_PATH`後`_NT_ALT_SYMBOL_PATH`します。 (通常は、パスがによって設定されます、`_NT_SYMBOL_PATH`します。 使用するただし、`_NT_ALT_SYMBOL_PATH`特殊でこれらの設定を上書きする、場合によっては共有シンボル ファイルのプライベート バージョンがある場合のようにします)。これらの環境変数を介して無効なディレクトリを追加しようとすると、デバッガーは、このディレクトリを無視します。

-   デバッガーを起動するときに使用して、 `-y` [コマンド ライン オプション](command-line-options.md)パスを設定します。

-   (WinDbg のみ)使用して、[ファイル |ファイルのパスをシンボル](file---symbol-file-path.md)コマンドまたはキーを押して`CTRL+S`を表示するには、設定、変更、またはパスに追加します。

使用する場合、 `-sins` [コマンド ライン オプション](command-line-options.md)デバッガーがシンボルの path 環境変数を無視します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[高度な SymSrv の使用](advanced-symsrv-use.md)

 

 

