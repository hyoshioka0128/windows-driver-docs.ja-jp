---
title: CDB のコマンドライン オプション
description: デバッグを使用して CDB、NTSD セクションと、CDB、NTSD の初回使用時のユーザーが開始する必要があります。
ms.assetid: 34dbb695-19e4-4efc-83c7-3a94e5fcf269
keywords:
- CDB コマンド ライン オプションの Windows デバッグ
ms.date: 08/01/2018
topic_type:
- apiref
api_name:
- CDB Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 37d49d78e2f4f04175faa580f44a0439bfe984fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375576"
---
# <a name="cdb-command-line-options"></a>CDB のコマンドライン オプション


CDB、NTSD の初回使用時のユーザーは、まず、[デバッグを使用して CDB、NTSD](debugging-using-cdb-and-ntsd.md)セクション。

CDB コマンドラインは、次の構文を使用します。

```dbgcmd
cdb  [ -server ServerTransport | -remote ClientTransport ] 
[ -premote SmartClientTransport ] [-log{a|au|o|ou} LogFile]
[-2] [-d] [-ddefer] [-g] [-G] [-hd] [-lines] [-myob] [-bonc] 
[-n] [-o] [-s] [-v] [-w] [-cf "filename"] [-cfr "filename"] [-c "command"] 
[-robp] [-r BreakErrorLevel]  [-t PrintErrorLevel] 
[ -x{e|d|n|i} Exception ] [-x] [-clines lines] 
[-i ImagePath]  [-y SymbolPath] [-srcpath SourcePath] 
[-aExtension] [-failinc] [-noio] [-noinh] [-noshell] [-nosqm]
[-sdce] [-ses] [-sicv] [-sins] [-snc] [-snul] [-zp PageFile] 
[-sup] [-sflags 0xNumber] [-ee {masm|c++}]
[-e Event] [-pb] [-pd] [-pe] [-pr] [-pt Seconds] [-pv] 
[ -- | -p PID | -pn Name | -psn ServiceName | -z DumpFile | executable ] 
[-cimp] [-isd] [-kqm] [-pvr] [-version] [-vf] [-vf:<opts>] [-netsyms:{yes|no}]

cdb -iae 

cdb -iaec KeyString 

cdb -iu KeyString

cdb -QR Server 

cdb -wake pid 

cdb -?
```

NTSD コマンドライン構文は、CDB のと同じです。

```dbgcmd
ntsd  [ -server ServerTransport | -remote ClientTransport ] 
[ -premote SmartClientTransport ] [-log{a|au|o|ou} LogFile]
[-2] [-d] [-ddefer] [-g] [-G] [-hd] [-lines] [-myob] [-bonc] 
[-n] [-o] [-s] [-v] [-w] [-cf "filename"] [-cfr "filename"] [-c "command"] 
[-robp] [-r BreakErrorLevel]  [-t PrintErrorLevel] 
[ -x{e|d|n|i} Exception ] [-x] [-clines lines] 
[-i ImagePath]  [-y SymbolPath] [-srcpath SourcePath] 
[-aExtension] [-failinc] [-noio] [-noinh] [-noshell] [-nosqm]
[-sdce] [-ses] [-sicv] [-sins] [-snc] [-snul] [-zp PageFile] 
[-sup] [-sflags 0xNumber] [-ee {masm|c++}] 
[-e Event] [-pb] [-pd] [-pe] [-pr] [-pt Seconds] [-pv] 
[ -- | -p PID | -pn Name | -psn ServiceName | -z DumpFile | executable ] 
[-cimp] [-isd] [-kqm] [-pvr] [-version] [-vf] [-vf:<opts>] [-netsyms:{yes|no}]

ntsd -iae 

ntsd -iaec KeyString 

ntsd -iu KeyString

ntsd -QR Server 

ntsd -wake PID 

ntsd -?
```

NTSD と CDB の唯一の違いは、CDB が呼び出されたウィンドウを継承する NTSD が新しいコンソール ウィンドウを生成します。 以降、**開始**コマンドが、新しいコンソール ウィンドウを起動することもでき、次の 2 つの構造は同じ結果になります。

```dbgcmd
start cdb [parameters]
ntsd [parameters]
```

CDB、NTSD コマンド ライン オプションの説明に従ってください。 のみ、 **-リモート**、 **-サーバー**、 **-g**と **-g**オプション小文字が区別されます。 最初のハイフンは、フォワード スラッシュ (/) に置き換えることができます。 その他のパラメーターを取らないオプションを連結できます - ように**cdb-o-d-g-g winmine**として記述できます**cdb - odGg winmine**します。

場合、 **-リモート**または **-サーバー**オプションを使用すると、コマンドラインでその他のオプションの前にする必要があります。 場合、*実行可能ファイル*を指定すると、最後に、コマンドラインに表示する必要がありますの後の任意のテキスト、*実行可能ファイル*名前は、実行可能プログラムに独自のコマンド ライン パラメーターとして渡されます。

## <a name="span-idddkcdbcommandlineoptionsdbgspanspan-idddkcdbcommandlineoptionsdbgspanparameters"></a><span id="ddk_cdb_command_line_options_dbg"></span><span id="DDK_CDB_COMMAND_LINE_OPTIONS_DBG"></span>パラメーター


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span> **-server** *ServerTransport*   
その他のデバッガーによってアクセスできるデバッグ サーバーを作成します。 については、使用可能な*サーバトランスポート*値を参照してください[**デバッグ サーバー アクティブ化する**](activating-a-debugging-server.md)します。 このパラメーターを使用すると、コマンドラインで最初のパラメーターがあります。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span> **-remote** *ClientTransport*   
デバッグ クライアントを作成し、既に実行されているデバッグ サーバーに接続します。 については、使用可能な*ClientTransport*値を参照してください[**デバッグ クライアントをアクティブ化する**](activating-a-debugging-client.md)します。 このパラメーターを使用すると、コマンドラインで最初のパラメーターがあります。

<span id="_______-premote_______SmartClientTransport______"></span><span id="_______-premote_______smartclienttransport______"></span><span id="_______-PREMOTE_______SMARTCLIENTTRANSPORT______"></span> **-premote** *SmartClientTransport*   
スマート クライアントを作成しが既に実行されているプロセス サーバーに接続します。 については、使用可能な*SmartClientTransport*値を参照してください[**スマート クライアントのアクティブ化**](activating-a-smart-client.md)します。

<span id="_______-2______"></span> **-2**   
ターゲット アプリケーションがある場合、*コンソール アプリケーション*、このオプションは、新しいコンソール ウィンドウでライブにします。 (既定値は、CDB、NTSD と、ウィンドウを共有するターゲットのコンソール アプリケーションは) です。

<span id="_______--______"></span> **--**   
クライアント サーバー ランタイム サブシステム (CSRSS) は、デバッグします。 詳細については、次を参照してください。[デバッグ CSRSS](debugging-csrss.md)します。

<span id="_______-a_______Extension______"></span><span id="_______-a_______extension______"></span><span id="_______-A_______EXTENSION______"></span> **-** *拡張機能*   
既定の拡張 DLL を設定します。 既定値は*userexts*します。 後にスペースが必要ない、"a"、および、.dll 拡張子を含めることはできません。 詳細、およびこの既定の設定の他のメソッドでは、次を参照してください。[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)します。

<span id="_______-bonc______"></span><span id="_______-BONC______"></span> **-bonc**   
このオプションが指定されている場合は、セッションを開始するとすぐに、ターゲットに、デバッガーが中断されます。 これは、機能は、ターゲットが現在壊れていないデバッグ サーバーに接続するときに特に便利です。

<span id="_______-c_________command______________"></span><span id="_______-C_________COMMAND______________"></span> **-c "** *command* **"**   
起動時に実行する初期のデバッガー コマンドを指定します。 このコマンドは、引用符で囲む必要があります。 複数のコマンドは、セミコロンで区切ることができます。 (長いコマンド リストがあれば、スクリプト内に配置し、使用する方が簡単なる、 **-c**オプションは、 [  **$ &lt;、$&gt;&lt;、$&gt; &lt;、$$&gt; &lt; (スクリプト ファイルを実行)** ](-----------------------a---run-script-file-.md)コマンド)。

デバッグ クライアントを開始すると、このコマンドは必要があります、デバッグ サーバー向けです。 などの特定のクライアントのコマンド **.lsrcpath**は許可されていません。

<span id="_______-cf_________filename______________"></span><span id="_______-CF_________FILENAME______________"></span> **-cf "** *filename* **"**   
スクリプト ファイルの名前とパスを指定します。 このスクリプト ファイルは、デバッガーを起動するとすぐに実行されます。 場合*filename*引用符で囲む必要があるスペースが含まれています。 パスを省略した場合、現在のディレクトリが使用されます。 場合、 **cf**オプションが使用されない現在のディレクトリにファイル ntsd.ini がスクリプト ファイルとして使用されます場合、。 ファイルが存在しない場合は、エラーは発生しません。 詳細については、次を参照してください。[スクリプト ファイルを使用する](using-script-files.md)します。

<span id="_______-cfr_________filename______________"></span><span id="_______-CFR_________FILENAME______________"></span> **-cfr "** *filename* **"**   
スクリプト ファイルの名前とパスを指定します。 このスクリプト ファイルは、デバッガーが開始され、いつでも、ターゲットが再起動すると、すぐに実行されます。 場合*filename*引用符で囲む必要があるスペースが含まれています。 パスを省略した場合、現在のディレクトリが使用されます。 ファイルが存在しない場合は、エラーは発生しません。 詳細については、次を参照してください。[スクリプト ファイルを使用する](using-script-files.md)します。

<span id="_______-cimp______"></span><span id="_______-CIMP______"></span> **-cimp**   
CDB/NTSD、明示的なプロセスを実行するのではなく DbgSrv 暗黙的なコマンド ラインで開始するよう指示します。 このオプションは、クライアント側の dbgsrv pc です。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span> **-clines** *行*   
リモート デバッグ中にアクセスできるコマンドの履歴には、コマンドのおおよその数を設定します。 詳細については、およびこの数を変更するには、他の方法については、「[デバッガー コマンドを使用して](using-debugger-commands.md)します。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
カーネル デバッガーには、このデバッガーの制御を渡します。 常にこのコントロールのリダイレクトがアクティブである CSRSS をデバッグしている場合場合でも **-d**が指定されていません。 (このオプションにすることはできませんを使用して、リモート デバッグ--中に使用される **- ddefer**代わりにします)。参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)詳細についてはします。 このオプションは、いずれかと組み合わせて使用することはできません、 **- ddefer**オプションまたは **- noio**オプション。

**注**  WinDbg の使い慣れた機能の多くはこのシナリオでは利用できませんカーネル デバッガーとして WinDbg を使用する場合。 たとえば、ローカル ウィンドウ、逆アセンブル ウィンドウまたは呼び出し履歴 ウィンドウを使用することはできませんし、ソース コードをステップすることはできません。 これは、(NTSD または CDB)、デバッガーのビューアーとして WinDbg がのみ機能するため、ターゲット コンピューターで実行します。

 

<span id="_______-ddefer______"></span><span id="_______-DDEFER______"></span> **-ddefer**   
デバッグ クライアントが接続されている場合を除き、カーネル デバッガーにこのデバッガーの制御を渡します。 (これは、一種の **-d**デバッグ サーバーから使用できる)。参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)詳細についてはします。 このオプションは、いずれかと組み合わせて使用することはできません、 **-d**オプションまたは **- noio**オプション。

<span id="_______-e_______Event______"></span><span id="_______-e_______event______"></span><span id="_______-E_______EVENT______"></span> **-e** *イベント*   
指定したイベントが発生したことをデバッガーに通知します。 プログラムで、デバッガーを開始するときに、このオプションはのみ使用します。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span> **-ee** {**masm**|**c++**}  
既定の式エバリュエーターを設定します。 場合**masm**指定すると、MASM 式の構文が使用されます。 場合**c++** 指定すると、C++ 式の構文が使用されます。 場合、 **ee**オプションを省略すると、MASM 式の構文は、既定値として使用されます。 参照してください[を評価する式](evaluating-expressions.md)詳細についてはします。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span> **-failinc**   
原因の問題のあるシンボルを無視するデバッガー。 ユーザー モードまたはカーネル モードのミニダンプ ファイルをデバッグするには、このオプションは、デバッガーをイメージをマップすることはできませんのすべてのモジュールを読み込むようにも。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_EXACT\_シンボル](symbol-options.md#symopt-exact-symbols)します。

<span id="_______-g______"></span><span id="_______-G______"></span> **-g**   
ターゲット アプリケーションでは、最初のブレークポイントを無視します。 このオプションは、ターゲット アプリケーションが開始されているか、CDB が接続すると後の別のブレークポイントが設定されている場合を除き、実行を続行します。 参照してください[最初のブレークポイント](initial-breakpoint.md)詳細についてはします。

<span id="_______-G______"></span><span id="_______-g______"></span> **-G**   
プロセスの終了時の最終的なブレークポイントを無視します。 既定では、イメージ run-down プロセス中に CDB が停止します。 このオプションは、子プロセスの終了時にすぐに CDB が発生します。 これは、コマンドを入力すると同じ効果**sxd epr**します。 詳細については、次を参照してください。[を制御する例外とイベント](controlling-exceptions-and-events.md)します。

<span id="_______-hd______"></span><span id="_______-HD______"></span> **-hd**   
 デバッグ ヒープを使用しないことを指定します。 参照してください[デバッグ ユーザー モード プロセスを使用して CDB](debugging-a-user-mode-process-using-cdb.md)詳細についてはします。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span> **-i** *ImagePath*   
違反を生成した実行可能ファイルの場所を指定します。 パスにスペースが含まれている場合は、引用符で囲む必要があります。

<span id="_______-iae______"></span><span id="_______-IAE______"></span> **-iae**   
事後分析のデバッガーと CDB をインストールします。 詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。

この操作が成功すると、メッセージは表示されません。失敗した場合、エラー メッセージが表示されます。

**- Iae**パラメーターは、その他のパラメーターを使用する必要があります。 このコマンド CDB は実際に開始されません。

<span id="_______-iaec_______KeyString______"></span><span id="_______-iaec_______keystring______"></span><span id="_______-IAEC_______KEYSTRING______"></span> **-iaec** *KeyString*   
事後分析のデバッガーと CDB をインストールします。 内容*KeyString*の末尾に追加されますが、 **AeDebug**レジストリ キー。 場合*KeyString*スペースが含まれることは、引用符で囲む必要があります。 詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。

この操作が成功すると、メッセージは表示されません。失敗した場合、エラー メッセージが表示されます。

**- Iaec**パラメーターは、その他のパラメーターを使用する必要があります。 このコマンド CDB は実際に開始されません。

<span id="_______-isd______"></span><span id="_______-ISD______"></span> **-isd**   
作成をオンに\_無視\_システム\_いずれかの既定のフラグの作成を処理します。

<span id="_______-iu________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span> **-iu** *KeyString*   
ユーザーは自動起動 url のデバッガーのリモート クライアントするためには、デバッガーのリモート処理、URL の種類として登録します。 *KeyString*形式`remdbgeng://RemotingOption`します。 *RemotingOption*トピックで定義されているトランスポート プロトコルを定義する文字列は、 [**デバッグ クライアントをアクティブ化する**](activating-a-debugging-client.md)します。 この操作が成功すると、メッセージは表示されません。失敗した場合、エラー メッセージが表示されます。

**-Iu**パラメーターは、その他のパラメーターを使用する必要があります。 このコマンド CDB は実際に開始されません。

<span id="_______-kqm______"></span><span id="_______-KQM______"></span> **-kqm**   
Quiet モードで CDB/NTSD を起動します。

<span id="_______-lines______"></span><span id="_______-LINES______"></span> **-lines**   
ソース行のデバッグを有効にします。 このオプションを省略した場合、 [ **.lines (切り替えのソース行のサポート)** ](-lines--toggle-source-line-support-.md)コマンドがソースのデバッグが許可される前に使用する必要があります。 これを制御するための他の方法では、次を参照してください。 [SYMOPT\_ロード\_行](symbol-options.md#symopt-load-lines)します。

<span id="_______-log_a_au_o_ou__LogFile"></span><span id="_______-log_a_au_o_ou__logfile"></span><span id="_______-LOG_A_AU_O_OU__LOGFILE"></span> **-log**{**a|au|o|ou**} *LogFile*  
ログ ファイルにログ情報を開始します。 指定したファイルが既に存在する場合は上書きされる場合 **-ロゴ**を使用または - loga を使用する場合にその出力がファイルに追加されます。 **- Logau**と **- logou**オプション操作のような **- loga**と **-ロゴ**それぞれを除き、ログ ファイルが Unicode ファイルであります。 詳細については、次を参照してください。 [CDB にログ ファイルを保持](keeping-a-log-file-in-cdb.md)します。

<span id="_______-myob______"></span><span id="_______-MYOB______"></span> **-myob**   
Dbghelp.dll をバージョンの不一致がある場合、デバッガーは実行し続けます。 (なし、 **- myob**スイッチと見なされます、致命的なエラー)。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
*ノイズの多いシンボルの読み込み*:シンボル ハンドラーから詳細な出力を有効にします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_デバッグ](symbol-options.md#symopt-debug)します。

<span id="_______-netsyms__yes_no_______"></span><span id="_______-NETSYMS__YES_NO_______"></span> **-netsyms {[はい] | ありません}**   
許可またはネットワーク パスからシンボルを読み込みを禁止します。

<span id="_______-noinh______"></span><span id="_______-NOINH______"></span> **-noinh**   
デバッガーからハンドルを継承することから、デバッガーによって作成されたプロセスをできないようにします。 これを制御するための他の方法では、次を参照してください。[デバッグ ユーザー モード プロセスを使用して CDB](debugging-a-user-mode-process-using-cdb.md)します。

<span id="_______-noio______"></span><span id="_______-NOIO______"></span> **-noio**   
デバッグ サーバーが使用されている入力または出力するを防ぎます。 入力は、デバッグのクライアントからのみ受け付けられます (さらに任意の最初のコマンドやコマンドのスクリプトで指定された、 **-c**コマンド ライン オプション)。

すべての出力は、デバッグのクライアントに転送されます。 サーバーの NTSD を使用する場合コンソール ウィンドウは作成されませんまったくです。 詳細については、次を参照してください。 [**デバッグ サーバー アクティブ化する**](activating-a-debugging-server.md)します。 このオプションは、いずれかと組み合わせて使用することはできません、 **-d**オプションまたは **- ddefer**オプション。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span> **-noshell**   
すべてを禁止 **.shell**コマンド。 この禁止は、新しいデバッグ セッションが開始された場合でも、デバッガーが実行されている限り最後されます。 無効にするには、他の方法に関する詳細、および **.shell**コマンドを参照してください[シェル コマンドを使用して](using-shell-commands.md)します。

<span id="_______-nosqm______"></span><span id="_______-NOSQM______"></span> **-nosqm**   
テレメトリ データの収集とアップロードを無効にします。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
ターゲット アプリケーション (子プロセス) で起動されたすべてのプロセスをデバッグします。 既定では、作成したプロセスをデバッグする 1 つでは、通常どおり、実行されます。 これを制御するための他の方法では、次を参照してください。[デバッグ ユーザー モード プロセスを使用して CDB](debugging-a-user-mode-process-using-cdb.md)します。

<span id="_______-p_______PID______"></span><span id="_______-p_______pid______"></span><span id="_______-P_______PID______"></span> **-p** *PID*   
デバッグする 10 進数のプロセス ID を指定します。 これは、既に実行されているプロセスのデバッグに使用されます。 詳細については、次を参照してください。[デバッグ ユーザー モード プロセスを使用して CDB](debugging-a-user-mode-process-using-cdb.md)します。

<span id="_______-pb______"></span><span id="_______-PB______"></span> **-pb**   
デバッガーがターゲット プロセスにアタッチするときに、初期の侵入を要求するを防ぎます。 アプリケーションが既に中断されている場合、またはターゲットで侵入スレッドを作成しないようにする場合は便利にできます。

<span id="_______-pd______"></span><span id="_______-PD______"></span> **-pd**   
により、ターゲット アプリケーションは、デバッグ セッションの終了時に終了するのにはしません。 参照してください[CDB でデバッグ セッションを終了する](ending-a-debugging-session-in-cdb.md)詳細についてはします。

<span id="_______-pe______"></span><span id="_______-PE______"></span> **-pe**   
対象アプリケーションは既にデバッグされていることを示します。 参照してください[対象アプリケーションを再アタッチ](reattaching-to-the-target-application.md)詳細についてはします。

<span id="_______-pn_______Name______"></span><span id="_______-pn_______name______"></span><span id="_______-PN_______NAME______"></span> **-pn** *名*   
デバッグするプロセスの名前を指定します。 (この名前必要がありますで一意である。)これは、既に実行されているプロセスのデバッグに使用されます。

<span id="_______-pr______"></span><span id="_______-PR______"></span> **-pr**   
原因、デバッガーをアタッチするときに実行されているターゲット プロセスを開始します。 これは、アプリケーションが既に中断されているし、実行を再開することを希望する場合に役立ちます。

<span id="_______-psn_______ServiceName______"></span><span id="_______-psn_______servicename______"></span><span id="_______-PSN_______SERVICENAME______"></span> **-psn** *ServiceName*   
デバッグするプロセスに含まれているサービスの名前を指定します。 これは、既に実行されているプロセスのデバッグに使用されます。

<span id="_______-pt_______Seconds______"></span><span id="_______-pt_______seconds______"></span><span id="_______-PT_______SECONDS______"></span> **pt -** *秒*   
区切りのタイムアウトを秒単位で指定します。 既定値は 30 です。 参照してください[ターゲットを制御する](controlling-the-target.md)詳細についてはします。

<span id="_______-pv______"></span><span id="_______-PV______"></span> **-pv**   
デバッガーがターゲット プロセスに noninvasively アタッチする必要がありますを指定します。 詳細については、次を参照してください。[待合室 (ユーザー モード) のデバッグ](noninvasive-debugging--user-mode-.md)します。

<span id="_______-pvr______"></span><span id="_______-PVR______"></span> **-pvr**   
同様に動作 **-pv**ターゲット プロセスが中断されていない点が異なります。

<span id="_______-QR_______Server______"></span><span id="_______-qr_______server______"></span><span id="_______-QR_______SERVER______"></span> **-QR** *サーバー*   
指定したネットワーク サーバーで実行されているすべてのデバッグ サーバーの一覧を表示します。 二重の円記号 (\\ \)前*Server*は省略可能です。 参照してください[**デバッグ サーバーの検索**](searching-for-debugging-servers.md)詳細についてはします。

**-QR**パラメーターは、その他のパラメーターでは使用できません。 このコマンド CDB は実際に開始されません。

<span id="_______-r________BreakErrorLevel______"></span><span id="_______-r________breakerrorlevel______"></span><span id="_______-R________BREAKERRORLEVEL______"></span> **-r** *BreakErrorLevel*   
デバッガーを中断するようにターゲットすると、エラー レベルを指定します。 これは、0、1、2、または 3 と等しい 10 進数です。 使用できる値は次のとおりです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">定数</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>すべてのエラーで中断しない操作を行います。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>エラー</p></td>
<td align="left"><p>エラー レベルのイベントのデバッグで中断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>デバッグ イベント MINORERROR とエラーのレベルで中断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>デバッグ イベント、警告、MINORERROR、およびエラーのレベルで中断します。</p></td>
</tr>
</tbody>
</table>

 

このエラーのレベルは、Microsoft Windows のチェック ビルドにだけ意味を持ちます。 既定値は 1 です。

<span id="_______-robp______"></span><span id="_______-ROBP______"></span> **-robp**   
これにより、CDB を読み取り専用メモリ ページにブレークポイントを設定できます。 (既定値は、このような操作が失敗するは) です。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
シンボルの遅延読み込みを無効にします。 これにより、プロセスの起動速度が低下します。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_遅延\_読み込み](symbol-options.md#symopt-deferred-loads)します。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span> **-sdce**   
デバッガー表示が**ファイル アクセス エラー**シンボルの読み込み中にダイアログ ボックス。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_失敗\_重大\_エラー](symbol-options.md#symopt-fail-critical-errors)します。

<span id="_______-ses______"></span><span id="_______-SES______"></span> **-ses**   
原因のデバッガーがすべてのシンボル ファイルの厳密な評価を実行し、問題のある任意の記号を無視します。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_EXACT\_シンボル](symbol-options.md#symopt-exact-symbols)します。

<span id="_______-sflags_0x_______Number______"></span><span id="_______-sflags_0x_______number______"></span><span id="_______-SFLAGS_0X_______NUMBER______"></span> **sflags 0 x** *数*   
一度にすべてのシンボルのハンドラーのオプションを設定します。 *数*付ける必要があります、16 進数**0 x** --、なし 10 進数、 **0 x**は許可されてが、シンボルのオプションはバイナリのフラグ、したがって、16 進数はお勧めします。 このオプションは、すべてのシンボルのハンドラーの既定値は上書きされますので注意して使用する必要があります。 詳細については、次を参照してください。[シンボル オプションを設定](symbol-options.md)します。

<span id="_______-sicv______"></span><span id="_______-SICV______"></span> **-sicv**   
CV レコードを無視するシンボルのハンドラーをによりします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_無視\_CVREC](symbol-options.md#symopt-ignore-cvrec)します。

<span id="_______-sins______"></span><span id="_______-SINS______"></span> **-sins**   
原因のデバッガーがシンボル パスと実行可能ファイル イメージのパス環境変数を無視します。 詳細については、次を参照してください。 [SYMOPT\_無視\_NT\_SYMPATH](symbol-options.md#symopt-ignore-nt-sympath)します。

<span id="_______-snc______"></span><span id="_______-SNC______"></span> **-snc**   
原因のデバッガーが C++ の変換をオフにします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_いいえ\_CPP](symbol-options.md#symopt-no-cpp)します。

<span id="_______-snul______"></span><span id="_______-SNUL______"></span> **-snul**   
非修飾名のシンボルの自動読み込みを無効にします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_いいえ\_UNQUALIFIED\_読み込み](symbol-options.md#symopt-no-unqualified-loads)します。

<span id="_______-srcpath_______SourcePath______"></span><span id="_______-srcpath_______sourcepath______"></span><span id="_______-SRCPATH_______SOURCEPATH______"></span> **-srcpath** *SourcePath*   
ソース ファイルの検索パスを指定します。 複数のパスをセミコロン (;) で区切ります。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細については、およびこのパスを変更するには、他の方法については、「[ソース パス](source-path.md)します。

<span id="_______-sup______"></span><span id="_______-SUP______"></span> **-sup**   
すべてのシンボルの検索中に、パブリック シンボル テーブルを検索するシンボルのハンドラーをによりします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_自動\_PUBLICS](symbol-options.md#symopt-auto-publics)します。

<span id="_______-t________PrintErrorLevel______"></span><span id="_______-t________printerrorlevel______"></span><span id="_______-T________PRINTERRORLEVEL______"></span> **-t** *PrintErrorLevel*   
デバッガーはエラー メッセージを表示すると、エラー レベルを指定します。 これは、0、1、2、または 3 と等しい 10 進数です。 使用できる値は次のとおりです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">定数</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>すべてのエラーは表示されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>エラー</p></td>
<td align="left"><p>エラー レベルのデバッグ イベントを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>デバッグ イベント MINORERROR とエラーのレベルを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>デバッグ イベント、警告、MINORERROR、およびエラーのレベルを表示します。</p></td>
</tr>
</tbody>
</table>

 

このエラーのレベルは、Microsoft Windows のチェック ビルドにだけ意味を持ちます。 既定値は 1 です。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
デバッガーから詳細な出力を有効にします。

<span id="_______-version______"></span><span id="_______-VERSION______"></span> **-version**   
デバッガーのバージョン文字列を出力します。

<span id="_______-vf______"></span><span id="_______-VF______"></span> **-vf**   
既定の ApplicationVerifier 設定を有効にします。

<span id="_______-vf________opts_"></span><span id="_______-VF________OPTS_"></span> **vf:**  *&lt;opts&gt;*  
ApplicationVerifier 設定を有効にします。

<span id="_______-w______"></span><span id="_______-W______"></span> **-w**   
別々 の VDM で 16 ビット アプリケーションをデバッグすることを指定します。

<span id="_______-wake_______PID______"></span><span id="_______-wake_______pid______"></span><span id="_______-WAKE_______PID______"></span> **-wake** *PID*   
原因はスリープ モードでプロセス ID が指定されたユーザー モード デバッガーの終了を*PID*します。 このコマンドは、ターゲット コンピューターのスリープ モード中に発行する必要があります。 参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)詳細についてはします。

**-Wake**パラメーターは、その他のパラメーターと共に使用しない必要があります。 このコマンド CDB は実際に開始されません。

<span id="_______-x_e_d_n_i__Exception"></span><span id="_______-x_e_d_n_i__exception"></span><span id="_______-X_E_D_N_I__EXCEPTION"></span> **-x**{**e**|**d**|**n**|**は**}*例外*  
指定したイベントが発生した場合は、デバッガーの動作を制御します。 *例外*例外の数またはイベント コードを使用できます。 コントロールのさまざまなイベントを複数回には、このオプションを指定することができます。 参照してください[を制御する例外とイベント](controlling-exceptions-and-events.md)とこれらの設定を制御するその他の方法の詳細についてはします。

<span id="_______-x______"></span><span id="_______-X______"></span> **-x**   
アクセス違反例外に初回の break を無効にします。 2 番目に出現するアクセス違反がデバッガーに中断されます。 これは、同じ **-xd av**します。

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span> **-y** *SymbolPath*   
シンボルの検索パスを指定します。 複数のパスをセミコロン (;) で区切ります。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細については、およびこのパスを変更するには、他の方法については、「[シンボル パス](symbol-path.md)します。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span> **-z** *DumpFile*   
デバッグするクラッシュ ダンプ ファイルの名前を指定します。 パスとファイル名にスペースが含まれている場合、これを引用符で囲む必要があります。 複数を含めることによって、いくつかのダンプ ファイルを一度に開くことは **-z**オプション、各の後に、異なる*DumpFile*値。 詳細については、次を参照してください。[ユーザー モード ダンプ ファイルの分析](analyzing-a-user-mode-dump-file.md)します。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span> **-zp** *PageFile*   
変更されたページのファイルの名前を指定します。 デバッグ ダンプ ファイルを使用する場合に便利ですが、 [ **.pagein (メモリ内のページ)** ](-pagein--page-in-memory-.md)コマンド。 使用することはできません **-zp**標準 Windows ページファイル--ページ ファイルを特別に変更のみを使用できます。

<span id="_______executable______"></span><span id="_______EXECUTABLE______"></span> *実行可能ファイル*   
実行可能ファイルのプロセスのコマンドラインを指定します。 これは、新しいプロセスを起動し、デバッグに使用されます。 コマンドラインで最後の項目をする必要があります。 実行可能ファイル名が渡された後引数の文字列として実行可能ファイルへのすべてのテキスト。

<span id="_______-_______"></span> **-?**   
ヘルプをコマンド ラインを表示します。

デバッガーを起動するときに**開始 |実行**またはコマンド プロンプト ウィンドウで、アプリケーションのファイル名の後にターゲット アプリケーションの引数を指定します。 例:

```dbgcmd
cdb myexe arg1arg2
```

 

 





