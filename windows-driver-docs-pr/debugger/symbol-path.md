---
title: Windows デバッガーのシンボル パス
description: シンボルパスは、Windows デバッガー (WinDbg、KD、CDB、NTST) がシンボルファイルを検索する場所を指定します。
ms.assetid: 705df98f-717f-40ad-a424-101826970691
keywords: シンボルファイルとパス、シンボル、遅延シンボルの読み込み、遅延シンボルの読み込み、シンボルパス
ms.date: 10/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 433f34062c372b6226bf833baddd95255c3cdfbc
ms.sourcegitcommit: d2dab8b8bf335835d0341ca3f0a36eab0ec028f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72892678"
---
# <a name="symbol-path-for-windows-debuggers"></a>Windows デバッガーのシンボル パス

シンボルパスは、Windows デバッガー (WinDbg、KD、CDB、NTST) がシンボルファイルを検索する場所を指定します。 シンボルおよびシンボルファイルの詳細については、「[シンボル](symbols.md)」を参照してください。

一部のコンパイラ (Microsoft Visual Studio など) では、バイナリファイルと同じディレクトリにシンボルファイルが配置されます。 シンボルファイルとチェックされるバイナリファイルには、パスとファイル名の情報が含まれています。 この情報は、デバッガーがシンボルファイルを自動的に検索できるようにするためによく使用されます。 実行可能ファイルがビルドされたコンピューターでユーザーモードプロセスをデバッグしていて、シンボルファイルが元の場所にある場合は、シンボルパスを設定しなくても、デバッガーでシンボルファイルを見つけることができます。

その他の状況では、シンボルファイルの場所を指すようにシンボルパスを設定する必要があります。

## <a name="span-idsymbol_path_syntaxspanspan-idsymbol_path_syntaxspanspan-idsymbol_path_syntaxspansymbol-path-syntax"></a><span id="Symbol_Path_Syntax"></span><span id="symbol_path_syntax"></span><span id="SYMBOL_PATH_SYNTAX"></span>シンボルパスの構文

デバッガーのシンボルパスは、セミコロンで区切られた複数のディレクトリパスで構成される文字列です。

相対パスがサポートされています。 ただし、常に同じディレクトリからデバッガーを起動する場合を除き、各パスの前にドライブ文字またはネットワーク共有を追加する必要があります。 ネットワーク共有もサポートされています。

シンボルパス内のディレクトリごとに、デバッガーは3つのディレクトリを検索します。 たとえば、シンボルパスに `c:\MyDir` ディレクトリが含まれていて、デバッガーが DLL のシンボル情報を探している場合、デバッガーは最初に `c:\MyDir\symbols\dll`、次に `c:\MyDir\dll`、最後に `c:\MyDir` を検索します。 デバッガーは、シンボルパス内のディレクトリごとにこのプロセスを繰り返します。 最後に、デバッガーは現在のディレクトリを検索し、現在のディレクトリに `..\dll` を追加します。 (デバッガーは、デバッグ対象のバイナリに応じて `..\dll`、`..\exe`、または `..\sys` を追加します)。

シンボルファイルには、日付と時刻のタイムスタンプがあります。 デバッガーでは、このシーケンスで最初に検出される可能性のある間違ったシンボルが使用されることを心配する必要はありません。 これは、デバッグ中のバイナリファイルのタイムスタンプに一致するシンボルを常に検索します。 シンボルファイルが使用できない場合の応答の詳細については、「[シンボル照合の問題の補正](matching-symbol-names.md)」を参照してください。

シンボルパスを設定する方法の1つは、 [**sympath**](-sympath--set-symbol-path-.md)コマンドを入力することです。 シンボルパスを設定するその他の方法については、このトピックで後述する「[シンボルパスの制御](#controlling-the-symbol-path)」を参照してください。

## <a name="span-idcaching_symbols_locallyspanspan-idcaching_symbols_locallyspanspan-idcaching_symbols_locallyspancaching-symbols-locally"></a><span id="Caching_Symbols_Locally"></span><span id="caching_symbols_locally"></span><span id="CACHING_SYMBOLS_LOCALLY"></span>シンボルをローカルにキャッシュする

シンボルは常にローカルにキャッシュすることを強くお勧めします。 シンボルをローカルにキャッシュする方法の1つとして、シンボルパスに `cache*;` または `cache*localsymbolcache;*` を含める方法があります。

シンボルパスに文字列 `cache*;` を含めると、この文字列の右側にある要素から読み込まれたシンボルは、ローカルコンピューターの既定のシンボルキャッシュディレクトリに格納されます。 たとえば、次のコマンドは、`\\someshare` ネットワーク共有からシンボルを取得し、ローカルコンピューター上の既定の場所にシンボルをキャッシュするようにデバッガーに指示します。

```dbgcmd
.sympath cache*;\\someshare
```

シンボルパスに文字列 `cache*localsymbolcache;` を含めると、この文字列の右側にある要素から読み込まれたシンボルは、 *localsymbol cache*ディレクトリに格納されます。

たとえば、次のコマンドは、`\\someshare` ネットワーク共有からシンボルを取得し、`c:\MySymbols` ディレクトリ内のシンボルをキャッシュするようにデバッガーに指示します。

```dbgcmd
.sympath cache*c:\MySymbols;\\someshare
```

## <a name="span-idusing_a_symbol_serverspanspan-idusing_a_symbol_serverspanspan-idusing_a_symbol_serverspanusing-a-symbol-server"></a><span id="Using_a_Symbol_Server"></span><span id="using_a_symbol_server"></span><span id="USING_A_SYMBOL_SERVER"></span>シンボルサーバーの使用

インターネットまたは企業ネットワークに接続している場合は、シンボルサーバーを使用するのが最も効率的な方法です。 シンボルサーバーを使用するには、シンボルパスで `srv*`、`srv*symbolstore`、または `srv*localsymbolcache*symbolstore` 文字列を使用します。

シンボルパスに文字列 `srv*` を含めると、デバッガーはシンボルサーバーを使用して既定のシンボルストアからシンボルを取得します。 たとえば、次のコマンドは、シンボルサーバーを使用して既定のシンボルストアからシンボルを取得するようにデバッガーに指示します。 これらのシンボルは、ローカルコンピューターにキャッシュされません。

```dbgcmd
.sympath srv*
```

シンボルパスに文字列 `srv*symbolstore` を含めると、デバッガーはシンボルサーバーを使用して symbol*ストア*ストアからシンボルを取得します。 たとえば、次のコマンドは、シンボルサーバーを使用して https://msdl.microsoft.com/download/symbols のシンボルストアからシンボルを取得するようにデバッガーに指示します。 これらのシンボルは、ローカルコンピューターにキャッシュされません。

```dbgcmd
.sympath srv*https://msdl.microsoft.com/download/symbols
```

シンボルパスに文字列 `srv*localcache*symbolstore` を含めると、デバッガーはシンボルサーバーを使用して symbol*ストア*ストアからシンボルを取得し、 *localcache*ディレクトリにキャッシュします。 たとえば、次のコマンドは、シンボルサーバーを使用して https://msdl.microsoft.com/download/symbols のシンボルストアからシンボルを取得し `c:\MyServerSymbols` にシンボルをキャッシュするようにデバッガーに指示します。

```dbgcmd
.sympath srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

コンピューターにシンボルを手動で配置するディレクトリがある場合は、そのディレクトリをシンボルサーバーから取得したシンボルのキャッシュとして使用しないでください。 代わりに、2つの異なるディレクトリを使用します。 たとえば、`c:\MyRegularSymbols` に手動でシンボルを配置し、サーバーから取得したシンボルのキャッシュとして `c:\MyServerSymbols` を指定することができます。 次の例は、シンボルパスに両方のディレクトリを指定する方法を示しています。

```dbgcmd
.sympath c:\MyRegularSymbols;srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

シンボルサーバーの詳細については、「[シンボルストアとシンボルサーバー](symbol-stores-and-symbol-servers.md)」を参照してください。

## <a name="span-idcombining_cache__and_srv_spanspan-idcombining_cache__and_srv_spanspan-idcombining_cache__and_srv_spancombining-cache-and-srv"></a><span id="Combining_cache__and_srv_"></span><span id="combining_cache__and_srv_"></span><span id="COMBINING_CACHE__AND_SRV_"></span>キャッシュ \* と srv \* の組み合わせ


シンボルパスに文字列 `cache*;` を含めると、この文字列の右側にある要素から読み込まれたシンボルは、ローカルコンピューターの既定のシンボルキャッシュディレクトリに格納されます。 たとえば、次のコマンドは、シンボルサーバーを使用して https://msdl.microsoft.com/download/symbols のストアからシンボルを取得し、既定のシンボルキャッシュディレクトリにキャッシュするようにデバッガーに指示します。

```dbgcmd
.sympath cache*;srv*https://msdl.microsoft.com/download/symbols
```

シンボルパスに文字列 `cache*localsymbolcache;` を含めると、この文字列の右側にある要素から読み込まれたシンボルは、 *localsymbol cache*ディレクトリに格納されます。

たとえば、次のコマンドは、シンボルサーバーを使用して https://msdl.microsoft.com/download/symbols のストアからシンボルを取得し、`c:\MySymbols` ディレクトリにシンボルをキャッシュするようにデバッガーに指示します。

```dbgcmd
.sympath cache*c:\MySymbols;srv*https://msdl.microsoft.com/download/symbols
```

## <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>AgeStore を使用してキャッシュサイズを小さくする

AgeStore ツールを使用すると、指定した日付より古いキャッシュファイルを削除したり、キャッシュの結果サイズが指定した量よりも少ない古いファイルを削除したりすることができます。 これは、ダウンストリームストアが大きすぎる場合に便利です。 詳細については、「 [Agestore](agestore.md)」を参照してください。

シンボルサーバーとシンボルストアの詳細については、「[シンボルストアとシンボルサーバー](symbol-stores-and-symbol-servers.md)」を参照してください。

## <a name="span-idlazy_symbol_loadingspanspan-idlazy_symbol_loadingspanlazy-symbol-loading"></a><span id="lazy_symbol_loading"></span><span id="LAZY_SYMBOL_LOADING"></span>遅延シンボルの読み込み

デバッガーの既定の動作では、遅延*シンボルの読み込み*(*遅延シンボルの読み込み*とも呼ばれます) を使用します。 この種の読み込みとは、シンボルが必要になるまで読み込まれないことを意味します。

たとえば、 [`.sympath`](-sympath--set-symbol-path-.md)コマンドを使用してシンボルパスを変更すると、エクスポートシンボルを含む読み込まれたすべてのモジュールが遅延再読み込みされます。

Pdb シンボルの読み込みに使用された元のパスが新しいパスに含まれなくなった場合、完全な PDB シンボルを持つモジュールのシンボルは遅延再読み込みされます。 新しいパスに PDB シンボルファイルへの元のパスがまだ含まれている場合、それらのシンボルは遅延再読み込みされません。

遅延シンボルの読み込みの詳細については、「[遅延シンボルの読み込み](deferred-symbol-loading.md)」を参照してください。

`-s`[コマンドラインオプション](command-line-options.md)を使用して、CDB および KD でのレイジーシンボルの読み込みをオフにすることができます。 シンボルの読み込みを強制するには、`ld` [ **(読み込みシンボル)** ](ld--load-symbols-.md)コマンドを使用するか、`/f` オプションと共に `.reload` [ **(モジュールの再読み込み)** ](-reload--reload-module-.md)コマンドを使用することもできます。

## <a name="span-idazurespanspan-idazurespanazure-devops-services-artifacts"></a><span id="azure"></span><span id="AZURE"></span>Azure DevOps Services の成果物

シンボルサーバーは、Azure DevOps Services の Azure Artifacts で使用できます。 WinDbg での Azure Artifacts の操作の詳細については、「 [windbg でのシンボルを使用したデバッグ](https://docs.microsoft.com/azure/devops/artifacts/symbols/debug-with-symbols-visual-studio)」を参照してください。 Azure によって生成されるシンボルに関する一般的な情報については、「[シンボルファイル (pdb)](https://docs.microsoft.com/azure/devops/artifacts/concepts/symbols)」を参照してください。

### <a name="span-idcontrolling-the-symbol-pathspanspan-idcontrolling-the-symbol-pathspancontrolling-the-symbol-path"></a><span id="controlling-the-symbol-path"></span><span id="CONTROLLING-THE-SYMBOL-PATH"></span>シンボルパスの制御

シンボルパスを制御するには、次のいずれかの操作を行います。

- [`.sympath`](-sympath--set-symbol-path-.md)コマンドを使用して、パスの表示、設定、変更、または追加を行います。 `.symfix` [ **(シンボルストアパスの設定)** ](-symfix--set-symbol-store-path-.md)コマンドは `.sympath` に似ていますが、いくつかの入力が保存されます。

- デバッガーを開始する前に、`_NT_SYMBOL_PATH` と `_NT_ALT_SYMBOL_PATH`[環境変数](environment-variables.md)を使用してパスを設定します。 シンボルパスは、`_NT_ALT_SYMBOL_PATH`後に `_NT_SYMBOL_PATH` を追加することによって作成されます。 (通常、パスは `_NT_SYMBOL_PATH`によって設定されます。 ただし、共有シンボルファイルのプライベートバージョンがある場合など、特殊なケースでは、`_NT_ALT_SYMBOL_PATH` を使用してこれらの設定をオーバーライドすることができます。これらの環境変数を使用して無効なディレクトリを追加しようとすると、デバッガーはこのディレクトリを無視します。

- デバッガーを起動するときに、`-y`[コマンドラインオプション](command-line-options.md)を使用してパスを設定します。

- (WinDbg のみ)File | を使用します。 [シンボルファイルのパス](file---symbol-file-path.md)コマンドまたは `CTRL+S` を押すと、パスの表示、設定、変更、または追加が実行されます。

`-sins`[コマンドラインオプション](command-line-options.md)を使用した場合、デバッガーはシンボルパス環境変数を無視します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[高度な SymSrv の使用](advanced-symsrv-use.md)
