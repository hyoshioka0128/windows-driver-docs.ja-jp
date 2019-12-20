---
title: CDB のコマンドライン オプション
description: CDB または NTSD の初めてのユーザーは、「CDB と NTSD を使用したデバッグ」セクションから始める必要があります。
ms.assetid: 34dbb695-19e4-4efc-83c7-3a94e5fcf269
keywords:
- CDB のコマンドラインオプション Windows のデバッグ
ms.date: 08/01/2018
topic_type:
- apiref
api_name:
- CDB Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5bd69b938be93ed1a876915e945495cd6dc34a92
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209400"
---
# <a name="cdb-command-line-options"></a>CDB のコマンドライン オプション


CDB または NTSD の初めてのユーザーは、「 [cdb と Ntsd を使用したデバッグ](debugging-using-cdb-and-ntsd.md)」セクションから始める必要があります。

CDB コマンドラインでは、次の構文を使用します。

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

NTSD のコマンドライン構文は、CDB と同じです。

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

NTSD と CDB の唯一の違いは、NTSD によって新しいコンソールウィンドウが生成され、CDB が呼び出されたウィンドウを継承するという点です。 **Start**コマンドを使用して新しいコンソールウィンドウを生成することもできるため、次の2つの構造で同じ結果が得られます。

```dbgcmd
start cdb [parameters]
ntsd [parameters]
```

CDB および NTSD のコマンドラインオプションの説明は次のようになります。 **-Remote**、 **-server**、 **-g** 、および **-g**オプションだけで、大文字と小文字が区別されます。 先頭のハイフンは、スラッシュ (/) に置き換えることができます。 追加のパラメーターを使用しないオプションは連結できます。そのため、 **odGg winmine**として作成できるのは**cdb**です。

**-Remote**または **-server**オプションを使用する場合は、コマンドラインの他のオプションの前に指定する必要があります。 *実行可能ファイル*が指定されている場合は、コマンドラインで最後に指定する必要があります。*実行可能*ファイル名の後のテキストは、独自のコマンドラインパラメーターとして実行可能プログラムに渡されます。

## <a name="span-idddk_cdb_command_line_options_dbgspanspan-idddk_cdb_command_line_options_dbgspanparameters"></a><span id="ddk_cdb_command_line_options_dbg"></span><span id="DDK_CDB_COMMAND_LINE_OPTIONS_DBG"></span>パラメータ


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span>**-server** *servertransport*   
他のデバッガーからアクセスできるデバッグサーバーを作成します。 使用可能な*Servertransport*値の詳細については、「[**デバッグサーバーのアクティブ化**](activating-a-debugging-server.md)」を参照してください。 このパラメーターを使用する場合は、コマンドラインの最初のパラメーターである必要があります。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span>**-リモート** *clienttransport*   
デバッグクライアントを作成し、既に実行されているデバッグサーバーに接続します。 使用可能な*Clienttransport*値の詳細については、「[**デバッグクライアントのアクティブ化**](activating-a-debugging-client.md)」を参照してください。 このパラメーターを使用する場合は、コマンドラインの最初のパラメーターである必要があります。

<span id="_______-premote_______SmartClientTransport______"></span><span id="_______-premote_______smartclienttransport______"></span><span id="_______-PREMOTE_______SMARTCLIENTTRANSPORT______"></span>**-premote** *smartclienttransport*   
スマートクライアントを作成し、既に実行されているプロセスサーバーに接続します。 *Smartclienttransport*の有効な値の説明については、「[**スマートクライアントのアクティブ化**](activating-a-smart-client.md)」を参照してください。

<span id="_______-2______"></span>**-2**   
ターゲットアプリケーションが*コンソールアプリケーション*の場合、このオプションを指定すると、新しいコンソールウィンドウに表示されます。 (既定では、ターゲットコンソールアプリケーションで、ウィンドウを CDB または NTSD と共有するために使用されます)。

<span id="_______--______"></span>**--**   
クライアントサーバーの実行時サブシステム (CSRSS) をデバッグします。 詳細については、「 [CSRSS のデバッグ](debugging-csrss.md)」を参照してください。

<span id="_______-a_______Extension______"></span><span id="_______-a_______extension______"></span><span id="_______-A_______EXTENSION______"></span>**-** *拡張機能*   
既定の拡張 DLL を設定します。 既定値は*userexts*です。 "A" の後にスペースを入れないでください。また、.dll 拡張子を含めることはできません。 この既定値を設定するその他の方法については、「[デバッガー拡張 dll の読み込み](loading-debugger-extension-dlls.md)」を参照してください。

<span id="_______-bonc______"></span><span id="_______-BONC______"></span>**-bonc**   
このオプションを指定した場合、デバッガーはセッションが開始されるとすぐにターゲットに中断します。 これは、現在ターゲットに分割されていない可能性があるデバッグサーバーに接続する場合に特に便利です。

<span id="_______-c_________command______________"></span><span id="_______-C_________COMMAND______________"></span>**-c "** *command* **"**   
起動時に実行する初期デバッガーコマンドを指定します。 このコマンドは引用符で囲む必要があります。 複数のコマンドは、セミコロンで区切ることができます。 (長いコマンドリストがある場合は、それをスクリプトに挿入し、 **-c**オプションを[**$&lt;、$&gt;&lt;、$&gt;&lt;、$ $&gt;&lt; (スクリプトファイルの実行)**](-----------------------a---run-script-file-.md)コマンドで使用する方が簡単な場合があります)。

デバッグクライアントを開始する場合、このコマンドはデバッグサーバーを対象としている必要があります。 **Lsrcpath**などのクライアント固有のコマンドは使用できません。

<span id="_______-cf_________filename______________"></span><span id="_______-CF_________FILENAME______________"></span>**-cf "** *filename* **"**   
スクリプトファイルのパスと名前を指定します。 このスクリプトファイルは、デバッガーが開始されるとすぐに実行されます。 *Filename*にスペースが含まれている場合は、引用符で囲む必要があります。 パスを省略した場合は、現在のディレクトリと見なされます。 **-Cf**オプションが使用されていない場合、現在のディレクトリの ntsd ファイルがスクリプトファイルとして使用されます。 ファイルが存在しない場合、エラーは発生しません。 詳細については、「[スクリプトファイルの使用](using-script-files.md)」を参照してください。

<span id="_______-cfr_________filename______________"></span><span id="_______-CFR_________FILENAME______________"></span>**-cfr "** *filename* **"**   
スクリプトファイルのパスと名前を指定します。 このスクリプトファイルは、デバッガーが開始されたときと、ターゲットが再起動されるとすぐに実行されます。 *Filename*にスペースが含まれている場合は、引用符で囲む必要があります。 パスを省略した場合は、現在のディレクトリと見なされます。 ファイルが存在しない場合、エラーは発生しません。 詳細については、「[スクリプトファイルの使用](using-script-files.md)」を参照してください。

<span id="_______-cimp______"></span><span id="_______-CIMP______"></span>**-cimp**   
実行する明示的なプロセスではなく、DbgSrv の暗黙的なコマンドラインで CDB/NTSD に指示します。 このオプションは、dbgsrv-pc のクライアント側です。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span>**-clines** *lines*   
リモートデバッグ中にアクセスできるコマンド履歴のコマンドの概数を設定します。 詳細と、この数を変更するその他の方法については、「[デバッガーコマンドの使用](using-debugger-commands.md)」を参照してください。

<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
このデバッガーの制御をカーネルデバッガーに渡します。 CSRSS をデバッグしている場合、 **-d**が指定されていない場合でも、このコントロールリダイレクトは常にアクティブになります。 (リモートデバッグ中にこのオプションを使用することはできません。代わりに、- **ddefer**を使用してください)。詳細については[、「カーネルデバッガーからのユーザーモードデバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)」を参照してください。 このオプションは、 **-ddefer**オプションまたは **-noio**オプションと組み合わせて使用することはできません。

**注**  、windbg をカーネルデバッガーとして使用する場合、このシナリオでは、windbg の使い慣れた機能の多くを使用できません。 たとえば、[ローカル] ウィンドウ、[逆アセンブル] ウィンドウ、または [呼び出し履歴] ウィンドウを使用することはできません。また、ソースコードをステップ実行することもできません。 これは、WinDbg はターゲットコンピューターで実行されているデバッガー (NTSD または CDB) のビューアーとしてのみ機能するためです。

 

<span id="_______-ddefer______"></span><span id="_______-DDEFER______"></span>**-ddefer**   
デバッグクライアントが接続されていない限り、このデバッガーの制御をカーネルデバッガーに渡します。 (これは、デバッグサーバーから使用できる **-d**の一種です)。詳細については[、「カーネルデバッガーからのユーザーモードデバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)」を参照してください。 このオプションは、 **-d**オプションまたは **-noio**オプションと組み合わせて使用することはできません。

<span id="_______-e_______Event______"></span><span id="_______-e_______event______"></span><span id="_______-E_______EVENT______"></span>**-e** *イベント*   
指定されたイベントが発生したことをデバッガーに通知します。 このオプションは、プログラムによってデバッガーを起動する場合にのみ使用されます。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span>**-ee** {**masm**|**c++**}  
既定の式エバリュエーターを設定します。 **Masm**が指定されている場合は、masm 式の構文が使用されます。 **C++** が指定されC++ている場合は、式の構文が使用されます。 **-Ee**オプションを省略した場合、MASM 式の構文が既定値として使用されます。 詳細については、「[式の評価](evaluating-expressions.md)」をご覧ください。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span>**-failinc**   
デバッガーが疑わしいシンボルをすべて無視します。 ユーザーモードまたはカーネルモードのミニダンプファイルをデバッグする場合、このオプションを使用すると、イメージをマップできないモジュールをデバッガーで読み込むことができなくなります。 詳細およびその他の制御方法については、「 [Symopt\_EXACT\_SYMBOLS](symbol-options.md#symopt-exact-symbols)」を参照してください。

<span id="_______-g______"></span><span id="_______-G______"></span>**-g**   
ターゲットアプリケーションの最初のブレークポイントを無視します。 このオプションを選択すると、別のブレークポイントが設定されていない限り、ターゲットアプリケーションが開始された後、または CDB がアタッチされた後も、実行を継続します。 詳細については、[最初のブレークポイント](initial-breakpoint.md)を参照してください。

<span id="_______-G______"></span><span id="_______-g______"></span>**-G**   
プロセスの終了時に最後のブレークポイントを無視します。 既定では、イメージの実行中に CDB が停止します。 このオプションを指定すると、子が終了した時点で CDB がすぐに終了します。 これはコマンド**sxd epr**を入力した場合と同じ効果があります。 詳細については、「[例外とイベントの制御](controlling-exceptions-and-events.md)」を参照してください。

<span id="_______-hd______"></span><span id="_______-HD______"></span>**-hd**   
 デバッグヒープを使用しないことを指定します。 詳細について[は、「CDB を使用したユーザーモードプロセスのデバッグ](debugging-a-user-mode-process-using-cdb.md)」を参照してください。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span>**-i** *ImagePath*   
エラーを生成した実行可能ファイルの場所を指定します。 パスにスペースが含まれている場合は、引用符で囲む必要があります。

<span id="_______-iae______"></span><span id="_______-IAE______"></span>**-iae**   
CDB を事後分析デバッガーとしてインストールします。 詳細については、「[事後分析デバッグの有効化](enabling-postmortem-debugging.md)」を参照してください。

この操作が成功した場合、メッセージは表示されません。失敗した場合は、エラーメッセージが表示されます。

**-Iae**パラメーターを他のパラメーターと共に使用することはできません。 このコマンドは、実際には CDB を起動しません。

<span id="_______-iaec_______KeyString______"></span><span id="_______-iaec_______keystring______"></span><span id="_______-IAEC_______KEYSTRING______"></span>**-iaec** *keystring*   
CDB を事後分析デバッガーとしてインストールします。 *Keystring*の内容は、 **AeDebug**レジストリキーの末尾に追加されます。 *Keystring*にスペースが含まれている場合は、引用符で囲む必要があります。 詳細については、「[事後分析デバッグの有効化](enabling-postmortem-debugging.md)」を参照してください。

この操作が成功した場合、メッセージは表示されません。失敗した場合は、エラーメッセージが表示されます。

**-Iaec**パラメーターを他のパラメーターと共に使用することはできません。 このコマンドは、実際には CDB を起動しません。

<span id="_______-isd______"></span><span id="_______-ISD______"></span>**-isd**   
プロセスの作成について、[\_システムの\_を無視する]\_既定のフラグをオンにします。

<span id="_______-iu________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span>**-iu** *keystring*   
Url 型としてデバッガーのリモート処理を登録し、ユーザーが URL を使用してデバッガーのリモートクライアントを自動起動できるようにします。 *Keystring*には `remdbgeng://RemotingOption`の形式があります。 *Remotingoption*は、「[**デバッグクライアントをアクティブ化する**](activating-a-debugging-client.md)」で定義されているトランスポートプロトコルを定義する文字列です。 この操作が成功した場合、メッセージは表示されません。失敗した場合は、エラーメッセージが表示されます。

**-Iu**パラメーターは、他のパラメーターと共に使用することはできません。 このコマンドは、実際には CDB を起動しません。

<span id="_______-kqm______"></span><span id="_______-KQM______"></span>**-kqm**   
非表示モードで CDB/NTSD を開始します。

<span id="_______-lines______"></span><span id="_______-LINES______"></span>**-行**   
ソース行のデバッグを有効にします。 このオプションを省略した場合は、ソースのデバッグを許可する前に、 [**. lines (ソースラインサポートの切り替え)**](-lines--toggle-source-line-support-.md)コマンドを使用する必要があります。 これを制御するその他の方法については、「 [Symopt\_LOAD\_LINES](symbol-options.md#symopt-load-lines)」を参照してください。

<span id="_______-log_a_au_o_ou__LogFile"></span><span id="_______-log_a_au_o_ou__logfile"></span><span id="_______-LOG_A_AU_O_OU__LOGFILE"></span>**-ログ**{**a | au | o | ou**}*ログファイル*  
ログファイルへの情報のログ記録を開始します。 指定したファイルが既に存在する場合は、 **-logo**が使用されていると上書きされます。-loga が使用されている場合は、出力がファイルに追加されます。 **-Logau**オプションと **-logau**オプションは、それぞれ、ログファイルが Unicode ファイルであることを除いて、 **-logau**および-- **logo**と同様に動作します。 詳細については、「 [CDB でのログファイルの保持](keeping-a-log-file-in-cdb.md)」を参照してください。

<span id="_______-myob______"></span><span id="_______-MYOB______"></span>**-myob**   
Dbghelp .dll とのバージョンが一致しない場合、デバッガーは引き続き実行されます。 ( **-Myob**スイッチがないと、これは致命的なエラーと見なされます)。

<span id="_______-n______"></span><span id="_______-N______"></span>**-n**   
*ノイズシンボルの読み込み*: シンボルハンドラーからの詳細出力を有効にします。 詳細およびその他の制御方法については、「 [Symopt\_デバッグ](symbol-options.md#symopt-debug)」を参照してください。

<span id="_______-netsyms__yes_no_______"></span><span id="_______-NETSYMS__YES_NO_______"></span>**-netsyms {yes | no}**   
ネットワークパスからのシンボルの読み込みを許可または禁止します。

<span id="_______-noinh______"></span><span id="_______-NOINH______"></span>**-noinh**   
デバッガーによって作成されたプロセスがデバッガーからハンドルを継承できないようにします。 これを制御するその他の方法については、「 [CDB を使用したユーザーモードプロセスのデバッグ](debugging-a-user-mode-process-using-cdb.md)」を参照してください。

<span id="_______-noio______"></span><span id="_______-NOIO______"></span>**-noio**   
デバッグサーバーを入力または出力に使用しないようにします。 入力は、デバッグクライアント (および **-c**コマンドラインオプションで指定された最初のコマンドまたはコマンドスクリプト) からのみ受け入れられます。

すべての出力は、デバッグクライアントに送られます。 サーバーに NTSD が使用されている場合、コンソールウィンドウはまったく作成されません。 詳細については、「[**デバッグサーバーのアクティブ化**](activating-a-debugging-server.md)」を参照してください。 このオプションは、 **-d**オプションまたは **-ddefer**オプションと組み合わせて使用することはできません。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span>**-noshell**   
すべて**のシェル**コマンドを禁止します。 この禁止は、新しいデバッグセッションが開始された場合でも、デバッガーが実行されている限り最後に実行されます。 詳細と、シェルコマンドを無効にするその他の方法については、「[シェルコマンドの使用](using-shell-commands.md)」を参照してください **。**

<span id="_______-nosqm______"></span><span id="_______-NOSQM______"></span>**-nosqm**   
テレメトリデータの収集とアップロードを無効にします。

<span id="_______-o______"></span><span id="_______-O______"></span>**-o**   
ターゲットアプリケーション (子プロセス) によって起動されたすべてのプロセスをデバッグします。 既定では、デバッグ中のプロセスによって作成されたプロセスは、通常どおり実行されます。 これを制御するその他の方法については、「 [CDB を使用したユーザーモードプロセスのデバッグ](debugging-a-user-mode-process-using-cdb.md)」を参照してください。

<span id="_______-p_______PID______"></span><span id="_______-p_______pid______"></span><span id="_______-P_______PID______"></span>**-p** *PID*   
デバッグする10進プロセス ID を指定します。 これは、既に実行中のプロセスをデバッグするために使用されます。 詳細については、「 [CDB を使用したユーザーモードプロセスのデバッグ](debugging-a-user-mode-process-using-cdb.md)」を参照してください。

<span id="_______-pb______"></span><span id="_______-PB______"></span>**-pb**   
ターゲットプロセスにアタッチするときに、デバッガーが初期のブレークインを要求できないようにします。 これは、アプリケーションが既に中断されている場合や、ターゲットに中断スレッドを作成しないようにする必要がある場合に役立ちます。

<span id="_______-pd______"></span><span id="_______-PD______"></span>**-pd**   
デバッグセッションの終了時にターゲットアプリケーションが終了しないようにします。 詳細については[、「CDB でのデバッグセッションの終了](ending-a-debugging-session-in-cdb.md)」を参照してください。

<span id="_______-pe______"></span><span id="_______-PE______"></span>**-pe**   
ターゲットアプリケーションが既にデバッグされていることを示します。 詳細について[は、「ターゲットアプリケーションへの再アタッチ](reattaching-to-the-target-application.md)」を参照してください。

<span id="_______-pn_______Name______"></span><span id="_______-pn_______name______"></span><span id="_______-PN_______NAME______"></span>**-pn** *名前*   
デバッグするプロセスの名前を指定します。 (この名前は一意である必要があります)。これは、既に実行中のプロセスをデバッグするために使用されます。

<span id="_______-pr______"></span><span id="_______-PR______"></span>**-pr**   
デバッガーがアタッチされたときに、実行中のターゲットプロセスを起動します。 これは、アプリケーションが既に中断されていて、実行を再開する場合に便利です。

<span id="_______-psn_______ServiceName______"></span><span id="_______-psn_______servicename______"></span><span id="_______-PSN_______SERVICENAME______"></span>**-psn** *ServiceName*   
デバッグするプロセスに含まれるサービスの名前を指定します。 これは、既に実行中のプロセスをデバッグするために使用されます。

<span id="_______-pt_______Seconds______"></span><span id="_______-pt_______seconds______"></span><span id="_______-PT_______SECONDS______"></span>**-pt** *秒*   
ブレークタイムアウトを秒単位で指定します。 既定値は 30 です。 詳細について[は、「ターゲットの制御](controlling-the-target.md)」を参照してください。

<span id="_______-pv______"></span><span id="_______-PV______"></span>**-pv**   
デバッガーをターゲットプロセス noninvasively にアタッチするように指定します。 詳細については、「 [Noninvasive デバッグ (ユーザーモード)](noninvasive-debugging--user-mode-.md)」を参照してください。

<span id="_______-pvr______"></span><span id="_______-PVR______"></span>**-pvr**   
は、ターゲットプロセスが中断されていないことを除いて **、-pv**のように動作します。

<span id="_______-QR_______Server______"></span><span id="_______-qr_______server______"></span><span id="_______-QR_______SERVER______"></span>**-QR** *サーバー*   
指定したネットワークサーバー上で実行されているすべてのデバッグサーバーを一覧表示します。 2つの円記号 (\\\) 前の*サーバー*は省略可能です。 詳細については、「[**デバッグサーバーの検索**](searching-for-debugging-servers.md)」を参照してください。

**-QR**パラメーターを他のパラメーターと共に使用することはできません。 このコマンドは、実際には CDB を起動しません。

<span id="_______-r________BreakErrorLevel______"></span><span id="_______-r________breakerrorlevel______"></span><span id="_______-R________BREAKERRORLEVEL______"></span>**-r** *breakerrorlevel*   
ターゲットがデバッガーに分割される原因となるエラーレベルを指定します。 これは、0、1、2、または3に等しい10進数です。 使用できる値は次のとおりです。

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
<td align="left"><p>エラーが発生しても中断しないでください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>エラー</p></td>
<td align="left"><p>エラーレベルのデバッグイベントを中断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>MINORERROR およびエラーレベルのデバッグイベントで中断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>警告、MINORERROR、およびエラーレベルのデバッグイベントで中断します。</p></td>
</tr>
</tbody>
</table>

 

このエラーレベルは、Microsoft Windows のチェックされたビルドでのみ意味があります。 既定値は 1 です。 チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。

<span id="_______-robp______"></span><span id="_______-ROBP______"></span>**-robp**   
これにより、CDB は読み取り専用メモリページにブレークポイントを設定できます。 (既定では、このような操作は失敗します)。

<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
遅延シンボルの読み込みを無効にします。 これにより、プロセスの起動が遅くなります。 詳細およびその他の制御方法については、「 [Symopt\_遅延\_読み込み](symbol-options.md#symopt-deferred-loads)」を参照してください。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span>**-sdce**   
シンボルの読み込み中に、デバッガーが**ファイルアクセスエラー**ダイアログボックスを表示します。 詳細およびその他の制御方法については、「 [Symopt\_FAIL\_重大\_エラー](symbol-options.md#symopt-fail-critical-errors)」を参照してください。

<span id="_______-ses______"></span><span id="_______-SES______"></span>**-ses**   
デバッガーがすべてのシンボルファイルの厳密な評価を実行し、疑わしいシンボルをすべて無視します。 詳細およびその他の制御方法については、「 [Symopt\_EXACT\_SYMBOLS](symbol-options.md#symopt-exact-symbols)」を参照してください。

<span id="_______-sflags_0x_______Number______"></span><span id="_______-sflags_0x_______number______"></span><span id="_______-SFLAGS_0X_______NUMBER______"></span>**-sflags 0x** *Number*   
すべてのシンボルハンドラーオプションを一度に設定します。 *Number*は**0x**で始まる16進数の数字にする必要があります。 **0x**が指定されていない10進数を使用できますが、シンボルオプションはバイナリフラグであるため、16進数を使用することをお勧めします。 このオプションは、すべてのシンボルハンドラーの既定値をオーバーライドするため、注意して使用する必要があります。 詳細については、「[シンボルオプションの設定](symbol-options.md)」を参照してください。

<span id="_______-sicv______"></span><span id="_______-SICV______"></span>**-sicv**   
シンボルハンドラーが CV レコードを無視するようにします。 詳細およびこれを制御するその他の方法については、「 [Symopt\_IGNORE\_CVREC](symbol-options.md#symopt-ignore-cvrec)」を参照してください。

<span id="_______-sins______"></span><span id="_______-SINS______"></span>**-sins**   
デバッガーがシンボルパスと実行可能イメージパス環境変数を無視するようにします。 詳細については、「 [Symopt\_IGNORE\_NT\_SYMPATH](symbol-options.md#symopt-ignore-nt-sympath)」を参照してください。

<span id="_______-snc______"></span><span id="_______-SNC______"></span>**-snc**   
デバッガーが変換をオフC++にします。 詳細およびその他の制御方法については、「 [Symopt\_no\_CPP](symbol-options.md#symopt-no-cpp)」を参照してください。

<span id="_______-snul______"></span><span id="_______-SNUL______"></span>**-snul**   
非修飾名に対するシンボルの自動読み込みを無効にします。 詳細およびその他の制御方法については、「 [Symopt\_no\_非修飾\_読み込み](symbol-options.md#symopt-no-unqualified-loads)」を参照してください。

<span id="_______-srcpath_______SourcePath______"></span><span id="_______-srcpath_______sourcepath______"></span><span id="_______-SRCPATH_______SOURCEPATH______"></span>**-srcpath** *SourcePath*   
ソースファイルの検索パスを指定します。 複数のパスをセミコロン (;) で区切ります。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細について、およびこのパスを変更するその他の方法については、「[ソースパス](source-path.md)」を参照してください。

<span id="_______-sup______"></span><span id="_______-SUP______"></span>**-sup**   
シンボルを検索するたびに、シンボルハンドラーがパブリックシンボルテーブルを検索します。 詳細およびその他の制御方法については、「 [Symopt\_AUTO\_PUBLICS](symbol-options.md#symopt-auto-publics)」を参照してください。

<span id="_______-t________PrintErrorLevel______"></span><span id="_______-t________printerrorlevel______"></span><span id="_______-T________PRINTERRORLEVEL______"></span>**-t** *プリンター rorlevel*   
デバッガーにエラーメッセージを表示させるエラーレベルを指定します。 これは、0、1、2、または3に等しい10進数です。 使用できる値は次のとおりです。

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
<td align="left"><p>エラーを表示しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>エラー</p></td>
<td align="left"><p>エラーレベルのデバッグイベントを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>MINORERROR およびエラーレベルのデバッグイベントを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>警告、MINORERROR、およびエラーレベルのデバッグイベントを表示します。</p></td>
</tr>
</tbody>
</table>

 

このエラーレベルは、Microsoft Windows のチェックされたビルドでのみ意味があります。 チェックされたビルドは、Windows 10 バージョン1803より前の以前のバージョンの Windows で使用できました。 既定値は 1 です。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
デバッガーからの詳細出力を有効にします。

<span id="_______-version______"></span><span id="_______-VERSION______"></span>**-バージョン**   
デバッガーのバージョン文字列を出力します。

<span id="_______-vf______"></span><span id="_______-VF______"></span>**-vf**   
既定の ApplicationVerifier 設定を有効にします。

<span id="_______-vf________opts_"></span><span id="_______-VF________OPTS_"></span>**-vf:&lt;は** *&gt;*  
指定された ApplicationVerifier 設定を有効にします。

<span id="_______-w______"></span><span id="_______-W______"></span>**-w**   
16ビットアプリケーションを別の VDM でデバッグすることを指定します。

<span id="_______-wake_______PID______"></span><span id="_______-wake_______pid______"></span><span id="_______-WAKE_______PID______"></span>**-wake** *PID*   
*PID*によってプロセス ID が指定されているユーザーモードデバッガーのスリープモードを終了します。 このコマンドは、スリープモード中にターゲットコンピューター上で発行する必要があります。 詳細については[、「カーネルデバッガーからのユーザーモードデバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)」を参照してください。

**-Wake**パラメーターを他のパラメーターと共に使用することはできません。 このコマンドは、実際には CDB を起動しません。

<span id="_______-x_e_d_n_i__Exception"></span><span id="_______-x_e_d_n_i__exception"></span><span id="_______-X_E_D_N_I__EXCEPTION"></span>**-x**{**e**|**d**|**n**|**i**}*例外*  
指定されたイベントが発生したときのデバッガーの動作を制御します。 例外*には*、例外番号とイベントコードのどちらかを指定できます。 このオプションを複数回指定して、さまざまなイベントを制御できます。 詳細については、[例外とイベントの制御](controlling-exceptions-and-events.md)に関する説明、およびこれらの設定を制御するその他の方法を参照してください。

<span id="_______-x______"></span><span id="_______-X______"></span>**-x**   
アクセス違反例外の初回の中断を無効にします。 2回目のアクセス違反が発生すると、デバッガーは中断されます。 これは、 **xd av**と同じです。

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span>**-y** *シンボルパス*   
シンボルの検索パスを指定します。 複数のパスをセミコロン (;) で区切ります。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細およびこのパスを変更するその他の方法については、「[シンボルパス](symbol-path.md)」を参照してください。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span>**-z** *ダンプファイル*   
デバッグするクラッシュダンプファイルの名前を指定します。 パスとファイル名にスペースが含まれている場合、引用符で囲む必要があります。 複数**の**ダンプファイルを同時に開くことができます。その際、それぞれに異なる*ダンプファイル*値を指定します。 詳細については、「[ユーザーモードのダンプファイルの分析](analyzing-a-user-mode-dump-file.md)」を参照してください。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span>**-zp** *ページファイル*   
変更されたページファイルの名前を指定します。 これは、ダンプファイルをデバッグしていて、[**ページイン (Page In Memory)**](-pagein--page-in-memory-.md)コマンドを使用する場合に便利です。 標準の Windows ページファイルで **-zp**を使用することはできません。特別に変更されたページファイルのみ使用できます。

<span id="_______executable______"></span><span id="_______EXECUTABLE______"></span>*実行可能ファイル*   
実行可能プロセスのコマンドラインを指定します。 これは、新しいプロセスを起動してデバッグするために使用されます。 これは、コマンドラインの最後の項目である必要があります。 実行可能ファイル名の後にあるすべてのテキストが、実行可能ファイルに引数文字列として渡されます。

<span id="_______-_______"></span>**-?**   
コマンドラインのヘルプテキストを表示します。

Start | からデバッガーを起動するとき**または**コマンドプロンプトウィンドウで、アプリケーションのファイル名の後にターゲットアプリケーションの引数を指定します。 例:

```dbgcmd
cdb myexe arg1arg2
```

 

 





