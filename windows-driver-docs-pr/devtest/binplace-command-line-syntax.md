---
title: BinPlace のコマンド ライン構文
description: BinPlace は、コマンドラインで、次の構文を使用します。
ms.assetid: 8489b7ae-3e3b-41d5-b9a6-0b69aa92087e
keywords:
- BinPlace コマンドライン構文のドライバーの開発ツール
topic_type:
- apiref
api_name:
- BinPlace Command-Line Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7bce3f1a3ea7ea83b688779742bc478ad29e80
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360424"
---
# <a name="binplace-command-line-syntax"></a>BinPlace のコマンド ライン構文


BinPlace は、コマンドラインで、次の構文を使用します。

```
    binplace [Options] File [ [Options] [@PlaceFile] File [...] ]
```

## <a name="span-idddkbinplacecommandlinesyntaxtoolsspanspan-idddkbinplacecommandlinesyntaxtoolsspanparameters"></a><span id="ddk_binplace_command_line_syntax_tools"></span><span id="DDK_BINPLACE_COMMAND_LINE_SYNTAX_TOOLS"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
これは、次のスイッチのいずれかを含めることができます。 スイッチは、ハイフン (-) またはスラッシュ (/) によって先行されなければなりません。 1 つのスラッシュ、またはハイフンの後にいくつかのオプションを結合することですが、追加のパラメーターを受け取るオプションをスペースで従う必要があります。 したがって、次の 2 つのコマンドは同等です。

```
binplace -q -k -g LCFile -v -s SymbolRoot File 
binplace -qkg LCFile -vs SymbolRoot File 
```

次のスイッチを使用できます。

<span id="-a"></span><span id="-A"></span> **-**  
配置されているときに、シンボル ファイルからプライベート シンボルを取り除く BinPlace をによりします。 これには、パブリック シンボルですがないプライベート シンボルを含めることが削除されたシンボル ファイルが作成されます。 使用する場合、 **-** スイッチを使用する必要がある **-s**と **-x**もします。 ときに **-** を使うと、によって指定されたパスでファイルを配置するシンボルの除去 **s * * * SymbolRoot*します。 場合 * *-n * * * FullSymbolRoot*があることも、ファイルを配置する完全なシンボル*FullSymbolRoot*します。 それ以外の場合、それらはかけ任意の場所。

<span id="-b_ExtraSubdirectory"></span><span id="-b_extrasubdirectory"></span><span id="-B_EXTRASUBDIRECTORY"></span> **-b** *ExtraSubdirectory*  
通常よりも別の場所にファイルを配置する BinPlace をによりします。 BinPlace 通常どおり、ルート インストール先ディレクトリ、クラスのサブディレクトリおよびファイルの種類のサブディレクトリを連結する場合は後に、この変更は追加し、 *ExtraSubdirectory*最終的な宛先ディレクトリを作成するには、このパスにします。 *ExtraSubdirectory*で始まるも円記号で終了する必要があります。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)の詳細。

<span id="-e"></span><span id="-E"></span> **-e**  
実行を続行する場合は、ファイルを配置することはできません BinPlace をによりします。 既定では、このエラーが発生したときに BinPlace は終了します。

<span id="-f"></span><span id="-F"></span> **-f**  
新しいファイルを上書きする場合でも、ファイルを配置する BinPlace を強制します。 既定では、BinPlace が、ファイルを配置しようとした場合、以前のバージョンが上書きされますより新しいバージョンは上書きされません。

<span id="-g_LCFile"></span><span id="-g_lcfile"></span><span id="-G_LCFILE"></span> **-g** *LCFile*  
実行可能ファイルを確認する BinPlace をによりします。 *LCFile*この検証に使用するローカリゼーション制約ファイルを指定します。

<span id="-h"></span><span id="-H"></span> **-h**  
ファイルを配置するときに、ファイルをコピーする代わりにハード リンクを作成する BinPlace をによりします。 このオプションは、NTFS ファイル システムで使用できるだけです。

<span id="-j"></span><span id="-J"></span> **-j**  
実行可能ファイルをコピーする前に適切なシンボルがあることを確認する BinPlace をによりします。 このオプションを使用するには、SymChk ツールは、パスにする必要があります。 (SymChk は Windows のツールをデバッグ パッケージの一部です。 参照してください[Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)詳細についてはします)。

<span id="-k"></span><span id="-K"></span> **-k**  
ファイル属性を維持する BinPlace をによりします。 既定では、BinPlace はアーカイブ属性をオフにします。

<span id="-n_FullSymbolRoot"></span><span id="-n_fullsymbolroot"></span><span id="-N_FULLSYMBOLROOT"></span> **-n** *FullSymbolRoot*  
完全なシンボル ファイル (パブリックとプライベート両方のシンボルが含まれているシンボル ファイル) のルート ディレクトリを指定します。 これが必要です、 **-a**、 **-x**、および **-s**スイッチもします。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)の詳細。

<span id="-o_RootSubdirectory"></span><span id="-o_rootsubdirectory"></span><span id="-O_ROOTSUBDIRECTORY"></span> **-o** *RootSubdirectory*  
使用するルート インストール先ディレクトリのサブディレクトリを指定します。 インストール先ディレクトリが作成されると、 *RootSubdirectory*ルート インストール先のディレクトリとクラスのサブディレクトリの間に挿入されます。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)の詳細。

<span id="-p_PlaceFile"></span><span id="-p_placefile"></span><span id="-P_PLACEFILE"></span> **-p** *PlaceFile*  
配置ファイルのパスとファイル名を指定します。 場合、 **-p**スイッチを使用しない、BinPlace という名前の場所を使用して *\\ツール\\placefil.txt*します。 参照してください[**配置ファイルの構文**](place-file-syntax.md)配置ファイルの内容の詳細についてはします。

**注**、 **-p**切り替えてファイルは廃止されましたとは使用できません。



<span id="-q"></span><span id="-Q"></span> **-q**  
BinPlace がログ ファイルを使用するを防ぎます。 場合、 **-q**スイッチを省略すると、指定されたファイルは、BINPLACE によって\_ログ環境変数は、ログ ファイルとして使用されます。

<span id="-r_RootDestinationPath"></span><span id="-r_rootdestinationpath"></span><span id="-R_ROOTDESTINATIONPATH"></span> **-r** *RootDestinationPath*  
ルートのインストール先ディレクトリを指定します。 これを省略すると、既定値が定め、 \_NT386TREE、 \_NTIA64TREE、または\_x86、Itanium ベースまたは x64 ベース コンピューターは、環境変数を NTAMD64TREE それぞれします。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)詳細についてはします。

<span id="-s_SymbolRoot"></span><span id="-s_symbolroot"></span><span id="-S_SYMBOLROOT"></span> **-s** *SymbolRoot*  
シンボル ファイルのルート ディレクトリを指定します。 場合、 **-a**と **-x**スイッチを使用することも、プライベート シンボルをシンボルのファイルから除去され、削除されたシンボル ファイルで指定されたディレクトリに配置されます*SymbolRoot*. 両方の削除と完全なシンボル ファイルを配置する場合は、使用してください--x の SymbolRoot-n FullSymbolRoot します。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)の詳細。

<span id="-t"></span><span id="-T"></span> **-t**  
*テスト モード*します。 このスイッチを使用する場合、ファイルはコピーされませんが、BinPlace ファイルを配置した場合、警告およびエラー メッセージが表示されます。 使用することがあります、 **-v**メッセージの数を増やすにスイッチします。

<span id="-u"></span><span id="-U"></span> **-u**  
BinPlace を追加すると、\\クラス サブディレクトリまでです。 これは、ユニプロセッサ (UP) ドライバーを分離する場合に便利です。 さらに、このスイッチを使用すると、常に BinPlace がシンボルを含む実行可能ファイルは分割されません。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)の詳細。

<span id="-v"></span><span id="-V"></span> **-v**  
*詳細モード*します。 詳細なエラー、警告、および進行状況メッセージを表示する BinPlace をによりします。

<span id="-w"></span><span id="-W"></span> **-w**  
シンボルのツリーに Windows 95 のシンボル ファイル (.sym) を追加する BinPlace をによりします。

<span id="-x"></span><span id="-X"></span> **-x**  
BinPlace を使用するファイルを検出すると、*古いシンボル システム*、このスイッチでは、実行可能ファイルからすべてのシンボルを削除し、シンボル ファイルを個別にこの情報を移動します。 参照してください[シンボル ファイル システム](symbol-file-systems.md)詳細についてはします。 使用する場合、 **-x**スイッチを使用する必要がある **-s**と **-** もします。

<span id="-y"></span><span id="-Y"></span> **-y**  
BinPlace がクラスのすべてのサブディレクトリを使用するを防ぎます。 インストール先ディレクトリがルート インストール先のディレクトリとファイルの種類のサブディレクトリからのみ作成されます。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)詳細についてはします。

<span id="-z"></span><span id="-Z"></span> **~ z**  
キャンセル、 **-x**スイッチします。 いくつかのターゲットを BinPlace を使用しているフォームのコマンドを使用する場合に便利ですこのできる**binplace** *argumentsTarget1argumentsTarget2*、コマンド ラインが左から右に解析されるため、*Target1*と*Target2*異なる引数の影響を受けます。 (解析の順序のセクションで次を参照してください。) 場合、 **-z**スイッチが発生した、以前のどの効果がキャンセル **-x**スイッチします。

<span id="-ci_ReturnCode_Application_Argument_Argument__..._"></span><span id="-ci_returncode_application_argument_argument__..._"></span><span id="-CI_RETURNCODE_APPLICATION_ARGUMENT_ARGUMENT__..._"></span> **-ci** <em>ReturnCode</em> **、** <em>アプリケーション</em> **、** <em>引数</em> **、** <em>引数</em> **、** .   
カスタム アプリケーションを使用して、すべての実行可能ファイルを検証する BinPlace をによりします。 使用することができます、 **- ci** BinPlace を他のアプリケーションを使用して、その検証を実行する場合に切り替えます。

*ReturnCode*実行可能ファイルで、エラーが見つかった場合に、このアプリケーションが返される値である必要があります。 その他のパラメーターは、このアプリケーションの起動に使用されます。 これらすべて区切りますコンマで区切ります。 *アプリケーション*プログラムの名前を指定します。 これは、コマンドライン引数の任意の数で実行できます。 含まれるコマンドラインを使用した、プログラムが開始される*アプリケーション*(コンマではなく、スペースで区切られた) 場合、すべての引数が続くと確認する実行可能ファイルの名前の最後に終了します。

<span id="-_ARC"></span><span id="-_arc"></span> **-: 円弧**  
BinPlace のみアーカイブ属性を持つ設定ファイルを配置するとします。

<span id="-_DBG"></span><span id="-_dbg"></span> **-: DBG**  
BinPlace が .dbg ファイルを配置するを防ぎます。 場合、 **-j**スイッチを使用しても、これにより、BinPlace .dbg ファイルをポイントするバイナリを配置するからです。 このオプションを使用するには、SymChk ツールは、パスにする必要があります。 (SymChk は Windows のツールをデバッグ パッケージの一部です。 参照してください[Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)詳細についてはします)。

<span id="-_DEST_ClassPath"></span><span id="-_dest_classpath"></span><span id="-_DEST_CLASSPATH"></span> **-: DEST** *クラスパス*  
BinPlace 配置ファイルを無視し、指定したを使用すると、*クラスパス*クラス サブディレクトリとして。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)詳細についてはします。

<span id="-_LOGPDB"></span><span id="-_logpdb"></span> **-: LOGPDB**  
ログ ファイルに .pdb の完全なパスを含める BinPlace をによりします。

<span id="-_REN_NewName"></span><span id="-_ren_newname"></span><span id="-_REN_NEWNAME"></span> **-:REN** *NewName*  
配置されているファイルの名前を変更する BinPlace をによりします。 拡張子を含む元のファイル名に置き換えられます*NewName*します。 (元のファイルが分割されていること、実行可能ファイルの場合は、新しいシンボル ファイルが与えられますは元のファイル名と拡張子 .dbg。)

<span id="-_TMF"></span><span id="-_tmf"></span> **-:TMF**  
BinPlace を作成すると、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)トレース メッセージを抽出することで、PDB シンボル ファイルの指示を書式設定します。 TMF ファイルは BinPlace トレースで指定されたディレクトリに配置する\_形式\_PATH 環境変数。 参照してください[BinPlace マクロと環境変数](binplace-macros-and-environment-variables.md)します。

<span id="-ChangeAsmsToRetailForSymbols"></span><span id="-changeasmstoretailforsymbols"></span><span id="-CHANGEASMSTORETAILFORSYMBOLS"></span> **-ChangeAsmsToRetailForSymbols**  
文字列を置換 BinPlace"asm"文字列"retail"シンボル ファイルの保存先ディレクトリ内に発生する場合。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)の詳細。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span> *ファイル*   
BinPlace の対象となるファイルの完全なパスとファイル名を指定します。 任意の数のスペースで区切られたファイルを一覧表示できます。 パスとファイル名にスペースが含まれている場合、パスとファイル名を引用符で囲む必要があります。

<span id="________PlaceFile______"></span><span id="________placefile______"></span><span id="________PLACEFILE______"></span> **@** <em>PlaceFile</em>   
任意のファイル名が続く場合、アット マーク ( **@** )、ファイル名は、配置ファイルの名前を表します。 詳細については、ファイルのセクションで次に指定するパラメーターを参照してください。

### <a name="span-idparsingorderspanspan-idparsingorderspanparsing-order"></a><span id="parsing_order"></span><span id="PARSING_ORDER"></span>解析の順序

BinPlace は左から右へのコマンド ラインを解析します。 いくつかのオプションを指定することができます、*ファイル*パラメーター、新しいオプションは、別*ファイル*パラメーターなどです。 BinPlace の新しいオプションを検出するたびに、採用、以前に発生、矛盾するオプションをオーバーライドします。 発生したときに、*ファイル*指定子が既に発生までの累積オプションを使用して、コマンドラインでそのファイルで機能します。

### <a name="span-idsupplyingparametersinafilespanspan-idsupplyingparametersinafilespansupplying-parameters-in-a-file"></a><span id="supplying_parameters_in_a_file"></span><span id="SUPPLYING_PARAMETERS_IN_A_FILE"></span>ファイル内のパラメーターを指定します。

テキスト ファイルから BinPlace にパラメーターを渡すことになります。 これには 2 つの方法があります。

-   ファイル名を指定するには、BINPLACE で\_オーバーライド\_環境変数のフラグ。 このファイルは、読み取りとその内容を BinPlace が実行されるたびに、パラメーターとして使用されます。 このファイル内のパラメーターは、実際に BinPlace コマンドラインに表示されるパラメーターの前に解析されます。

-   付ける BinPlace コマンドラインでファイル名を指定することができます、アット マーク ( **@** )。 文字列、削除、BinPlace は、コマンドラインで、この記号で始まる文字列を見ては、記号を参照し、この名前のファイルにします。 このファイルを検出した場合は、まったくの場所でコマンドラインにそのテキストが挿入されます、元のパラメーターの先頭に、アット マークされていた。 BinPlace が左から右へのパラメーターを解析するための複数のインスタンスと共にこの手法を使用することができます*ファイル*BinPlace ごとにさまざまなオプションを複数のファイルを使用するすべてのオプションを入力しなくても毎回です。 (BinPlace が元の文字列を扱うこのファイルが見つからない場合など、アット マークは、として、*ファイル*パラメーターです)。









