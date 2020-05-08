---
title: 言語の仕様 1
description: 言語の仕様 1
ms.assetid: 7c770200-ed2a-47e0-8389-e79a5624a3dd
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4334732130a0db42fa066fe1015901788bf24be2
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925625"
---
# <a name="language-specification-1"></a>言語の仕様 1


SrcSrv の最初のバージョンは次のように動作します。 (この動作は将来のバージョンで変更される可能性があります)。

最初に、クライアントは、すべてのソースファイル抽出のベースとして使用されるターゲットパスを使用して、 **Srcsrvinit**を呼び出します。 このパスは、特別な変数 TARG に格納されます。

DbgHelp がモジュールの .pdb ファイルを読み込むと、.pdb ファイルから SrcSrv ストリームを抽出し、 **SrcSrvLoadModule**を呼び出すことによって、このデータブロックを srcsrv に渡します。

次に、DbgHelp がソースファイルを取得する必要があるときに、 **Srcsrvgetfile**を呼び出して、指定されたソースファイルをバージョンコントロールから取得します。

SrcSrv は、要求されたソース仕様と正確に一致するエントリのデータブロック内のすべてのソースファイルエントリをレビューします。 この一致は、VAR1 で見つかります。

SrcSrv によってエントリが検出されると、このソースファイルエントリの内容と共に、特別な変数 (VAR1、VAR2 など) が入力されます。 次に、これらの特殊な変数を使用して、SRCSRVTRG 変数を解決します。

次に、特別な変数を使用して SRCSRVTRG 変数を解決する方法を示します。 ソースパスは引き続き次のようになります。

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3
```

各行は、1つの特殊な変数の解決方法を示しています。 解決された変数は太字です。

```console
SRCSRVTRG=%sdtrg% 
SDTRG=%targ%\%var2%\%fnbksl%(%var3%)\%var4%\%fnfile%(%var1%)
c:\src\%var2%\%fnbksl%(%var3%)\%var4%\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\%fnbksl%(%var3%)\%var4%\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\%fnbksl%( sdktools/debuggers/srcsrv/shell.cpp )\%var4%\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\ sdktools\debuggers\srcsrv\shell.cpp\%var4%\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\%fnfile%( c:\db\srcsrv\shell.cpp)
c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp
```

この生成されたターゲットパスが一意であり、同じファイルの2つのバージョンを同じ場所に抽出することを許可していないことに注意してください。

SrcSrv によって、ファイルが既に存在するかどうかが確認されるようになりました。 指定されている場合、SrcSrv は呼び出し元に位置を返します。 それ以外の場合、SrcSrv は SRCSRVCMD を解決して、ファイルを抽出する実行コマンドをビルドします。

次の例では、各行に1つの特殊な変数の解像度が示されています。 解決された変数は太字です。

```console
DEPOT=//depot 
WIN_SDKTOOLS= sserver.microsoft.com:4444 
SRCSRVCMD=%sdcmd% 
SDCMD=sd.exe -p %fnvar%(%var2%) print -o %srcsrvtrg% -q %depot%/%var3%#%var4% 
sd.exe -p %fnvar%(WIN_SDKTOOLS) print -o %srcsrvtrg% -q %depot%/%var3%#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o %srcsrvtrg% -q %depot%/%var3%#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp -q %depot%/%var3%#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp -q //depot/%var3%#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp -q //depot/ sdktools/debuggers/srcsrv/shell.cpp#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp -q //depot/ sdktools/debuggers/srcsrv/shell.cpp#3 
```

これで、SrcSrv がこのコマンドを実行します。 このコマンドの結果が予期される場所にあるファイルの場合、このパスは呼び出し元に返されます。

変数を解決できない場合は、OS 環境変数として参照しようとすることに注意してください。 失敗した場合は、処理中のテキストから変数名が削除されます。

2つの連続するパーセント記号は、1つのパーセント記号として解釈されます。

### <a name="span-idsource_server_data_blocksspanspan-idsource_server_data_blocksspansource-server-data-blocks"></a><span id="source_server_data_blocks"></span><span id="SOURCE_SERVER_DATA_BLOCKS"></span>ソースサーバーのデータブロック

SrcSrv は、.pdb ファイル内の2つのデータブロック (ソースファイルリストとデータブロック) に依存します。

ソースファイルの一覧は、モジュールのビルド時に自動的に作成されます。 この一覧には、モジュールのビルドに使用されるソースファイルへの完全修飾パスが含まれています。

データブロックは、ソースのインデックス作成中に作成されます。 この時点で、"srcsrv" という名前の代替ストリームが .pdb ファイルに追加されます。 このデータを挿入するスクリプトは、使用されている特定のビルドプロセスとソース管理システムに依存します。

データブロックは、ini、変数、およびソースファイルの3つのセクションに分かれています。 データブロックの構文は次のとおりです。

```console
SRCSRV: ini ------------------------------------------------ 
VERSION=1
VERCTRL=<source_control_str>
DATETIME=<date_time_str>
SRCSRV: variables ------------------------------------------ 
SRCSRVTRG=%sdtrg% 
SRCSRVCMD=%sdcmd% 
SRCSRVENV=var1=string1\bvar2=string2 
DEPOT=//depot 
SDCMD=sd.exe -p %fnvar%(%var2%) print -o %srcsrvtrg% -q %depot%/%var3%#%var4% 
SDTRG=%targ%\%var2%\%fnbksl%(%var3%)\%var4%\%fnfile%(%var1%) 
WIN_SDKTOOLS= sserver.microsoft.com:4444 
SRCSRV: source files --------------------------------------- 
<path1>*<var2>*<var3>*<var4> 
<path2>*<var2>*<var3>*<var4> 
<path3>*<var2>*<var3>*<var4> 
<path4>*<var2>*<var3>*<var4> 
SRCSRV: end ------------------------------------------------
```

パーセント記号 (%) で囲まれたテキストを除き、すべてのテキストは文字どおりに解釈されます。 パーセント記号で囲まれたテキストは、次のいずれかの関数でない限り、再帰的に解決される変数名として扱われます。

<span id="_fnvar___"></span><span id="_FNVAR___"></span>**% fnvar% ()**  
パラメーターテキストはパーセント記号で囲み、解決する変数として処理する必要があります。

<span id="_fnbksl___"></span><span id="_FNBKSL___"></span>**% fnbksl% ()**  
パラメーターテキスト内のすべてのスラッシュ (/) は、円記号 (\)) に置き換える必要があります。

<span id="_fnfile___"></span><span id="_FNFILE___"></span>**% fnfile% ()**  
パラメーターテキスト内のすべてのパス情報は、ファイル名だけを残して、削除する必要があります。

データ\[ブロック\]の ini セクションには、要件を説明する変数が含まれています。 インデックス作成スクリプトでは、このセクションに任意の数の変数を追加できます。 次に例を示します。

<span id="VERSION"></span><span id="version"></span>**バージョン**  
言語仕様のバージョン。 この変数は必須です。 現在の言語仕様に基づいてスクリプトを開発する場合は、この値を1に設定します。 SrcSrv クライアントコードは、独自の値より大きい値を持つスクリプトを実行しようとしません。 SrcSrv の現在のバージョンでは、値2を使用します。

<span id="VERCTL"></span><span id="verctl"></span>**VERCTL**  
ソースバージョンコントロールシステムを説明する文字列。 この変数は省略可能です。

<span id="DATETIME"></span><span id="datetime"></span>**/**  
.Pdb ファイルが処理された日付と時刻を示す文字列。 この変数は省略可能です。

データ\[ブロック\]の variables セクションには、ソース管理からファイルを抽出する方法を記述する変数が含まれています。 また、データブロックのサイズを小さくするために、一般的に使用されるテキストを変数として定義するために使用することもできます。

<span id="SRCSRVTRG"></span><span id="srcsrv"></span>**SRCSRVTRG**  
抽出されたファイルのターゲットパスを作成する方法について説明します。 これは必須の変数です。

<span id="SRCSRVCMD"></span><span id="srcsrvcmd"></span>**SRCSRVCMD**  
ソース管理からファイルを抽出するコマンドを作成する方法について説明します。 これには、実行可能ファイルの名前とコマンドラインパラメーターが含まれます。 これは、任意の抽出コマンドを実行する必要がある場合に必要です。

<span id="SRCSRVENV"></span><span id="srcsrvenv"></span>**SRCSRベンダー**  
ファイルの抽出中に作成される環境変数を一覧表示します。 これは文字列です。 複数のエントリをバックスペース文字 (\\b) で区切ります。 これは省略可能な変数です。

<span id="SRCSRVVERCTRL"></span><span id="srcsrvverctrl"></span>**SRCSRVVERCTRL**  
使用するバージョンコントロールシステムを指定します。 Perforce の場合、これは perforce です。 Visual SourceSafe の場合、これは vss です。 Team Foundation Server の場合、これは tfs です。 この変数は、サーバーエラーを永続化するために使用されます。 これは省略可能な変数です。

<span id="SRCSRVVERRDESC"></span><span id="srcsrvverrdesc"></span>**SRCSRVVERRDESC**  
抽出するソースファイルが含まれているサーバーにバージョンコントロールクライアントが接続できない場合に表示するテキストを指定します。 SrcSrv は、この値を使用して接続の問題を確認します。 これは省略可能な変数です。

<span id="SRCSRVERRVAR"></span><span id="srcsrverrvar"></span>**SRCSRVERRVAR**  
ファイルエントリ内のどの変数がバージョンコントロールサーバーに対応するかを示します。 これは、以前の障害に基づいて、機能しないコマンドを識別するために SrcSrv によって使用されます。 テキストの形式は **var * * * x*です。 *x*は、指定されている変数の番号です。 これは省略可能な変数です。

データ\[ブロックの\] source files セクションには、インデックスが作成された各ソースファイルのエントリが含まれています。 各行の内容は、「VAR1、VAR2、VAR3 など」という名前の変数として解釈されます。 変数はアスタリスクで区切られます。 VAR1 は、.pdb ファイル内の他の場所にあるソースファイルへの完全修飾パスを指定する必要があります。 次に例を示します。

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3 
```

は次のように解釈されます。

```console
VAR1=c:\proj\src\file.cpp
VAR2=TOOLS_PRJ
VAR3=tools/mytool/src/file.cpp
VAR4=3
```

この例では、VAR4 はリビジョン番号です。 ただし、ほとんどのソース管理システムでは、特定のビルドのソース状態を復元できるように、ファイルのラベル付けがサポートされています。 そのため、代わりにビルドのラベルを使用できます。 サンプルデータブロックは、次のような変数を含むように変更できます。

```console
LABEL=BUILD47 
```

次に、ソース管理システムがラベルを示すためにアットマーク (@) を使用することを前提として、SRCSRVCMD 変数を次のように変更できます。

```console
sd.exe -p %fnvar%(%var2%) print -o %srcsrvtrg% -q %depot%/%var3%@%label%
```

### <a name="span-idhandling_server_errorsspanspan-idhandling_server_errorsspanhandling-server-errors"></a><span id="handling_server_errors"></span><span id="HANDLING_SERVER_ERRORS"></span>サーバーエラーの処理

クライアントが1つのバージョンコントロールサーバーからすべてのファイルを抽出できない場合があります。 これは、サーバーがダウンしてネットワークから切断されているか、ユーザーがソースにアクセスするための適切な特権を持っていないことが原因である可能性があります。 ただし、このソースを取得しようとすると時間が大幅に低下する可能性があります。 このような状況では、使用できないことが証明されたソースからの抽出を無効にすることをお勧めします。

SrcSrv は、ファイルの抽出に失敗するたびに、コマンドによって生成された出力テキストを調べます。 このコマンドのいずれかの部分に SRCSRVERRDESC の内容と完全に一致するものが含まれている場合、同じバージョン管理サーバーに対する今後のコマンドはすべてスキップされます。 複数のエラー文字列を定義するには、数値または任意のテキストを SRCSRVERRDESC 変数名の末尾に追加します。 たとえば次のようになります。

```console
SRCSRVERRDESC=lime: server not found
SRCSRVERRDESC_2=pineapple: network error
```

サーバーの id は、SRCSRVERRVAR から取得されます。 したがって、SRCSRVERRVAR に "var2" が含まれていて、.pdb ファイル内のファイルエントリが次のようになっているとします。

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3
```

変数2の "TOOLS\_拡張子が .prj" を含むファイルエントリを使用してソースを取得しようとすると、その後のすべての試行はバイパスされます。

[Srcsrv .ini](the-srcsrv-ini-file.md)を編集して、デバッガークライアントにエラーインジケーターを追加することもできます。 詳細については、srcsrv の付属のサンプルバージョンを参照してください。

 

 





