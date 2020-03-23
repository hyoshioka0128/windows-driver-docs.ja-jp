---
title: Windows デバッガーのシンボル パス
description: シンボル パスでは、Windows デバッガー (WinDbg、KD、CDB、NTST) によってシンボル ファイルが検索される場所が指定されています。
ms.assetid: 705df98f-717f-40ad-a424-101826970691
keywords: シンボル ファイルとパス, シンボル, 遅延シンボル読み込み, シンボルの遅延読み込み, シンボル パス
ms.date: 10/23/2019
ms.localizationpriority: high
ms.openlocfilehash: 71cf811cffadf33a34c207e5455ff2a0e3d322f6
ms.sourcegitcommit: 29d9e97439f19d2c5a090006640e4e5659e56412
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2020
ms.locfileid: "78335963"
---
# <a name="symbol-path-for-windows-debuggers"></a>Windows デバッガーのシンボル パス

シンボル パスでは、Windows デバッガー (WinDbg、KD、CDB、NTST) によってシンボル ファイルが検索される場所が指定されています。 シンボルとシンボル ファイルの詳細については、[シンボル](symbols.md)に関する記事を参照してください。

一部のコンパイラ (Microsoft Visual Studio など) では、シンボル ファイルはバイナリ ファイルと同じディレクトリに配置されます。 シンボル ファイルとチェックされたバイナリ ファイルには、パスとファイル名の情報が含まれます。 この情報により、多くの場合、デバッガーではシンボル ファイルを自動的に検索できます。 実行可能ファイルがビルドされたコンピューターでユーザー モード プロセスをデバッグしていて、シンボル ファイルがまだ元の場所にある場合は、シンボル パスを設定しなくても、デバッガーでシンボル ファイルを見つけることができます。

その他のほとんどの状況では、シンボル ファイルの場所を指すようにシンボル パスを設定する必要があります。

## <a name="span-idsymbol_path_syntaxspanspan-idsymbol_path_syntaxspanspan-idsymbol_path_syntaxspansymbol-path-syntax"></a><span id="Symbol_Path_Syntax"></span><span id="symbol_path_syntax"></span><span id="SYMBOL_PATH_SYNTAX"></span>シンボル パスの構文

デバッガーのシンボル パスは、セミコロンで区切られた複数のディレクトリ パスで構成される文字列です。

相対パスもサポートされています。 ただし、常に同じディレクトリからデバッガーを起動する場合を除き、各パスの前にドライブ文字またはネットワーク共有を追加する必要があります。 ネットワーク共有もサポートされています。

シンボル パス内のディレクトリごとに、デバッガーでは 3 つのディレクトリが検索されます。 たとえば、シンボル パスに `c:\MyDir` ディレクトリが含まれていて、デバッガーで DLL のシンボル情報が検索されている場合、デバッガーでは最初に `c:\MyDir\symbols\dll`、次に `c:\MyDir\dll`、最後に `c:\MyDir` が検索されます。 その後、デバッガーでは、シンボル パス内のディレクトリごとにこのプロセスが繰り返されます。 最後に、デバッガーでは現在のディレクトリが検索された後、現在のディレクトリに `..\dll` を追加した場所が検索されます。 (デバッガーでは、デバッグ対象のバイナリに応じて、`..\dll`、`..\exe`、または `..\sys` が追加されます)。

シンボル ファイルには、日付と時刻のスタンプがあります。 この順序で最初に検出される可能性のある間違ったシンボルがデバッガーによって使用されることを心配する必要はありません。 デバッグ対象のバイナリ ファイルのタイムスタンプと一致するシンボルが常に検索されます。 シンボル ファイルが使用できない場合の応答の詳細については、[シンボル照合の問題の補正](matching-symbol-names.md)に関する記事を参照してください。

シンボル パスを設定する方法の 1 つは、[ **.sympath**](-sympath--set-symbol-path-.md) コマンドを入力することです。 シンボル パスを設定する他の方法については、このトピックで後述する「[シンボル パスを制御する](#controlling-the-symbol-path)」を参照してください。

## <a name="span-idcaching_symbols_locallyspanspan-idcaching_symbols_locallyspanspan-idcaching_symbols_locallyspancaching-symbols-locally"></a><span id="Caching_Symbols_Locally"></span><span id="caching_symbols_locally"></span><span id="CACHING_SYMBOLS_LOCALLY"></span>シンボルをローカルにキャッシュする

常にシンボルをローカルにキャッシュすることを強くお勧めします。 シンボルをローカルにキャッシュする方法の 1 つは、シンボル パスに `cache*;` または `cache*localsymbolcache;*` を含めることです。

シンボル パスに `cache*;` という文字列を含めた場合、この文字列の右側にある要素から読み込まれたシンボルは、ローカル コンピューターの既定のシンボル キャッシュ ディレクトリに格納されます。 たとえば、次のコマンドでは、`\\someshare` ネットワーク共有からシンボルを取得し、ローカル コンピューター上の既定の場所にシンボルをキャッシュするように、デバッガーに指示されます。

```dbgcmd
.sympath cache*;\\someshare
```

シンボル パスに `cache*localsymbolcache;` という文字列を含めた場合、この文字列の右側にある要素から読み込まれたシンボルは、*localsymbolcache* ディレクトリに格納されます。

たとえば、次のコマンドでは、`\\someshare` ネットワーク共有からシンボルを取得し、`c:\MySymbols` ディレクトリにシンボルをキャッシュするように、デバッガーに指示されます。

```dbgcmd
.sympath cache*c:\MySymbols;\\someshare
```

## <a name="span-idusing_a_symbol_serverspanspan-idusing_a_symbol_serverspanspan-idusing_a_symbol_serverspanusing-a-symbol-server"></a><span id="Using_a_Symbol_Server"></span><span id="using_a_symbol_server"></span><span id="USING_A_SYMBOL_SERVER"></span>シンボル サーバーを使用する

インターネットまたは企業ネットワークに接続している場合は、シンボル サーバーを使用するのが、シンボルにアクセスする最も効率的な方法です。 シンボル パスで `srv*`、`srv*symbolstore`、または `srv*localsymbolcache*symbolstore` という文字列を使用することにより、シンボル サーバーを使用できます。

シンボル パスに文字列 `srv*` を含めると、デバッガーではシンボル サーバーを使用して既定のシンボル ストアからシンボルが取得されます。 たとえば、次のコマンドでは、シンボル サーバーを使用して既定のシンボル ストアからシンボルを取得することが、デバッガーに指示されます。 これらのシンボルは、ローカル コンピューターにキャッシュされません。

```dbgcmd
.sympath srv*
```

シンボル パスに文字列 `srv*symbolstore` を含めると、デバッガーではシンボル サーバーを使用して *symbolstore* ストアからシンボルが取得されます。 たとえば、次のコマンドでは、シンボル サーバーを使用して https://msdl.microsoft.com/download/symbols にあるシンボル ストアからシンボルを取得することが、デバッガーに指示されます。 これらのシンボルは、ローカル コンピューターにキャッシュされません。

```dbgcmd
.sympath srv*https://msdl.microsoft.com/download/symbols
```

シンボル パスに文字列 `srv*localcache*symbolstore` を含めると、デバッガーでは、シンボル サーバーを使用して *symbolstore* ストアからシンボルが取得されて、*localcache* ディレクトリにキャッシュされます。 たとえば、次のコマンドでは、シンボル サーバーを使用して https://msdl.microsoft.com/download/symbols にあるシンボル ストアからシンボルを取得し、`c:\MyServerSymbols` にシンボルをキャッシュすることが、デバッガーに指示されます。

```dbgcmd
.sympath srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

お使いのコンピューター上のディレクトリにシンボルを手動で配置する場合は、シンボル サーバーから取得したシンボルのキャッシュとして、そのディレクトリを使用しないでください。 代わりに、2 つの異なるディレクトリを使用します。 たとえば、`c:\MyRegularSymbols` に手動でシンボルを配置し、サーバーから取得されたシンボルのキャッシュとして `c:\MyServerSymbols` を指定することができます。 次の例は、シンボル パスで両方のディレクトリを指定する方法を示したものです。

```dbgcmd
.sympath c:\MyRegularSymbols;srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

シンボル サーバーの詳細については、「[シンボル ストアとシンボル サーバー](symbol-stores-and-symbol-servers.md)」を参照してください。

## <a name="span-idcombining_cache__and_srv_spanspan-idcombining_cache__and_srv_spanspan-idcombining_cache__and_srv_spancombining-cache-and-srv"></a><span id="Combining_cache__and_srv_"></span><span id="combining_cache__and_srv_"></span><span id="COMBINING_CACHE__AND_SRV_"></span>cache\* と srv\* を組み合わせる


シンボル パスに `cache*;` という文字列を含めた場合、この文字列の右側にある要素から読み込まれたシンボルは、ローカル コンピューターの既定のシンボル キャッシュ ディレクトリに格納されます。 たとえば、次のコマンドでは、シンボル サーバーを使用して https://msdl.microsoft.com/download/symbols にあるストアからシンボルを取得し、既定のシンボル キャッシュ ディレクトリにそれをキャッシュすることが、デバッガーに指示されます。

```dbgcmd
.sympath cache*;srv*https://msdl.microsoft.com/download/symbols
```

シンボル パスに `cache*localsymbolcache;` という文字列を含めた場合、この文字列の右側にある要素から読み込まれたシンボルは、*localsymbolcache* ディレクトリに格納されます。

たとえば、次のコマンドでは、シンボル サーバーを使用して https://msdl.microsoft.com/download/symbols にあるストアからシンボルを取得し、`c:\MySymbols` ディレクトリにシンボルをキャッシュすることが、デバッガーに指示されます。

```dbgcmd
.sympath cache*c:\MySymbols;srv*https://msdl.microsoft.com/download/symbols
```

## <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>AgeStore を使用してキャッシュのサイズを小さくする

AgeStore ツールを使用すると、指定した日付より古いキャッシュ ファイルを削除したり、結果のキャッシュ サイズが指定した量より少なくなるのに十分なだけ古いファイルを削除したりすることができます。 これは、ダウンストリーム ストアが大きすぎる場合に便利です。 詳しくは、「[AgeStore](agestore.md)」をご覧ください。

シンボル サーバーとシンボル ストアについて詳しくは、「[シンボル ストアとシンボル サーバー](symbol-stores-and-symbol-servers.md)」をご覧ください。

## <a name="span-idlazy_symbol_loadingspanspan-idlazy_symbol_loadingspanlazy-symbol-loading"></a><span id="lazy_symbol_loading"></span><span id="LAZY_SYMBOL_LOADING"></span>シンボルの遅延読み込み

デバッガーの既定の動作では、"*シンボルの遅延読み込み*" ("*遅延シンボル読み込み*" とも呼ばれます) が使用されます。 この種の読み込みは、必要になるまでシンボルが読み込まれないことを意味します。

たとえば [`.sympath`](-sympath--set-symbol-path-.md) コマンドを使用するなどして、シンボル パスが変更されると、エクスポート シンボルを含む読み込まれたすべてのモジュールが遅延で再読み込みされます。

完全な PDB シンボルが含まれるモジュールのシンボルは、PDB シンボルの読み込みに使用された元のパスが新しいパスに含まれなくなった場合、遅延で再読み込みされます。 PDB シンボル ファイルへの元のパスが新しいパスにまだ含まれる場合は、それらのシンボルは遅延で再読み込みされません。

シンボルの遅延読み込みについて詳しくは、「[シンボルの遅延読み込み](deferred-symbol-loading.md)」をご覧ください。

`-s` [コマンドライン オプション](command-line-options.md)を使用することにより、CDB および KD でのシンボルの遅延読み込みをオフにすることができます。 また、`ld` [ **(シンボル読み込み)** ](ld--load-symbols-.md) コマンドを使用するか、`/f` オプションを指定して `.reload` [ **(モジュール再読み込み)** ](-reload--reload-module-.md) コマンドを使用することで、シンボルを強制的に読み込むことができます。

## <a name="span-idazurespanspan-idazurespanazure-devops-services-artifacts"></a><span id="azure"></span><span id="AZURE"></span>Azure DevOps Services の成果物

シンボル サーバーは、Azure DevOps Services の Azure Artifacts で使用できます。 WinDbg での Azure Artifacts の使用について詳しくは、[WinDbg でのシンボルを使用したデバッグ](https://docs.microsoft.com/azure/devops/artifacts/symbols/debug-with-symbols-visual-studio)に関する記事をご覧ください。 Azure によって生成されるシンボルに関する一般的な情報については、「[シンボル ファイル (PDB)](https://docs.microsoft.com/azure/devops/artifacts/concepts/symbols)」をご覧ください。

### <a name="span-idcontrolling-the-symbol-pathspanspan-idcontrolling-the-symbol-pathspancontrolling-the-symbol-path"></a><span id="controlling-the-symbol-path"></span><span id="CONTROLLING-THE-SYMBOL-PATH"></span>シンボル パスを制御する

シンボル パスを制御するには、次のいずれかを行うことができます。

- [`.sympath`](-sympath--set-symbol-path-.md) コマンドを使用して、パスを表示、設定、変更、または追加します。 `.symfix` [ **(シンボル ストア パスの設定)** ](-symfix--set-symbol-store-path-.md) コマンドは `.sympath` に似ていますが、一部の入力を省略できます。

- デバッガーを開始する前に、`_NT_SYMBOL_PATH` および `_NT_ALT_SYMBOL_PATH` [環境変数](environment-variables.md)を使用して、パスを設定します。 シンボル パスは、`_NT_ALT_SYMBOL_PATH` の後に `_NT_SYMBOL_PATH` を追加することによって作成されます。 (通常、パスは `_NT_SYMBOL_PATH` によって設定されます。 ただし、共有シンボル ファイルのプライベート バージョンがある場合など、特殊なケースでは、`_NT_ALT_SYMBOL_PATH` を使用してこれらの設定をオーバーライドすることができます。)これらの環境変数を使用して無効なディレクトリを追加しようとすると、デバッガーではこのディレクトリが無視されます。

- デバッガーを開始するときに、`-y` [コマンドライン オプション](command-line-options.md)を使用してパスを設定します。

- (WinDbg のみ) [[File]\(ファイル\) > [Symbol File Path]\(シンボル ファイル パス\)](file---symbol-file-path.md) コマンドを使用するか、`CTRL+S` キーを押して、パスを表示、設定、変更、または追加します。

`-sins` [コマンドライン オプション](command-line-options.md)を使用した場合、デバッガーではシンボル パス環境変数が無視されます。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[SymSrv の高度な使用方法](advanced-symsrv-use.md)
