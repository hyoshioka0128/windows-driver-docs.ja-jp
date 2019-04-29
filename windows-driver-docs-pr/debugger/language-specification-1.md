---
title: 言語の仕様 1
description: 言語の仕様 1
ms.assetid: 7c770200-ed2a-47e0-8389-e79a5624a3dd
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55a81ac47ec93c8000e0c0c7ba8b4c36406d5d40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383516"
---
# <a name="language-specification-1"></a>言語の仕様 1


SrcSrv の最初のバージョンはように動作します。 (この動作が変更将来のバージョン)。

最初に、クライアントが呼び出す**SrcSrvInit**すべてのソース ファイルの抽出のベースとして使用するターゲット パスを使用します。 このパスは、特殊な変数のターゲットに格納されます。

.Pdb ファイルから SrcSrv ストリームを抽出しを呼び出して SrcSrv にこのデータ ブロックを渡しますがモジュールの .pdb ファイルが読み込まれる DbgHelp **SrcSrvLoadModule**します。

呼び出して DbgHelp は、ソース ファイルを取得する必要がある、 **SrcSrvGetFile**をバージョン コントロールから指定されたソース ファイルを取得します。

SrcSrv では、要求されたソースの仕様では正確に一致するエントリのデータ ブロックのすべてのソース ファイルのエントリを確認します。 VAR1 では、この一致が見つかった。

SrcSrv には、エントリが検出されると後でこのソース ファイルのエントリの内容 (VAR1、VAR2 など) の特殊な変数で塗りつぶします。 SRCSRVTRG 変数は、これらの特殊な変数を使用して解決されます。

SRCSRVTRG 変数は、次の表示、特別な変数を使用して解決します。 そのソース パスがまだと仮定します。

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3 
```

各行には、1 つの特殊な変数の解像度が表示されます。 解決された変数は太字です。

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

この生成されたターゲット パスの一意では、同じ場所に抽出する同じファイルの 2 つのバージョンを許可しないことを確認します。

SrcSrv はファイルが既に存在して次のようです。 場合は、SrcSrv は呼び出し元に場所を返します。 それ以外の場合、SrcSrv SRCSRVCMD を解決することで、ファイルを抽出する実行コマンドを構築します。

次の例では、各の行は、1 つの特殊な変数の解決方法を示しています。 解決された変数は太字です。

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

SrcSrv がこのコマンドを実行しているようになりました。 このコマンドの結果が予期された場所にファイルの場合は、このパスは、呼び出し元に返されます。

変数を解決できない場合に、しようとが OS 環境変数として検索する行われたことに注意してください。 失敗した場合は、変数名は、処理されているテキストから削除されます。

2 つの連続するパーセント記号の文字は、1 つのパーセント記号として解釈されます。

### <a name="span-idsourceserverdatablocksspanspan-idsourceserverdatablocksspansource-server-data-blocks"></a><span id="source_server_data_blocks"></span><span id="SOURCE_SERVER_DATA_BLOCKS"></span>ソース サーバーのデータのブロック

SrcSrv は、.pdb ファイル、ソース ファイルの一覧、およびデータ ブロック内のデータの 2 つのブロックに依存します。

ソース ファイルの一覧は、モジュールのビルド時に自動的に作成されます。 この一覧には、モジュールを構築するために使用するソース ファイルへの完全修飾パスが含まれています。

データ ブロックは、ソースのインデックス作成中に作成されます。 この時点では、別のストリームを"srcsrv"という名前は、.pdb ファイルに追加されます。 このデータを挿入するスクリプトが使用中で特定のビルド プロセスとソース管理システムに依存します。

データ ブロックは 3 つのセクションに分かれています。 ini、変数、およびソース ファイル。 データ ブロックには、次の構文があります。

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

パーセント記号 (%) で囲まれたテキストを除くすべてのテキストが文字どおり、解釈されます。 パーセント記号で囲まれたテキストは、次の関数のいずれかである場合を除き、変数の名前解決の再帰的にすると見なされます。

<span id="_fnvar___"></span><span id="_FNVAR___"></span>**%fnvar%()**  
パラメーターのテキストのパーセント記号で囲まれ、解決される変数として処理する必要があります。

<span id="_fnbksl___"></span><span id="_FNBKSL___"></span>**%fnbksl%()**  
パラメーターのテキストでのすべてのフォワード スラッシュ (/) は、旧バージョンとのスラッシュで置き換える必要があります (\)します。

<span id="_fnfile___"></span><span id="_FNFILE___"></span>**%fnfile%()**  
パラメーターのテキスト内のすべてのパス情報は、ファイル名のみを離れること、削除する必要があります。

\[Ini\]データ ブロックのセクションには、要件を記述する変数が含まれています。 インデックス作成のスクリプトでは、このセクションに任意の数の変数を追加できます。 次に例を示します。

<span id="VERSION"></span><span id="version"></span>**バージョン**  
言語仕様バージョン。 この変数は必須です。 現在の言語仕様に基づくスクリプトを開発する場合は、この値を 1 に設定します。 SrcSrv のクライアント コードは、独自のよりも大きい値を持つ任意のスクリプトを実行しません。 SrcSrv の現在のバージョンでは、2 の値を使用します。

<span id="VERCTL"></span><span id="verctl"></span>**VERCTL**  
ソースのバージョン管理システムを説明する文字列。 この変数は省略可能です。

<span id="DATETIME"></span><span id="datetime"></span>**DATETIME**  
日時を示す文字列の .pdb ファイルが処理されました。 この変数は省略可能です。

\[変数\]データ ブロックのセクションには、ソース管理からファイルを抽出する方法を説明する変数が含まれています。 データ ブロックのサイズを小さく変数としてよく使用されるテキストを定義することにも使用できます。

<span id="SRCSRV"></span><span id="srcsrv"></span>**SRCSRV**  
抽出されたファイルのターゲット パスを構築する方法について説明します。 これは、必要な変数です。

<span id="SRCSRVCMD"></span><span id="srcsrvcmd"></span>**SRCSRVCMD**  
ソース管理からファイルを抽出するコマンドを構築する方法について説明します。 これには、実行可能ファイルとそのコマンド ライン パラメーターの名前が含まれます。 抽出のいずれかのコマンドを実行する必要がある場合に必要です。

<span id="SRCSRVENV"></span><span id="srcsrvenv"></span>**SRCSRVENV**  
ファイルの解凍中に作成される環境変数を一覧表示します。 これは、文字列です。 バック スペース文字に複数のエントリを区切ります (\\b)。 これは、省略可能な変数です。

<span id="SRCSRVVERCTRL"></span><span id="srcsrvverctrl"></span>**SRCSRVVERCTRL**  
使用して、バージョン コントロール システムを指定します。 Perforce、これは perforce です。 Visual SourceSafe は、これは vss. Team Foundation Server では、これは tfs です。 この変数は、サーバー エラーの保持に使用されます。 これは、省略可能な変数です。

<span id="SRCSRVVERRDESC"></span><span id="srcsrvverrdesc"></span>**SRCSRVVERRDESC**  
バージョン コントロールのクライアントが抽出するソース ファイルを含むサーバーに接続できない場合に表示するテキストを指定します。 SrcSrv では、値を使用して、接続の問題を確認します。 これは、省略可能な変数です。

<span id="SRCSRVERRVAR"></span><span id="srcsrverrvar"></span>**SRCSRVERRVAR**  
ファイルのエントリでどの変数がバージョン コントロール サーバーに対応を示します。 SrcSrv では機能せず、以前のエラーに基づいてコマンドを識別するために使用されます。 テキストの形式は **var * * * X*場所*X*は指定されている変数の数です。 これは、省略可能な変数です。

\[ソース ファイル\]データ ブロックのセクションには、インデックスが作成されているソース ファイルごとにエントリが含まれています。 各行の内容は、VAR10 までなど、VAR1 VAR2、VAR3 の名前を持つ変数として解釈されます。 変数は、アスタリスクで区切られます。 VAR1 は、.pdb ファイルを他の場所で記載されているソース ファイルへの完全修飾パスを指定する必要があります。 次に、例を示します。

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3 
```

次のように解釈されます。

```console
VAR1=c:\proj\src\file.cpp
VAR2=TOOLS_PRJ
VAR3=tools/mytool/src/file.cpp
VAR4=3
```

この例では、VAR4 は、リビジョン番号です。 ただし、ほとんどのソースは、システムのサポート ファイルを特定のビルドのソースの状態を復元できるようにラベル付けを制御します。 そのため、ビルドのラベルを代わりに使用できます。 サンプル データのブロックは、次の変数を格納する変更でした。

```console
LABEL=BUILD47 
```

次を使用して、ソース管理システムを前提とします、アット マーク (@) でラベルを示すことが変数を変更する、SRCSRVCMD 次のようにします。

```console
sd.exe -p %fnvar%(%var2%) print -o %srcsrvtrg% -q %depot%/%var3%@%label%
```

### <a name="span-idhandlingservererrorsspanspan-idhandlingservererrorsspanhandling-server-errors"></a><span id="handling_server_errors"></span><span id="HANDLING_SERVER_ERRORS"></span>サーバー エラーの処理

場合があります、クライアントは、1 つのバージョン コントロール サーバーからすべてのファイルを抽出することができません。 これは、ため、サーバーがダウンし、ネットワーク、または、ユーザーがソースにアクセスする適切な特権を持っていないために指定できます。 ただし、このソースを取得しようとしています。 使用された時間できる速度の低下が大幅にします。 このような状況では、使用できないことが証明されているソースから抽出するあらゆる試みを無効にすることをお勧めします。

ファイルを抽出する SrcSrv が失敗したときに、コマンドによって生成された出力テキストを確認します。 このコマンドの任意の部分に、SRCSRVERRDESC の内容と完全に一致が含まれている場合は、以降のコマンドは、同じバージョンの管理サーバーはスキップされます。 SRCSRVERRDESC 変数名の末尾に数字または任意のテキストを追加することで、複数のエラー文字列を定義できることに注意してください。 以下に例を示します。

```console
SRCSRVERRDESC=lime: server not found
SRCSRVERRDESC_2=pineapple: network error
```

サーバーの id は SRCSRVERRVAR から取得されます。 したがって SRCSRVERRVAR には、"var2"と .pdb ファイルに、ファイルのエントリが含まれている場合は、ようになります。

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3
```

将来のすべてを含むファイルのエントリを使用してソースを取得しようとしました。"ツール\_PRJ"変数に 2 がバイパスされます。

編集することにより、デバッガーのクライアントでエラー インジケーターを追加することも[Srcsrv.ini](the-srcsrv-ini-file.md)します。 詳細については、srcsrv.ini の含まれているサンプル バージョンを参照してください。

 

 





