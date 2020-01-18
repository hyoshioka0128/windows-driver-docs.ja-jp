---
title: WinDbg のコマンドライン オプション
description: WinDbg の初回ユーザーは、WinDbg セクションを使用したデバッグを開始する必要があります。
ms.assetid: bd169c73-0a46-41b5-bd7b-71adf7747069
keywords:
- WinDbg のコマンドラインオプション Windows のデバッグ
ms.date: 08/10/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- WinDbg Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 304e083f7220234ea55f997527fa5ad3a25f9be2
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256750"
---
# <a name="windbg-command-line-options"></a>WinDbg のコマンドライン オプション

WinDbg の初回ユーザーは、 [windbg セクションを使用](debugging-using-windbg.md)したデバッグを開始する必要があります。

WinDbg コマンドラインでは、次の構文を使用します。

```dbgsyntax
windbg [ -server ServerTransport | -remote ClientTransport ] [-lsrcpath ]
   [ -premote SmartClientTransport ] [-?] [-ee {masm|c++}] 
   [-clines lines] [-b] [-d] [-aExtension]  
   [-failinc] [-g] [-G] [-hd] [-j] [-n] [-noshell] [-o] [-openPrivateDumpByHandle Handle]
   [-Q | -QY] [-QS | -QSY] [-robp] [-secure] [-ses] [-sdce] 
   [-sicv] [-sins] [-snc] [-snul] [-sup] [-sflags 0xNumber] 
   [-T Title] [-v] [-log{o|a} LogFile] [-noinh] 
   [-i ImagePath] [-y SymbolPath] [-srcpath SourcePath] 
   [-k [ConnectType] | -kl | -kx ExdiOptions] [-c "command"] 
   [-pb] [-pd] [-pe] [-pr] [-pt Seconds] [-pv]
   [-W Workspace] [-WF Filename] [-WX] [-zp PageFile] 
   [ -p PID | -pn Name | -psn ServiceName | -z DumpFile | executable ] 

windbg -I[S] 

windbg -IU KeyString

windbg -IA[S] 
```

WinDbg コマンドラインオプションの説明は次のようになります。 **-J**を除き、すべてのコマンドラインオプションで大文字と小文字が区別されます。 先頭のハイフンは、スラッシュ (/) に置き換えることができます。

**-Remote**または **-server**オプションを使用する場合は、コマンドラインの他のオプションの前に指定する必要があります。 *実行可能ファイル*が指定されている場合は、コマンドラインで最後に指定する必要があります。*実行可能*ファイル名の後のテキストは、独自のコマンドラインパラメーターとして実行可能プログラムに渡されます。

## <a name="span-idddk_windbg_command_line_options_dbgspanspan-idddk_windbg_command_line_options_dbgspanparameters"></a><span id="ddk_windbg_command_line_options_dbg"></span><span id="DDK_WINDBG_COMMAND_LINE_OPTIONS_DBG"></span>パラメータ


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span> **-server** *servertransport*   
他のデバッガーからアクセスできるデバッグサーバーを作成します。 使用可能な*Servertransport*値の詳細については、「[**デバッグサーバーのアクティブ化**](activating-a-debugging-server.md)」を参照してください。 このパラメーターを使用する場合は、コマンドラインの最初のパラメーターである必要があります。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span> **-リモート** *clienttransport*   
デバッグクライアントを作成し、既に実行されているデバッグサーバーに接続します。 使用可能な*Clienttransport*値の詳細については、「[**デバッグクライアントのアクティブ化**](activating-a-debugging-client.md)」を参照してください。 このパラメーターを使用する場合は、コマンドラインの最初のパラメーターである必要があります。

<span id="_______-premote_______SmartClientTransport______"></span><span id="_______-premote_______smartclienttransport______"></span><span id="_______-PREMOTE_______SMARTCLIENTTRANSPORT______"></span> **-premote** *smartclienttransport*   
スマートクライアントを作成し、既に実行されているプロセスサーバーに接続します。 *Smartclienttransport*の有効な値の説明については、「[**スマートクライアントのアクティブ化**](activating-a-smart-client.md)」を参照してください。

<span id="_______-a________Extension______"></span><span id="_______-a________extension______"></span><span id="_______-A________EXTENSION______"></span> **-** *拡張機能*   
既定の拡張 DLL を設定します。 既定値は kdextx86 または kdexts です。 "A" の後にスペースを入れないでください。また、.dll ファイル名拡張子を含めることはできません。 この既定値を設定するその他の方法については、「[デバッガー拡張 dll の読み込み](loading-debugger-extension-dlls.md)」を参照してください。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
このオプションはサポートされなくなりました。

<span id="_______-c_________command______________"></span><span id="_______-C_________COMMAND______________"></span> **-c "** *command* **"**    
起動時に実行する初期デバッガーコマンドを指定します。 このコマンドは引用符で囲む必要があります。 複数のコマンドは、セミコロンで区切ることができます。 (長いコマンドリストがある場合は、それをスクリプトに挿入し、 **-c**オプションを[ **$&lt;、$&gt;&lt;、$&gt;&lt;、$ $&gt;&lt; (スクリプトファイルの実行)** ](-----------------------a---run-script-file-.md)コマンドで使用する方が簡単な場合があります)。

デバッグクライアントを開始する場合、このコマンドはデバッグサーバーを対象としている必要があります。 **Lsrcpath**などのクライアント固有のコマンドは使用できません。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span> **-clines** *lines*   
リモートデバッグ中にアクセスできるコマンド履歴のコマンドの概数を設定します。 詳細と、この数を変更するその他の方法については、「[デバッガーコマンドの使用](using-debugger-commands.md)」を参照してください。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
(カーネルモードのみ)再起動後、カーネルモジュールが読み込まれるとすぐに、デバッガーはターゲットコンピューターを中断します。 (これは、 **-b**オプションの中断よりも前のものです)。詳細およびこの状態を変更するその他の方法については、「[ターゲットコンピューターのクラッシュと再起動](crashing-and-rebooting-the-target-computer.md)」を参照してください。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span> **-ee** {**masm**|**c++** }  
既定の式エバリュエーターを設定します。 **Masm**が指定されている場合は、masm 式の構文が使用されます。 **C++** が指定されC++ている場合は、式の構文が使用されます。 **-Ee**オプションを省略した場合、MASM 式の構文が既定値として使用されます。 詳細については、「[式の評価](evaluating-expressions.md)」をご覧ください。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span> **-failinc**   
デバッガーが疑わしいシンボルをすべて無視します。 ユーザーモードまたはカーネルモードのミニダンプファイルをデバッグする場合、このオプションを使用すると、イメージをマップできないモジュールをデバッガーで読み込むことができなくなります。 詳細およびその他の制御方法については、「 [Symopt\_EXACT\_SYMBOLS](symbol-options.md#symopt-exact-symbols)」を参照してください。

<span id="_______-g______"></span><span id="_______-G______"></span> **-g**   
(ユーザーモードのみ)ターゲットアプリケーションの最初のブレークポイントを無視します。 このオプションを選択すると、別のブレークポイントが設定されていない限り、開始された後、または WinDbg がアタッチされた後も、ターゲットアプリケーションは実行を継続します。 詳細については、[最初のブレークポイント](initial-breakpoint.md)を参照してください。

<span id="_______-G______"></span><span id="_______-g______"></span> **-G**   
(ユーザーモードのみ)プロセスの終了時に最後のブレークポイントを無視します。 通常、デバッグセッションは、イメージの実行プロセス中に終了します。 このオプションを指定すると、子が終了するとすぐにデバッグセッションが終了します。 これはコマンド**sxd epr**を入力した場合と同じ効果があります。 詳細については、「[例外とイベントの制御](controlling-exceptions-and-events.md)」を参照してください。

<span id="_______-hd______"></span><span id="_______-HD______"></span> **-hd**   
(ユーザーモードのみ)デバッグヒープを使用しないことを指定します。

<span id="_______-I_S_"></span><span id="_______-i_s_"></span> **-I**\[**S**\]  
WinDbg を事後分析デバッガーとしてインストールします。 詳細については、「[事後分析デバッグの有効化](enabling-postmortem-debugging.md)」を参照してください。

この操作が試行されると、成功または失敗のメッセージが表示されます。 が**含まれている場合**、このプロシージャは正常に実行されると、サイレントモードで実行されます。エラーメッセージのみが表示されます。

**-I**パラメーターを他のパラメーターと共に使用することはできません。 このコマンドでは、windbg を開始することはできませんが、WinDbg ウィンドウはすぐに表示されます。

<span id="_______-IA_S_"></span><span id="_______-ia_s_"></span> **-IA**\[**S**\]  
ファイル拡張子 .dmp、mdmp、および wew と共に、レジストリに WinDbg を関連付けます。 この操作が試行されると、成功または失敗のメッセージが表示されます。 が**含まれている場合**、このプロシージャは正常に実行されると、サイレントモードで実行されます。エラーメッセージのみが表示されます。 この関連付けが行われた後、これらの拡張機能のいずれかを使用してファイルをダブルクリックすると、WinDbg が開始されます。

**-IA**パラメーターを他のパラメーターと共に使用することはできません。 このコマンドでは、windbg を開始することはできませんが、WinDbg ウィンドウはすぐに表示されます。

<span id="_______-IU________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span> **-IU** *keystring*   
Url 型としてデバッガーのリモート処理を登録し、ユーザーが URL を使用してデバッガーのリモートクライアントを自動起動できるようにします。 *Keystring*には `remdbgeng://RemotingOption`の形式があります。 *Remotingoption*は、「[**デバッグクライアントをアクティブ化する**](activating-a-debugging-client.md)」で定義されているトランスポートプロトコルを定義する文字列です。 この操作が成功した場合、メッセージは表示されません。失敗した場合は、エラーメッセージが表示されます。

**-IU**パラメーターは、他のパラメーターと共に使用することはできません。 WinDbg ウィンドウはしばらく表示される場合がありますが、このコマンドは実際には WinDbg を開始しません。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span> **-i** *ImagePath*   
エラーを生成した実行可能ファイルの場所を指定します。 パスにスペースが含まれている場合は、引用符で囲む必要があります。

<span id="_______-j______"></span><span id="_______-J______"></span> **-j**   
ジャーナルを許可します。

<span id="_______-k__ConnectType_"></span><span id="_______-k__connecttype_"></span><span id="_______-K__CONNECTTYPE_"></span> **-k** \[*connecttype*\]  
(カーネルモードのみ)カーネルデバッグセッションを開始します。 詳細については、「 [WinDbg を使用したライブカーネルモードデバッグ](performing-kernel-mode-debugging-using-windbg.md)」を参照してください。 **-K**が、その後に*connecttype*オプションを指定せずに使用されている場合は、コマンドラインの最後のエントリである必要があります。

<span id="_______-kl______"></span><span id="_______-KL______"></span> **-kl ダイバージェンス**   
(カーネルモードのみ)デバッガーと同じコンピューター上でカーネルデバッグセッションを開始します。

<span id="_______-kx_______ExdiOptions______"></span><span id="_______-kx_______exdioptions______"></span><span id="_______-KX_______EXDIOPTIONS______"></span> **-kx** *exdioptions*   
(カーネルモードのみ)EXDI ドライバーを使用して、カーネルデバッグセッションを開始します。 EXDI ドライバーについては、このドキュメントでは説明しません。 ハードウェアプローブまたはハードウェアシミュレーターへの EXDI インターフェイスがある場合は、デバッグ情報について Microsoft にお問い合わせください。

<span id="_______-log_o_a__LogFile"></span><span id="_______-log_o_a__logfile"></span><span id="_______-LOG_O_A__LOGFILE"></span> **-ログ**{**o**|**a**} ログ*ファイル*  
ログファイルへの情報のログ記録を開始します。 指定したログファイルが既に存在する場合は、 **-logo**が使用されていると上書きされます。 **Loga**が使用されている場合は、出力がファイルに追加されます。 詳細については、「 [WinDbg でのログファイルの保持](keeping-a-log-file-in-windbg.md)」を参照してください。

<span id="_______-lsrcpath______"></span><span id="_______-LSRCPATH______"></span> **-lsrcpath**   
リモートクライアントのローカルソースパスを設定します。 このオプションは、コマンドラインで **-remote**の後に指定する必要があります。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
*ノイズシンボルの読み込み*: シンボルハンドラーからの詳細出力を有効にします。 詳細およびその他の制御方法については、「 [Symopt\_デバッグ](symbol-options.md#symopt-debug)」を参照してください。

<span id="_______-noinh______"></span><span id="_______-NOINH______"></span> **-noinh**   
(ユーザーモードのみ)デバッガーによって作成されたプロセスがデバッガーからハンドルを継承できないようにします。 これを制御するその他の方法については、「 [WinDbg を使用したユーザーモードプロセスのデバッグ](debugging-a-user-mode-process-using-windbg.md)」を参照してください。

<span id="_______-noprio______"></span><span id="_______-NOPRIO______"></span> **-noprio**   
優先順位を変更しないようにします。 このパラメーターを指定すると、WinDbg がアクティブな間、CPU 時間の優先順位を取得できなくなります。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span> **-noshell**   
すべて**のシェル**コマンドを禁止します。 この禁止は、新しいデバッグセッションが開始された場合でも、デバッガーが実行されている限り最後に実行されます。 詳細と、シェルコマンドを無効にするその他の方法については、「[シェルコマンドの使用](using-shell-commands.md)」を参照してください。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
(ユーザーモードのみ)ターゲットアプリケーション (子プロセス) によって起動されたすべてのプロセスをデバッグします。 既定では、デバッグ中のプロセスによって作成されたプロセスは、通常どおり実行されます。

<span id="_______-openPrivateDumpByHandle______"></span><span id="_______-OPENPRIVATEDUMPBYHANDLE______"></span> **-openprivatedumpbyhandle** *ハンドル *  
デバッグするクラッシュダンプファイルのハンドルを指定します。

<span id="_______-p_______PID______"></span><span id="_______-p_______pid______"></span><span id="_______-P_______PID______"></span> **-p** *PID*   
デバッグする10進プロセス ID を指定します。 これは、既に実行中のプロセスをデバッグするために使用されます。

<span id="_______-pb______"></span><span id="_______-PB______"></span> **-pb**   
(ユーザーモードのみ)ターゲットプロセスにアタッチするときに、デバッガーが初期のブレークインを要求できないようにします。 これは、アプリケーションが既に中断されている場合や、ターゲットに中断スレッドを作成しないようにする必要がある場合に役立ちます。

<span id="_______-pd______"></span><span id="_______-PD______"></span> **-pd**   
(ユーザーモードのみ)デバッグセッションの終了時にターゲットアプリケーションが終了しないようにします。 詳細については[、「WinDbg でのデバッグセッションの終了](ending-a-debugging-session-in-windbg.md)」を参照してください。

<span id="_______-pe______"></span><span id="_______-PE______"></span> **-pe**   
(ユーザーモードのみ)ターゲットアプリケーションが既にデバッグされていることを示します。 詳細について[は、「ターゲットアプリケーションへの再アタッチ](reattaching-to-the-target-application.md)」を参照してください。

<span id="_______-pn_______Name______"></span><span id="_______-pn_______name______"></span><span id="_______-PN_______NAME______"></span> **-pn** *名前*   
デバッグするプロセスの名前を指定します。 (この名前は一意である必要があります)。これは、既に実行中のプロセスをデバッグするために使用されます。

<span id="_______-pr______"></span><span id="_______-PR______"></span> **-pr**   
(ユーザーモードのみ)デバッガーがアタッチされたときに、実行中のターゲットプロセスを起動します。 これは、アプリケーションが既に中断されていて、実行を再開する場合に便利です。

<span id="_______-psn_______ServiceName______"></span><span id="_______-psn_______servicename______"></span><span id="_______-PSN_______SERVICENAME______"></span> **-psn** *ServiceName*   
デバッグするプロセスに含まれるサービスの名前を指定します。 これは、既に実行中のプロセスをデバッグするために使用されます。

<span id="_______-pt_______Seconds______"></span><span id="_______-pt_______seconds______"></span><span id="_______-PT_______SECONDS______"></span> **-pt** *秒*   
ブレークタイムアウトを秒単位で指定します。 既定値は 30 です。 詳細について[は、「ターゲットの制御](controlling-the-target.md)」を参照してください。

<span id="_______-pv______"></span><span id="_______-PV______"></span> **-pv**   
(ユーザーモードのみ)デバッガーをターゲットプロセス noninvasively にアタッチするように指定します。 詳細については、「 [Noninvasive デバッグ (ユーザーモード)](noninvasive-debugging--user-mode-.md)」を参照してください。

<span id="_______-Q______"></span><span id="_______-q______"></span> **-Q**   
"ワークスペースの保存" を抑制します。 ダイアログ ボックスでオプションを指定するときは、表を参考にしてください。 ワークスペースは自動的には保存されません。 詳細については、「[ワークスペースの使用」を](using-workspaces.md)ご覧ください。

<span id="_______-QS______"></span><span id="_______-qs______"></span> **-QS**   
"ソースの再読み込み" を抑制します。 ダイアログ ボックスでオプションを指定するときは、表を参考にしてください。 ソースファイルは自動的に再読み込みされません。

<span id="_______-QSY______"></span><span id="_______-qsy______"></span> **-QSY**   
"ソースの再読み込み" を抑制します。 を選択すると、ソースファイルが自動的に再読み込みされます。

<span id="_______-QY______"></span><span id="_______-qy______"></span> **-QY**   
"ワークスペースの保存" を抑制します。 ダイアログボックスが自動的にワークスペースを保存します。 詳細については、「[ワークスペースの使用」を](using-workspaces.md)ご覧ください。

<span id="_______-robp______"></span><span id="_______-ROBP______"></span> **-robp**   
これにより、CDB は読み取り専用メモリページにブレークポイントを設定できます。 (既定では、このような操作は失敗します)。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span> **-sdce**   
シンボルの読み込み中に、デバッガーが**ファイルアクセスエラー**メッセージを表示します。 詳細およびその他の制御方法については、「 [Symopt\_FAIL\_重大\_エラー](symbol-options.md#symopt-fail-critical-errors)」を参照してください。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span> **-セキュリティで保護された**   
[保護モード](secure-mode.md)をアクティブにします。

<span id="_______-ses______"></span><span id="_______-SES______"></span> **-ses**   
デバッガーがすべてのシンボルファイルの厳密な評価を実行し、疑わしいシンボルをすべて無視します。 詳細およびその他の制御方法については、「 [Symopt\_EXACT\_SYMBOLS](symbol-options.md#symopt-exact-symbols)」を参照してください。

<span id="_______-sflags_0x________Number______"></span><span id="_______-sflags_0x________number______"></span><span id="_______-SFLAGS_0X________NUMBER______"></span> **-sflags 0x** *Number*   
すべてのシンボルハンドラーオプションを一度に設定します。 *Number*は**0x**で始まる16進数の数字にする必要があります。 **0x**が指定されていない10進数を使用できますが、シンボルオプションはバイナリフラグであるため、16進数を使用することをお勧めします。 このオプションは、すべてのシンボルハンドラーの既定値をオーバーライドするため、注意して使用する必要があります。 詳細については、「[シンボルオプションの設定](symbol-options.md)」を参照してください。

<span id="_______-sicv______"></span><span id="_______-SICV______"></span> **-sicv**   
シンボルハンドラーが CV レコードを無視するようにします。 詳細およびこれを制御するその他の方法については、「 [Symopt\_IGNORE\_CVREC](symbol-options.md#symopt-ignore-cvrec)」を参照してください。

<span id="_______-sins______"></span><span id="_______-SINS______"></span> **-sins**   
デバッガーがシンボルパスと実行可能イメージパス環境変数を無視するようにします。 詳細については、「 [Symopt\_IGNORE\_NT\_SYMPATH](symbol-options.md#symopt-ignore-nt-sympath)」を参照してください。

<span id="_______-snc______"></span><span id="_______-SNC______"></span> **-snc**   
デバッガーが変換をオフC++にします。 詳細およびその他の制御方法については、「 [Symopt\_no\_CPP](symbol-options.md#symopt-no-cpp)」を参照してください。

<span id="_______-snul______"></span><span id="_______-SNUL______"></span> **-snul**   
非修飾名に対するシンボルの自動読み込みを無効にします。 詳細およびその他の制御方法については、「 [Symopt\_no\_非修飾\_読み込み](symbol-options.md#symopt-no-unqualified-loads)」を参照してください。

<span id="_______-srcpath_______SourcePath______"></span><span id="_______-srcpath_______sourcepath______"></span><span id="_______-SRCPATH_______SOURCEPATH______"></span> **-srcpath** *SourcePath*   
ソースファイルの検索パスを指定します。 複数のパスはセミコロン ( **;** ) で区切ります。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細について、およびこのパスを変更するその他の方法については、「[ソースパス](source-path.md)」を参照してください。

<span id="_______-sup______"></span><span id="_______-SUP______"></span> **-sup**   
シンボルを検索するたびに、シンボルハンドラーがパブリックシンボルテーブルを検索します。 詳細およびその他の制御方法については、「 [Symopt\_AUTO\_PUBLICS](symbol-options.md#symopt-auto-publics)」を参照してください。

<span id="_______-T_______Title______"></span><span id="_______-t_______title______"></span><span id="_______-T_______TITLE______"></span> **-T** *タイトル*   
WinDbg ウィンドウのタイトルを設定します。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
デバッガーからの詳細出力を有効にします。

<span id="_______-W_______Workspace______"></span><span id="_______-w_______workspace______"></span><span id="_______-W_______WORKSPACE______"></span> **-W** *ワークスペース*   
指定された名前付きワークスペースを読み込みます。 ワークスペース名にスペースが含まれている場合は、引用符で囲みます。 この名前のワークスペースが存在しない場合は、この名前で新しいワークスペースを作成するか、読み込みの試行を破棄するかを選択できます。 詳細については、「[ワークスペースの使用](using-workspaces.md)」を参照してください。

<span id="_______-WF_______Filename______"></span><span id="_______-wf_______filename______"></span><span id="_______-WF_______FILENAME______"></span> **-WF** *ファイル名*   
指定されたファイルからワークスペースを読み込みます。 *Filename*には、ファイルと拡張子 (通常は wew) を含める必要があります。 ワークスペース名にスペースが含まれている場合は、引用符で囲みます。 この名前のワークスペースファイルが存在しない場合は、この名前で新しいワークスペースファイルを作成するか、読み込みの試行を破棄するかを選択できます。 詳細については、「[ワークスペースの使用](using-workspaces.md)」を参照してください。

<span id="_______-WX______"></span><span id="_______-wx______"></span> **-WX**   
ワークスペースの自動読み込みを無効にします。 詳細については、「[ワークスペースの使用](using-workspaces.md)」を参照してください。

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span> **-y** *シンボルパス*   
シンボルの検索パスを指定します。 複数のパスはセミコロン ( **;** ) で区切ります。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細およびこのパスを変更するその他の方法については、「[シンボルパス](symbol-path.md)」を参照してください。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span> **-z** *ダンプファイル*   
デバッグするクラッシュダンプファイルの名前を指定します。 パスとファイル名にスペースが含まれている場合、引用符で囲む必要があります。 複数**の**ダンプファイルを同時に開くことができます。その際、それぞれに異なる*ダンプファイル*値を指定します。 詳細については、「[ユーザーモードのダンプファイルの分析](analyzing-a-user-mode-dump-file.md)」または「 [WinDbg を使用したカーネルモードのダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)」を参照してください。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span> **-zp** *ページファイル*   
変更されたページファイルの名前を指定します。 これは、ダンプファイルをデバッグしていて、[**ページイン (Page In Memory)** ](-pagein--page-in-memory-.md)コマンドを使用する場合に便利です。 標準の Windows ページファイルで **-zp**を使用することはできません。特別に変更されたページファイルのみ使用できます。

<span id="_______executable______"></span><span id="_______EXECUTABLE______"></span>*実行可能ファイル*   
実行可能プロセスのコマンドラインを指定します。 これは、新しいプロセスを起動してデバッグするために使用されます。 これは、コマンドラインの最後の項目である必要があります。 実行可能ファイル名の後にあるすべてのテキストが、実行可能ファイルに引数文字列として渡されます。 詳細については、「 [WinDbg を使用したユーザーモードプロセスのデバッグ](debugging-a-user-mode-process-using-windbg.md)」を参照してください。

<span id="_______-_______"></span> **-?**    
この HTML ヘルプウィンドウをポップアップ表示します。

コマンドラインからデバッガーを実行する場合は、アプリケーションのファイル名の後に対象アプリケーションの引数を指定します。 例:

```dbgcmd
windbg myexe arg1 arg2
```

 

 





