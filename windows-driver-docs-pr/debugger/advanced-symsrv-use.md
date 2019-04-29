---
title: SymSrv の高度な使用方法
description: SymSrv の高度な使用方法
ms.assetid: 16d4dda0-4bcf-4450-9972-e20d71efc845
keywords:
- SymSrv の機能
- シンボルのキャッシュ
- キャッシュのシンボル サーバー
- キャッシュのシンボル
- シンボル サーバーをダウン ストリームのストア
- ダウン ストリームのストア (シンボル サーバー)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 566163bd79334c22c2b094ab08975af1b03b439c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327366"
---
# <a name="advanced-symsrv-use"></a>SymSrv の高度な使用方法


SymSrv を一元的なシンボル ストアからシンボル ファイルを配信できます。 このストアは、プログラムまたはオペレーティング システムの任意の数に対応する、シンボル ファイルの任意の数を含めることができます。 ストアは、バイナリ ファイル (これは便利なミニダンプをデバッグするときに) を含めることもできます。

ストアは、実際の記号と、バイナリ ファイルに含めることができますか、単にシンボル ファイルへのポインターが含めることができます。 場合は、ストアには、ポインターが含まれている、SymSrv はそのソースから直接、実際のファイルを取得します。

SymSrv が特殊なデバッグ タスクに適した小規模なサブセットに大規模なシンボル ストアを分離することもできます。

最後に、SymSrv では、オペレーティング システムによって提供されるログオン情報を使用して、HTTP または HTTPS のソースからシンボル ファイルを取得することができます。 SymSrv には、スマート カード、証明書、および通常のログインおよびパスワードで保護されている HTTPS サイトがサポートしています。 詳細については、次を参照してください。 [HTTP シンボル ストア](http-symbol-stores.md)します。

### <a name="span-idsettingthesymbolpathspanspan-idsettingthesymbolpathspansetting-the-symbol-path"></a><span id="setting_the_symbol_path"></span><span id="SETTING_THE_SYMBOL_PATH"></span>シンボル パスを設定します。

このシンボル サーバーを使用するには、デバッガーと同じディレクトリに symsrv.dll をインストールする必要があります。 シンボル パスは、次に示すように設定できます。

```console
set _NT_SYMBOL_PATH = symsrv*ServerDLL*DownstreamStore*\\Server\Share 

set _NT_SYMBOL_PATH = symsrv*ServerDLL*\\Server\Share 

set _NT_SYMBOL_PATH = srv*DownstreamStore*\\Server\Share 

set _NT_SYMBOL_PATH = srv*\\Server\Share 
```

この構文の一部は以下のとおりです。

<span id="________symsrv"></span><span id="________SYMSRV"></span> **symsrv**  
このキーワードは、最初に常に指定する必要があります。 デバッガーに示すこの項目が通常のシンボルのディレクトリだけでなく、シンボル サーバーであります。

<span id="ServerDLL"></span><span id="serverdll"></span><span id="SERVERDLL"></span>*ServerDLL*  
シンボル サーバー DLL の名前を指定します。 SymSrv のシンボル サーバーを使用している場合は、常に symsrv.dll します。

<span id="srv"></span><span id="SRV"></span>**srv**  
これは、短縮形**symsrv\*symsrv.dll**します。

<span id="DownstreamStore"></span><span id="downstreamstore"></span><span id="DOWNSTREAMSTORE"></span>*DownstreamStore*  
ダウン ストリームのストアを指定します。 これは、個々 のシンボル ファイルをキャッシュに使用されるローカル ディレクトリまたはネットワーク共有です。

アスタリスクで区切られた 1 つ以上のダウン ストリーム ストアを指定することができます。 複数のダウン ストリーム ストアについてで**カスケード Downstream ストア**このページの後半。

ダウン ストリームのストアが指定すると通常の行に 2 つのアスタリスクを含めると、既定のダウン ストリーム ストアが使用されます。 このストアは、ホーム ディレクトリの sym サブディレクトリに配置されます。 ホーム ディレクトリの既定値は、デバッガーのインストール ディレクトリ。使用してこれを変更することができます、 [ **! homedir** ](-homedir.md)拡張機能を設定、DBGHELP\_HOMEDIR 環境変数。

場合*DownstreamStore*が存在しないディレクトリを指定 SymStore はそれを作成しようとしています。

場合、 *DownstreamStore*パラメーターを省略して、余分なアスタリスクが含まれていない - つまり、使用する場合**srv**正確に 1 つのアスタリスクまたは**symsrv**正確に 2 つのアスタリスク--しないダウン ストリームのストアが作成されます。 ローカルにキャッシュせず、サーバーから直接、デバッガーはすべてのシンボル ファイルを読み込みます。

**注**  シンボルは、HTTP または HTTPS サイトからアクセスしているかどうか、またはシンボル ストアでは、圧縮されたファイルを使用すると、ダウン ストリームのストアは常に使用します。 ダウン ストリームのストアが指定されていない場合、1 つが、sym、ホーム ディレクトリのサブディレクトリに作成されます。

 

<span id="__Server_Share"></span><span id="__server_share"></span><span id="__SERVER_SHARE"></span>*\\\\Server\\共有*  
サーバーとのリモート シンボル ストア共有を指定します。

ダウン ストリームのストアを使用する場合、デバッガーは、まずこのストア内のシンボル ファイル。 指定された対象からシンボル ファイルの検索は、デバッガー シンボル ファイルが見つからない場合*Server*と*共有*、ダウン ストリームのストアにこのファイルのコピーをキャッシュします。 ツリーの下にサブディレクトリをファイルがコピーされる*DownstreamStore*の下のツリー内の場所に対応する *\\ \\Server\\共有*します。

シンボル サーバーをシンボル パスのエントリのみにする必要はありません。 シンボル パスが複数のエントリで構成される場合、デバッガーがシンボル サーバーまたは実際のディレクトリの名前がかどうかに関係なく (左から右へ) の順に、必要なシンボル ファイルの各エントリをチェックします。

例をいくつか紹介します。 SymSrv サーバーとして使用する、シンボルをシンボル ストアでの\\ \\mybuilds\\mysymbols は、次のシンボル パスを設定します。

```console
set _NT_SYMBOL_PATH= symsrv*symsrv.dll*\\mybuilds\mysymbols
```

デバッガーは上のシンボル ストアからシンボル ファイルをコピーするために、シンボル パスを設定する\\ \\mybuilds\\mysymbols c: ローカル ディレクトリに\\localsymbols を使用します。

```console
set _NT_SYMBOL_PATH=symsrv*symsrv.dll*c:\localsymbols*\\mybuilds\mysymbols
```

デバッガーは、HTTP のサイト www.company.com/manysymbols からシンボル ファイルをローカル ネットワーク ディレクトリにコピーするように、シンボル パスを設定する\\ \\localserver\\myshare\\mycache を使用します。

```console
set _NT_SYMBOL_PATH=symsrv*symsrv.dll*\\localserver\myshare\mycache*https://www.company.com/manysymbols
```

この最後の例は、そのためも短縮できます。

```console
set _NT_SYMBOL_PATH=srv*\\localserver\myshare\mycache*https://www.company.com/manysymbols
```

さらに、シンボル パスには、複数のディレクトリまたはセミコロンで区切られた、シンボル サーバーを含めることができます。 これにより、複数の場所 (または複数のシンボル サーバー) からシンボルを検索できます。 バイナリに一致しないシンボル ファイルがある場合は、デバッガーが特定の正確なパラメーターのみをチェックするために、シンボル サーバーを使用することはできません。 ただし、デバッガーは、従来のシンボル パスを使用して、正しい名前を持つ記号が一致しないファイルを検索し、正常に読み込むこと可能性があります。 ファイルには、技術的には、適切なシンボル ファイルではありませんが、有用な情報を提供します。

### <a name="span-idcompressedfilesspanspan-idcompressedfilesspancompressed-files"></a><span id="compressed_files"></span><span id="COMPRESSED_FILES"></span>圧縮されたファイル

この圧縮が使用される compress.exe ツールを使用して行われている限り、SymSrv は圧縮されたファイルが含まれているシンボル ストアと互換性のある[ここ](https://go.microsoft.com/fwlink/p/?linkid=239917)します。 圧縮されたファイルでは、それらのファイル拡張子の最後の文字として、アンダー スコアが必要 (たとえば、module1.pd\_または module2.db\_)。 詳細については、次を参照してください。 [SymStore](symstore.md)します。

ストアのファイルが圧縮されている場合は、ダウン ストリームのストアを使用する必要があります。 SymSrv はダウン ストリームのストアにそれらをキャッシュする前にすべてのファイルを解凍します。

### <a name="span-iddeletingthecachespanspan-iddeletingthecachespandeleting-the-cache"></a><span id="deleting_the_cache"></span><span id="DELETING_THE_CACHE"></span>キャッシュを削除します。

使用する場合、 *DownstreamStore*をキャッシュとして、ディスク領域を節約するには、いつでもこのディレクトリを削除することができます。

多くのさまざまなプログラムまたは Windows のバージョンのシンボル ファイルを含む vast シンボル ストアを含めることは可能になります。 ターゲット コンピューター上で使用する Windows のバージョンをアップグレードする場合、キャッシュされたシンボル ファイルはすべてと一致以前のバージョン。 これらのキャッシュされたファイルは、さらに、使用できませんし、そのためこのキャッシュを削除すると良いなる場合があります。

### <a name="span-idcascadingdownstreamstoresspanspan-idcascadingdownstreamstoresspancascading-downstream-stores"></a><span id="cascading_downstream_stores"></span><span id="CASCADING_DOWNSTREAM_STORES"></span>ダウン ストリームのストアのカスケード

アスタリスクで区切られた、ダウン ストリームのストアの任意の数を指定することができます。 これらのストアと呼ばれる*カスケード型のシンボル ストア*します。

頭文字の後**srv\\*** または**symsrv\\**<strong>ServerDLL</strong>*\** *、以降の各トークンは、シンボルの場所。 一番左のトークンが最初にチェックされます。 -行で、2 つのアスタリスクまたは文字列の末尾のアスタリスクで示される--空のトークンは、既定のダウン ストリームのストアを表します。

アクセスされるメイン シンボル ストアから情報を保持するためにダウン ストリームの 2 つのストアを使用するシンボル パスの例を次に示します。 これらは、マスターのストア、中程度のストア、およびローカル キャッシュ呼び出すことができます。

```console
srv*c:\localcache*\\interim\store*https://msdl.microsoft.com/download/symbols
```

このシナリオで SymSrv は、まず c:\\localcache シンボル ファイル。 見つかった場合に、パスを返します。 表示されることが見つからない場合があります、 \\\\中間\\を格納します。 シンボル ファイルは、そこで見つかった場合は、SymSrv はコピーを c:\\localcache し、パスを返します。 SymSrv で表示されることが見つからない場合があります、 [Microsoft パブリック シンボル ストア](microsoft-public-symbols.md)で<https://msdl.microsoft.com/download/symbols>; ファイルが見つからないかどうかは、SymSrv は両方にコピー \\\\中間\\ストアと c:\\localcache します。

次のパスを使用して同様の動作を取得します。

```console
srv**\\interim\store*https://internetsite
```

この場合は、ローカル キャッシュは既定のダウン ストリーム ストアとし、マスターの保存はインターネット サイトとします。 中程度ストア\\\\中間\\他の 2 つの間使用してストアが指定されています。

SymSrv カスケード ストアを含むパスを処理するときは、読み取りまたは書き込みができないストアをスキップします。 ので、共有がダウンした場合、ダウン ストリームのストアにファイルをコピー エラーなし、不足しているストアから、されます。 このエラーのメリットは、ユーザーがマスターのストアが書き込み可能でない限り、ダウン ストリームのストアの 1 つのストリームをフィードする複数のマスター ストアを指定できます。

圧縮されたシンボル ファイルはマスター ストアから取得する場合は、中程度のストアに圧縮形式で格納されます。 ファイルは、パスの最下位のストアに圧縮されます。

### <a name="span-idworkingwithhttpandsmbsymbolserverpathsspanspan-idworkingwithhttpandsmbsymbolserverpathsspanspan-idworkingwithhttpandsmbsymbolserverpathsspanworking-with-http-and-smb-symbol-server-paths"></a><span id="Working_With_HTTP_and_SMB__Symbol_Server_Paths"></span><span id="working_with_http_and_smb__symbol_server_paths"></span><span id="WORKING_WITH_HTTP_AND_SMB__SYMBOL_SERVER_PATHS"></span>HTTP と SMB のシンボル サーバーのパスを使用します。

既に説明した、チェーン (またはカスケード) とそれぞれの間で行われるコピーを指します"\*"シンボル パスの区切り記号。 シンボルは、左から右の順序で検索されます。 各のミスで、[次へ] (アップ ストリーム) シンボル サーバーでクエリを実行、ファイルが見つかるまでです。

かどうか、ファイル (アップ ストリーム) のシンボル サーバーからサーバーにコピーされます、以前 (ダウン ストリーム) シンボル。 これは、(ダウン ストリーム) シンボル サーバーごとに繰り返されます。 この方法で、ダウン ストリーム (共有) のシンボル サーバーには、シンボル サーバーを使用してすべてのクライアントの集合的な取り組みが設定されます。

なし、SRV 連鎖の UNC パスで使用できる場合でも\*プレフィックスをお勧めその SRV\* symsrv.dll の高度なエラー処理を使用するように指定します。

パス内には、HTTP のシンボル サーバーを含む、ときに 1 つだけごとに指定できます (チェーン)、および (キャッシュとして処理するために書き込まれることはできません) とき、パスの末尾にあります。 HTTP ベースでシンボルが、中間またはストアの一覧の左側にある、検出されたファイルをコピーすることはできませんし、チェーンが壊れているでしょう。 さらに、シンボル ハンドラーは、web サイトからファイルを開くことはできません、ため、HTTP ベースのストアまたはしないでください、左端にあるのみをリストに格納します。 このパスとシンボル SymSrv が表示されること場合、をファイルを既定のダウン ストリームのストアにコピーして復旧し、既定のダウン ストリーム ストアがシンボル パスに示されているかどうかどうかに関係なく、そこから開いて試みます。

HTTP が、SRV を使用する場合にのみサポートされている\*プレフィックス (symsrv.dll シンボル ハンドラーによって実装される)。

**例 HTTP と SMB 共有のシンボル サーバーのシナリオ**

一般的な UNC のみのデプロイは、すべてのファイルをホストしているセントラル オフィス (\\\\MainOffice\\記号)、ブランチ オフィスのキャッシュのサブセット (\\\\BranchOfficeA\\記号)、デスクトップ (c:\\記号) を参照するファイルをキャッシュします。

```console
srv*C:\Symbols*\\BranchOfficeA\Symbols*\\MainOffice\Symbols
```

SMB 共有は、プライマリ (アップ ストリーム) シンボル ストアが、読み取りが必要です。

```console
srv*C:\Symbols*\\MachineName\Symbols
```

SMB 共有は、中間 (下位) シンボルが、読み取りと変更が必要です。 SMB 共有にプライマリ シンボル ストアから、ローカル フォルダーに SMB 共有から、クライアントは、ファイルをコピーします。

```console
srv*C:\Symbols*\\MachineName\Symbols*https://msdl.microsoft.com/download/symbols
srv*C:\Symbols*\\MachineName\Symbols*\\MainOffice\Symbols
```

SMB 共有が SymProxy 展開で、中間 (下位) シンボル ストアの場合は、読み取りのみが必要です。 SymProxy ISAPI フィルターでは、クライアントではなく、書き込みを実行します。

```console
srv*C:\Symbols*\\MachineName\Symbols*https://SymProxyName/Symbols
```

**複数の HTTP と SMB 共有シンボル サーバーのキャッシュ シナリオ**

シンボル サーバーの複数のチェーンを指定し、セミコロンで区切られた場所をキャッシュすることは「;」します。 シンボルは、最初のチェーンに存在する場合は、2 番目のチェーンは走査されません。 シンボルは、最初のチェーンにない場合は、2 番目のチェーンを走査して、シンボルは、2 番目のチェーンに存在する場合、指定した場所にキャッシュがします。 このアプローチは通常、サーバーで使用される、セカンダリのみが使用されている、シンボルが最初のチェーンで指定されたプライマリのシンボル サーバーの利用できない場合にプライマリのシンボル サーバーを許可します。

```console
srv*C:\Symbols*\\Machine1\Symbols*https://SymProxyName/Symbols;srv*C:\WebSymbols* https://msdl.microsoft.com/download/symbols
```

### <a name="span-idcachelocalsymbolcachespanspan-idcachelocalsymbolcachespancachelocalsymbolcache"></a><span id="cache_localsymbolcache"></span><span id="CACHE_LOCALSYMBOLCACHE"></span>cache\**localsymbolcache*

シンボルのローカル キャッシュを作成する別の方法を使用して、**キャッシュ\\**<em>* localsymbolcache</em>シンボル パス文字列。 Symbol server 要素が、シンボル パスに個別の要素の一部ではありません。 デバッガーが、指定されたディレクトリを使用して*localsymbolcache*シンボル パスにこの文字列の右側に表示される任意の要素から読み込まれたすべてのシンボルを格納します。 これにより、シンボル サーバーによってダウンロードされたものだけでなく、任意の場所からダウンロードしたシンボルをローカル キャッシュを使用することができます。

たとえば、次のシンボル パスではから取得したシンボルをキャッシュしません *\\ \\someshare*します。 C: を使用する\\から取得したシンボルをキャッシュする mysymbols  *\\ \\anothershare*ため、要素が始まる *\\ \\anothershare*の右側に表示されます、**キャッシュ\*c:\\mysymbols**要素。 C: は使用も\\mysymbols シンボル サーバーによって使用される通常の構文が、Microsoft パブリック シンボル ストアから取得したシンボルをキャッシュする (**srv** 2 つ以上のアスタリスクで)。 さらに、その後に使用する場合、 [ **.sympath +** ](-sympath--set-symbol-path-.md)このパスに追加の場所を追加するコマンドでこれらの新しい要素もキャッシュされます、ため、パスの右側に追加されます。

```console
_NT_SYMBOL_PATH=\\someshare\that\cachestar\ignores;srv*c:\mysymbols*https://msdl.microsoft.com/download/symbols;cache*c:\mysymbols;\\anothershare\that\gets\cached
```

### <a name="span-idhowsymsrvlocatesfilesspanspan-idhowsymsrvlocatesfilesspanhow-symsrv-locates-files"></a><span id="how_symsrv_locates_files"></span><span id="HOW_SYMSRV_LOCATES_FILES"></span>SymSrv がファイルを検索する方法

SymSrv は、必要なシンボル ファイルへの完全修飾 UNC パスを作成します。 このパスに記録されているシンボル ストアへのパスで始まる、 \_NT\_シンボル\_PATH 環境変数。 **SymbolServer**ルーチンは、目的のファイルの名前を識別するために使用し、ディレクトリ名とパスにこの名前が追加されます。 連結から成る別のディレクトリ名、 *id*、 *2 つ*、および*3*に渡されるパラメーター **SymbolServer**は次に追加します。 これらの値が 0 の場合省略されます。

シンボル ファイル、またはシンボル ストア ポインター ファイル、結果のディレクトリが検索されます。

この検索が成功すると場合、 **SymbolServer** 、呼び出し元へのパスを返します**TRUE**します。 ファイルが見つからない場合**SymbolServer**返します**FALSE**します。

### <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>AgeStore を使用して、キャッシュのサイズを小さくには

AgeStore ツールは、指定した日付より古いキャッシュ ファイルを削除するか、指定したサイズ以下のキャッシュの内容を削減することできます。 ダウン ストリーム ストアが大きすぎる場合に役立ちます。 ことができます。 詳細については、次を参照してください。 [AgeStore](agestore.md)します。

 

 





