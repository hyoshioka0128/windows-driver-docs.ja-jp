---
title: SymSrv の高度な使用方法
description: SymSrv の高度な使用方法
ms.assetid: 16d4dda0-4bcf-4450-9972-e20d71efc845
keywords:
- SymSrv, 機能
- シンボルのキャッシュ
- シンボルサーバー, キャッシュ
- シンボル、キャッシュ
- シンボルサーバー、ダウンストリームストア
- ダウンストリームストア (シンボルサーバー)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec394624406cf4cf4d4844bff2ecd6ec3cc46740
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533961"
---
# <a name="advanced-symsrv-use"></a>SymSrv の高度な使用方法


SymSrv は、一元化されたシンボルストアからシンボルファイルを配信できます。 このストアには、任意の数のプログラムやオペレーティングシステムに対応する任意の数のシンボルファイルを含めることができます。 ストアには、バイナリファイルを含めることもできます (これはミニダンプをデバッグする場合に便利です)。

ストアには、実際のシンボルファイルとバイナリファイルを含めることができます。また、シンボルファイルへのポインターだけを格納することもできます。 ストアにポインターが含まれている場合、SymSrv は実際のファイルをソースから直接取得します。

SymSrv を使用すると、大きなシンボルストアを、特殊なデバッグタスクに適した小さいサブセットに分割することもできます。

最後に、SymSrv は、オペレーティングシステムによって提供されるログオン情報を使用して、HTTP または HTTPS ソースからシンボルファイルを取得できます。 SymSrv は、スマートカード、証明書、および通常のログインとパスワードによって保護された HTTPS サイトをサポートしています。 詳細については、「 [HTTP シンボルストア](http-symbol-stores.md)」を参照してください。

### <a name="span-idsetting_the_symbol_pathspanspan-idsetting_the_symbol_pathspansetting-the-symbol-path"></a><span id="setting_the_symbol_path"></span><span id="SETTING_THE_SYMBOL_PATH"></span>シンボルパスの設定

このシンボルサーバーを使用するには、デバッガーと同じディレクトリに symsrv .dll をインストールする必要があります。 シンボルパスは次のように設定できます。

```console
set _NT_SYMBOL_PATH = symsrv*ServerDLL*DownstreamStore*\\Server\Share 

set _NT_SYMBOL_PATH = symsrv*ServerDLL*\\Server\Share 

set _NT_SYMBOL_PATH = srv*DownstreamStore*\\Server\Share 

set _NT_SYMBOL_PATH = srv*\\Server\Share 
```

この構文の部分は、次のように説明されています。

<span id="________symsrv"></span><span id="________SYMSRV"></span>**symsrv**  
このキーワードは常に最初に表示される必要があります。 これは、この項目が通常のシンボルディレクトリではなく、シンボルサーバーであることをデバッガーに示します。

<span id="ServerDLL"></span><span id="serverdll"></span><span id="SERVERDLL"></span>*ServerDLL*  
シンボルサーバー DLL の名前を指定します。 SymSrv シンボルサーバーを使用している場合、これは常に symsrv .dll です。

<span id="srv"></span><span id="SRV"></span>**is**  
これは**symsrv \* symsrv .dll**の短縮形です。

<span id="DownstreamStore"></span><span id="downstreamstore"></span><span id="DOWNSTREAMSTORE"></span>*DownstreamStore*  
ダウンストリームストアを指定します。 これは、個々のシンボルファイルをキャッシュするために使用されるローカルディレクトリまたはネットワーク共有です。

複数のダウンストリームストアを指定するには、アスタリスクで区切ります。 複数のダウンストリームストアについては、このページの下位にある**カスケードダウンストリームストア**で説明されています。

通常、ダウンストリームストアが指定されている行に2つのアスタリスクを含めると、既定のダウンストリームストアが使用されます。 このストアは、ホームディレクトリの sym サブディレクトリにあります。 ホームディレクトリの既定値は、デバッガーのインストールディレクトリです。これは、 [**! homedir**](-homedir.md)拡張機能を使用するか、dbghelp homedir 環境変数を設定することによって変更でき \_ ます。

*Downstreamstore*に存在しないディレクトリが指定されている場合、SymStore はそれを作成しようとします。

*Downstreamstore*パラメーターが省略されていて、追加のアスタリスクが含まれていない場合 (つまり、1つのアスタリスクまたは**symsrv**が2つのアスタリスクで**srv**を使用する場合、ダウンストリームストアは作成されません)。 デバッガーは、ローカルでキャッシュせずに、すべてのシンボルファイルをサーバーから直接読み込みます。

**メモ**   HTTP または HTTPS サイトからシンボルにアクセスする場合、またはシンボルストアで圧縮ファイルが使用されている場合は、常にダウンストリームストアが使用されます。 ダウンストリームストアが指定されていない場合は、ホームディレクトリの sym サブディレクトリに1つが作成されます。

 

<span id="__Server_Share"></span><span id="__server_share"></span><span id="__SERVER_SHARE"></span>*\\\\サーバー \\ 共有*  
リモートシンボルストアのサーバーと共有を指定します。

ダウンストリームストアが使用されている場合、デバッガーは最初にこのストア内のシンボルファイルを検索します。 シンボルファイルが見つからない場合、デバッガーは指定された*サーバー*と*共有*からシンボルファイルを見つけ、そのファイルのコピーを下流ストアにキャッシュします。 このファイルは、ツリー内の [ * \\ \\ サーバー \\ 共有*] の下*にあるツリー*内のサブディレクトリにコピーされます。

シンボルサーバーは、シンボルパス内の唯一のエントリである必要はありません。 シンボルパスが複数のエントリで構成されている場合、デバッガーは、シンボルサーバーまたは実際のディレクトリの名前が付けられているかどうかに関係なく、必要なシンボルファイルの各エントリを (左から右に) 順番にチェックします。

次に例をいくつか示します。 Mybuilds でシンボルストアを使用して SymSrv をシンボルサーバーとして使用するには \\ \\ \\ 、次のシンボルパスを設定します。

```console
set _NT_SYMBOL_PATH= symsrv*symsrv.dll*\\mybuilds\mysymbols
```

シンボルパスを設定して、 \\ \\ \\ mybuilds on mybuilds をローカルディレクトリ c: localsymbols にコピーし、mybuilds をシンボルストアからコピーするようにシンボルパスを設定するには \\ 、次のように使用します。

```console
set _NT_SYMBOL_PATH=symsrv*symsrv.dll*c:\localsymbols*\\mybuilds\mysymbols
```

シンボルパスを設定して、デバッガーがシンボルファイルを HTTPS サイトから `https://www.company.com/manysymbols` ローカルネットワークディレクトリ localserver myshare mycache にコピーするようにするには \\ \\ \\ \\ 、次のように使用します。

```console
set _NT_SYMBOL_PATH=symsrv*symsrv.dll*\\localserver\myshare\mycache*https://www.company.com/manysymbols
```

この最後の例は、次のように短縮することもできます。

```console
set _NT_SYMBOL_PATH=srv*\\localserver\myshare\mycache*https://www.company.com/manysymbols
```

また、シンボルパスには、複数のディレクトリまたはシンボルサーバーをセミコロンで区切って含めることができます。 これによって、複数の場所 (または複数のシンボルサーバー) からシンボルを見つけることができます。 バイナリに一致しないシンボルファイルがある場合、デバッガーは、正確なパラメーターのみをチェックするため、シンボルサーバーを使用してそれを見つけることができません。 ただし、デバッガーは、従来のシンボルパスを使用して、正しい名前で一致しないシンボルファイルを見つけ、正常に読み込みます。 ファイルは技術的には正しいシンボルファイルではありませんが、役に立つ情報を提供する場合があります。

### <a name="span-idcompressed_filesspanspan-idcompressed_filesspancompressed-files"></a><span id="compressed_files"></span><span id="COMPRESSED_FILES"></span>圧縮されたファイル

SymSrv は、圧縮されたファイルを含むシンボルストアと互換性があります。ただし、[ここで](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=17657)使用可能な compress ツールで圧縮が行われている必要があります。 圧縮ファイルには、ファイル拡張子の最後の文字としてアンダースコア (たとえば、 \_ module2 または) を指定する必要があり \_ ます。 詳細については、「 [SymStore](symstore.md)」を参照してください。

ストアのファイルが圧縮されている場合は、ダウンストリームストアを使用する必要があります。 SymSrv は、ダウンストリームストアにキャッシュする前にすべてのファイルを圧縮解除します。

### <a name="span-iddeleting_the_cachespanspan-iddeleting_the_cachespandeleting-the-cache"></a><span id="deleting_the_cache"></span><span id="DELETING_THE_CACHE"></span>キャッシュを削除しています

キャッシュとして*Downstreamstore*を使用している場合は、いつでもこのディレクトリを削除してディスク領域を節約できます。

多くの異なるプログラムまたは Windows バージョンのシンボルファイルを含む膨大なシンボルストアを用意することができます。 対象のコンピューターで使用されている Windows のバージョンをアップグレードする場合、キャッシュされたシンボルファイルはすべて以前のバージョンと一致します。 キャッシュされたこれらのファイルは、それ以上使用されないため、キャッシュを削除することをお勧めします。

### <a name="span-idcascading_downstream_storesspanspan-idcascading_downstream_storesspancascading-downstream-stores"></a><span id="cascading_downstream_stores"></span><span id="CASCADING_DOWNSTREAM_STORES"></span>カスケードダウンストリームストア

任意の数のダウンストリームストアをアスタリスクで区切って指定できます。 これらのストアは、*カスケードシンボルストア*として知られています。

最初の**srv \\ *** または**symsrv \\ **<strong>serverdll</strong> * \* * * の後に、後続の各トークンはシンボルの場所を表します。 一番遠い方のトークンが最初にチェックされます。 空のトークン。行に2つのアスタリスクが示されるか、文字列の末尾にアスタリスクで示されます。既定の下流ストアを表します。

次に示すのは、2つの下流ストアを使用して、アクセスされているメインシンボルストアからの情報を保持するシンボルパスの例です。 これらは、マスターストア、中間レベルストア、およびローカルキャッシュと呼ばれることがあります。

```console
srv*c:\localcache*\\interim\store*https://msdl.microsoft.com/download/symbols
```

このシナリオでは、SymSrv は最初に \\ シンボルファイルの c: localcache を検索します。 見つかった場合は、パスを返します。 見つからない場合は、中間ストアに表示され \\ \\ \\ ます。 シンボルファイルが見つかった場合、SymSrv はそれを c: \\ localcache にコピーし、パスを返します。 見つからない場合、SymSrv は[Microsoft パブリックシンボルストア](microsoft-public-symbols.md)をで検索します <https://msdl.microsoft.com/download/symbols> 。ファイルが見つかった場合、symsrv はそれを \\ \\ 中間 \\ ストアと c: localcache の両方にコピーし \\ ます。

同様の動作は、次のパスを使用して取得されます。

```console
srv**\\interim\store*https://internetsite
```

この場合、ローカルキャッシュは既定の下流ストアで、マスターストアはインターネットサイトです。 中間ストアの中間レベルのストア \\ \\ が、他の \\ 2 つの間で使用するように指定されています。

SymSrv は、カスケードストアを含むパスを処理するときに、読み取りまたは書き込みができないストアをスキップします。 そのため、共有がダウンした場合、見つからないストアから下流のストアにファイルがコピーされ、エラーは発生しません。 このエラーの優れた副作用は、マスターストアが書き込み可能でない限り、1つの下流ストアのストリームをフィードする複数のマスターストアをユーザーが指定できることです。

圧縮されたシンボルファイルは、マスターストアから取得されると、中間レベルのストアの圧縮された形式で格納されます。 ファイルは、パスの一番下のストアで圧縮解除されます。

### <a name="span-idworking_with_http_and_smb__symbol_server_pathsspanspan-idworking_with_http_and_smb__symbol_server_pathsspanspan-idworking_with_http_and_smb__symbol_server_pathsspanworking-with-http-and-smb-symbol-server-paths"></a><span id="Working_With_HTTP_and_SMB__Symbol_Server_Paths"></span><span id="working_with_http_and_smb__symbol_server_paths"></span><span id="WORKING_WITH_HTTP_AND_SMB__SYMBOL_SERVER_PATHS"></span>HTTP および SMB シンボルサーバーパスの操作

既に説明したように、チェーン (またはカスケード) とは、 \* シンボルパス内の各区切り記号の間に出現するコピーを指します。 シンボルは、左から右への順序で検索されます。 各ミスでは、ファイルが見つかるまで、次の (上流の) シンボルサーバーが照会されます。

見つかった場合は、(アップストリーム) シンボルサーバーから以前の (下流の) シンボルサーバーにファイルがコピーされます。 これは、(下流の) シンボルサーバーごとに繰り返されます。 このようにして、(共有) ダウンストリームシンボルサーバーには、シンボルサーバーを使用するすべてのクライアントの集合的な作業が設定されます。

チェーンされた UNC パスは、SRV プレフィックスなしでも使用でき \* ますが、 \* symsrv の高度なエラー処理を使用するように srv を指定することをお勧めします。

HTTP シンボルサーバーをパスに含める場合は、1つだけを指定でき (チェーンごとに)、パスの末尾に配置する必要があります (キャッシュとして機能するように書き込むことはできません)。 HTTP ベースのシンボルストアがストアの一覧の中央または左側に配置されている場合、検出されたファイルをコピーしてそのチェーンを破損させることはできません。 さらに、シンボルハンドラーは web サイトからファイルを開くことができないので、HTTP ベースのストアを一番左にしたり、リストにのみ格納したりすることはできません。 SymSrv がこのシンボルパスで表示されている場合、既定の下流ストアがシンボルパスに示されているかどうかに関係なく、ファイルを既定の下流ストアにコピーしてそこから開くことで、回復を試みます。

HTTP は、SRV \* プレフィックス (symsrv シンボルハンドラーによって実装されている) を使用する場合にのみサポートされます。

**HTTP および SMB 共有シンボルサーバーのシナリオ例**

一般的な UNC のみの展開には、すべてのファイル ( \\ \\ mainoffice シンボル) をホストする中央オフィス、 \\ サブセット (BranchOfficeA シンボル) をキャッシュするブランチオフィス、 \\ \\ \\ および参照するファイルをキャッシュするデスクトップ (C: \\ シンボル) が含まれます。

```console
srv*C:\Symbols*\\BranchOfficeA\Symbols*\\MainOffice\Symbols
```

SMB 共有がプライマリ (アップストリーム) シンボルストアの場合は、Read が必要です。

```console
srv*C:\Symbols*\\MachineName\Symbols
```

SMB 共有が中間 (下流) シンボルストアの場合は、読み取り/変更が必要です。 クライアントは、プライマリシンボルストアから SMB 共有にファイルをコピーし、SMB 共有からローカルフォルダーにコピーします。

```console
srv*C:\Symbols*\\MachineName\Symbols*https://msdl.microsoft.com/download/symbols
srv*C:\Symbols*\\MachineName\Symbols*\\MainOffice\Symbols
```

SMB 共有が SymProxy 展開で中間 (下流) シンボルストアである場合は、読み取りのみが必要です。 SymProxy ISAPI フィルターは、クライアントではなく書き込みを実行します。

```console
srv*C:\Symbols*\\MachineName\Symbols*https://SymProxyName/Symbols
```

**複数の HTTP および SMB 共有シンボルサーバーのキャッシュシナリオ**

シンボルサーバーとキャッシュの場所の複数のチェーンを、セミコロン ";" で区切って指定できます。 シンボルが最初のチェーンに配置されている場合、2番目のチェーンは走査されません。 シンボルが最初のチェーンに存在しない場合は、2番目のチェーンが走査され、シンボルが2番目のチェーンにある場合は、指定した場所にキャッシュされます。 この方法では、最初のチェーンで指定されたプライマリシンボルサーバーでシンボルが使用できない場合に、プライマリシンボルサーバーを通常使用することができます。セカンダリサーバーは使用されません。

```console
srv*C:\Symbols*\\Machine1\Symbols*https://SymProxyName/Symbols;srv*C:\WebSymbols* https://msdl.microsoft.com/download/symbols
```

### <a name="span-idcache_localsymbolcachespanspan-idcache_localsymbolcachespancachelocalsymbolcache"></a><span id="cache_localsymbolcache"></span><span id="CACHE_LOCALSYMBOLCACHE"></span>\**localシンボルキャッシュ*をキャッシュする

シンボルのローカルキャッシュを作成するもう1つの方法は、シンボルパス内の**cache \\ **<em>* localsymbol cache</em>文字列を使用することです。 これは、シンボルサーバー要素の一部ではなく、シンボルパス内の個別の要素です。 デバッガーは、指定されたディレクトリ*localsymbol キャッシュ*を使用して、この文字列の右側のシンボルパスに出現する任意の要素から読み込まれたすべてのシンボルを格納します。 これにより、シンボルサーバーによってダウンロードされたシンボルだけでなく、任意の場所からダウンロードしたシンボルに対してローカルキャッシュを使用できます。

たとえば、次のシンボルパスでは、 * \\ \\ someshare*から取得したシンボルはキャッシュされません。 他の共有から取得したシンボルをキャッシュするには、c: mysymbols を使用します。これは、別の共有 \\ で始まる要素* \\ \\ * * \\ \\ *が**cache \* c: \\ mysymbols**要素の右側に表示されるためです。 また、c: mysymbols を使用して、 \\ Microsoft パブリックシンボルストアから取得したシンボルをキャッシュします。これは、シンボルサーバーで使用される通常の構文 (2 つ以上のアスタリスクを持つ**srv** ) が原因です。 さらに、後で[**sympath +**](-sympath--set-symbol-path-.md)コマンドを使用してこのパスに場所を追加すると、これらの新しい要素もキャッシュされます。これは、パスの右側に追加されるためです。

```console
_NT_SYMBOL_PATH=\\someshare\that\cachestar\ignores;srv*c:\mysymbols*https://msdl.microsoft.com/download/symbols;cache*c:\mysymbols;\\anothershare\that\gets\cached
```

### <a name="span-idhow_symsrv_locates_filesspanspan-idhow_symsrv_locates_filesspanhow-symsrv-locates-files"></a><span id="how_symsrv_locates_files"></span><span id="HOW_SYMSRV_LOCATES_FILES"></span>SymSrv がファイルを検索する方法

SymSrv は、目的のシンボルファイルへの完全修飾 UNC パスを作成します。 このパスは、 \_ NT \_ シンボルパス環境変数に記録されたシンボルストアへのパスで始まり \_ ます。 次に、**シンボルサーバー**ルーチンを使用して、目的のファイルの名前を識別します。この名前は、ディレクトリ名としてパスに追加されます。 2つのパラメーターの連結で構成される別のディレクトリ名*と、* *2*つの**SymbolServer**パラメーターと*3*つのパラメーターが追加されます。 これらの値のいずれかが0の場合、省略されます。

結果として得られるディレクトリでは、シンボルファイルまたはシンボルストアポインターファイルが検索されます。

この検索が成功した場合、**シンボルサーバー**は呼び出し元にパスを渡し、 **TRUE**を返します。 ファイルが見つからない場合、**シンボルサーバー**は**FALSE**を返します。

### <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>AgeStore を使用してキャッシュサイズを小さくする

AgeStore ツールを使用すると、指定した日付よりも古いキャッシュファイルを削除したり、キャッシュの内容を指定されたサイズより小さくしたりすることができます。 これは、ダウンストリームストアが大きすぎる場合に便利です。 詳細については、「 [Agestore](agestore.md)」を参照してください。

 

 





